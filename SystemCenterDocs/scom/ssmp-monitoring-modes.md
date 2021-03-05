---
ms.assetid: 5be59923-32d6-4758-b078-a26bf85ae28b
title: Monitoring Modes
description: This article explains monitoring modes in Management Pack for SQL Server
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 2/5/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Monitoring Modes

Management Pack for SQL Server provides the following monitoring modes:

- **Agent monitoring**
  
    Agent monitoring is performed by the System Center Operations Manager agent and supports SQL on Windows only.

    In this monitoring mode, the management pack automatically discovers stand-alone and clustered instances of SQL Server across all managed systems that run the System Center Operations Manager agent service.

    The following protocols are supported in this mode: 
    
    - TCP/IP
    
    - Named Pipes
    
    - Shared Memory

- **Agentess monitoring**

    This monitoring mode supports both SQL on Linux and SQL on Windows.

    In this monitoring mode, the management pack workflows run on Management Servers and Gateway Servers. Both servers are mapped to **SQL Server Monitoring Pool**. If SQL Server Monitoring Pool is not configured, **All Management Servers Pool** is used.

    This monitoring mode does not provide automatic discovery of SQL Server instances. To discover SQL Server instances, add them to the monitoring list manually, as described in [Configuring Agentless Monitoring Mode](#configuring-agentless-monitoring-mode).

    To make monitoring more efficient, configure a dedicated pool of Management Servers, as described in [Configuring SQL Server Monitoring Pool](ssmp-sql-server-monitoring-pool.md).

    The following protocols are supported in this mode: 
    
    - TCP/IP
    
    - Named Pipes

- **Mixed monitoring**

    This monitoring mode supports SQL on Windows only.

    In this monitoring mode, the management pack places its seed on each computer that has the System Center Operations Manager agent. This seed is then used to automatically discover all SQL Server on Windows instances. The entire monitoring is performed by Management Servers and Gateway Servers that are members of the SQL Server Monitoring Pool.

    For more information on how to configure this mode, see [Configuring Mixed Monitoring Mode](#configuring-mixed-monitoring-mode).

    Only the TCP/IP protocol is supported in this mode.

Each of these modes supports both the SQL Server and the Windows authentication.

## Configuring Agentless Monitoring Mode

To configure agentless monitoring, perform the following steps:

1. In the Operations Manager console, navigate to **Authoring** | **Management Pack Templates**, right-click **Microsoft SQL Server**, and select **Add Monitoring Wizard**.

    ![Running Add Monitoring Wizard](media/ssmp/running-add-monitoring-wizard.png)

2. At the **Monitoring Type** step, select **Microsoft SQL Server**, and click **Next**.

    ![Selecting SQL Server](media/ssmp/selecting-sql-server.png)

3. At the **General Properties** step, enter a new name and description.

4. From the **Select destination management pack** drop-down list, select a management pack that you want to use to store the template.

    ![Entering name](media/ssmp/entering-name.png)

    To create a new management pack, click **New**.

5. At the **Service Details** step, click **Add Instances** to add instances that you want to monitor.

    ![Adding instances](media/ssmp/adding-instances.png)

6. In the **Add Instances** window, perform the following steps:

    - Select a preferable authentication type, which can be either **SQL Credentials** or **Windows AD credentials**.

      Use the **Windows AD credentials** method when SQL Server instances run on Windows or Linux-based servers that are part of an Active Directory domain.

    - Select a common Run As Account created in the Operations Manager with appropriate credentials or create a new one by clicking **New**.

      When you create a new Run As account, enter a name and credentials to connect to the SQL server that you want to monitor and click **OK**.

    - Specify data sources and/or connection strings.

      Use the following format when specifying connection strings:

        - 172.31.2.133;MachineName="W12BOX-839";InstanceName="MSSQLSERVER";Platform="Windows"
  
        - 172.31.2.133,50626;MachineName="W12BOX-839";InstanceName="SQLEXPRESS";Platform="Windows"

        - 172.17.5.115;MachineName="ubuntu";InstanceName="MSSQLSERVER";Platform="Linux"
     
     When you add a Linux-based instance, a connection test will fail if an IP address is specified as a connection string and the authentication type is **Windows AD credentials**. In this case, specify the machine name as the connection string.

    ![Authentication type](./media/ssmp/authentication-type.png)

7. Click **OK** and wait until the connection is established.

    **Monitoring Template Wizard** may show the following error when establishing connection: "An error occurred discovery: A connection was successfully established with the server, but then an error occurred during the login process".

    To workaround this issue, decrease intervals for both the **MSSQL: Generic Monitoring Pool Watcher Discovery** discovery and the **Discover All Management Servers Pool Watcher** discovery to force them to run right away, then restore the previous value.

    ![Decrease intervals](./media/ssmp/decrease-intervals.png)

    Once connection is established, you can view and edit properties of the instance. To view properties, select an instance and click **Edit Instance**.

    ![Editing instance configuration](./media/ssmp/editing-instance-configuration.png)

    To skip connection testing and enter data manually, select the **Skip Test Connection and enter this data manually** checkbox.

8. At the **Summary** step, review summary information and click **Create**.

    ![Server summary](./media/ssmp/server-details-summary.png)

## Configuring Mixed Monitoring Mode

Use mixed monitoring mode when you want to switch monitoring from the agent to a System Center Operations Manager pool.

In this monitoring mode, you do not need to configure connection strings manually. Instead, you can use overrides.

When enabling mixed monitoring mode, only a SQL Server seed is discovered locally by the System Center Operations Manager agent. All other workflows are executed on a dedicated Management Server Pool.

To configure mixed monitoring, perform the following steps:

1. In the Operations Manager console, navigate to **Authoring** | **Management Pack Objects** and select **Object Discoveries**.

2. Right-click **MSSQL: Discover Local SQL Database Engines on Windows** and select **Overrides** > **Override the Object Discovery** > **For all objects of class: MSSQL on Windows: Local Discovery Seed**.

    ![Local discovery seed](./media/ssmp/local-discovery-seed.png)

3. In the **Override Properties** window, enable the **Mixed Monitoring** override.

4. In the **Override Value** field, specify instances that you want to switch to agentless monitoring.
  
    Use commas to separate instance names. To add all instances, including instances with the same name and instances that are located on different servers, use asterisk (\'*').

    ![Override properties](./media/ssmp/override-properties.png)

## Agentless and Mixed Modes Performance

When you use either agentless or mixed monitoring mode, the management pack workflows are mapped to either **SQL Server Monitoring Pool** or **All Management Servers Pool**. In this case, Management Servers experience a higher load than in the agent monitoring mode.

The following monitoring configuration is validated for both agentless and mixed monitoring modes:

- System Center Operations Manager Server 1

    Azure tier: Standard DS12_v2, 4 vcpus, 28GB memory, 12800 IOPS, Windows Server 2012R2, System Center Operations Manager 2012R2

- System Center Operations Manager Server 2 – a server dedicated to monitor SQL Server. The only member of the SQL Server Monitoring Pool.

    Azure tier: Standard DS12\_v2, 4 vcpus, 28GB memory, 12800 IOPS, Windows Server 2012R2, System Center Operations Manager 2012R2.

- 12 VMs with SQL Server (2012, 2014, 2016, 2017) – 600 databases per instance, \~40000 SQL Server MP objects in total.

More than half of its CPU and RAM resources were available on the System Center Operations Manager Server 2 during the performance testing session.

## Viewing Monitoring Type

Management Pack for SQL Server allows you to customize views and configure auxiliary columns that show used monitoring types.

To view currently used monitoring types, perform the following steps:

1. Right-click the **Database Engines** view and select **Personalize View**.

2. In the **Columns to display** list, select the **Monitoring Type** checkbox.

    ![Monitoring type](./media/ssmp/monitoring-type-view.png)

    After enabling the **Monitoring Type** checkbox, used monitoring types become available in the **Database Engines** table.

    ![Monitoring types view](./media/ssmp/enabled-monitoring-types.png)