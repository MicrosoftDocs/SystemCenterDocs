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

- **Agent monitoring mode**
  
    This monitoring mode supports SQL on Windows only and is performed by the SCOM Agent.

    In this monitoring mode, the management pack automatically discovers stand-alone and clustered instances of SQL Server across all managed systems that run the System Center Operations Manager agent service.

- **Agentess monitoring mode**

    This monitoring mode supports both SQL on Linux and SQL on Windows.

    In this monitoring mode, the management pack workflows run on Management Servers and Gateway Servers, both of which are mapped to **SQL Server Monitoring Pool**. If SQL Server Monitoring Pool is not configured, **All Management Servers Pool** is used.

    This monitoring mode does not provide automatic discovery of SQL Server instances. To discover SQL Server instances, add them to the monitoring list manually, as described in [Configuring Agentless Monitoring Mode](#configuring-agentless-monitoring-mode).

    To make monitoring more efficient, configure a dedicated pool of Management Servers, as described in [Configuring SQL Server Monitoring Pool](./ssmp-configuring-sql-server-monitoring-pool.md).

- **Mixed monitoring mode**

    This monitoring mode supports SQL on Windows only.

    In this monitoring mode, the management pack places its seed on each computer that has the SCOM Agent and uses this seed to automatically discover all SQL Server on Windows instances. The entire monitoring is performed from Management Servers and Gateway Servers that are members of the SQL Server Monitoring Pool.

    For more information on how to configure this mode, see [Configuring Mixed Monitoring Mode](#configuring-mixed-monitoring-mode).

Each of these modes supports both the SQL Server and the Windows authentication.

## Agentless and Mixed Modes Performance

When either agentless or mixed monitoring mode is used, management pack workflows that run on Management Servers are mapped to either **SQL Server Monitoring Pool** or **All Management Servers Pool**. In this case, Management Servers experience a higher load than in the agent monitoring mode.

The following monitoring configuration is validated for both agentless and mixed monitoring modes:

- SCOM Server 1

    Azure size: Standard DS12_v2, 4 vcpus, 28 GB memory, 12800 IOPS, Windows Server 2012R2, SCOM 2012R2

- SCOM Server 2 – a server dedicated to monitor SQL Server. The only member of the SQL Server Monitoring Pool.

    Azure size: Standard DS12\_v2, 4 vcpus, 28 GB memory, 12800 IOPS, Windows Server 2012R2, SCOM 2012R2.

- 12 VMs with SQL Server (2012, 2014, 2016, 2017) – 600 databases per instance, \~40000 SQL Server MP objects in total.

More than half of its CPU and RAM resources were available on the SCOM Server 2 during the performance testing session.

## Configuring Agentless Monitoring Mode

To configure agentless monitoring, perform the following steps:

1. In the Operations Manager console, navigate to **Authoring** | **Management Pack Templates**, right-click **Microsoft SQL Server** and select **Add Monitoring Wizard**.

    ![Configuring Agentless Monitoring Mode](media/ssmp/running-add-monitoring-wizard.png)

2. At the **Monitoring Type** step, select **Microsoft SQL Server** and click **Next**.

    ![Configuring Agentless Monitoring Mode](media/ssmp/selecting-sql-server.png)

3. At the **General Properties** step, enter a new name and description, and from the **Select destination management pack** drop-down list, select a management pack that you want to use to store the template.

    ![Configuring Agentless Monitoring Mode](media/ssmp/entering-name.png)

    To create a new management pack, click **New**.

4. At the **Service Details** step, click **Add Instances** to add instances that you want to monitor.

    ![Configuring Agentless Monitoring Mode](media/ssmp/adding-instances.png)

5. In the **Add Instances** window, perform the following:

    - Select a preferable authentication type, which can be either **SQL Credentials** or **Windows AD credentials**.

      The **Windows AD credentials** method should be used when SQL Server instances run on Windows or Linux servers that are part of an Active Directory domain.

    - Select a common Run As Account created in the Operations Manager with appropriate credentials or create a new one by clicking **New**.

      When creating a new Run as Account, enter a name and credentials to connect to the SQL server that you want to monitor and click **OK**.

    - Specify data sources and/or connection strings. Follow the instructions provided in this window to avoid errors and skip excessive connection testing.

      The following are examples of the format that should be used when specifying connection strings:

        - 172.31.2.133;MachineName="W12BOX-839";InstanceName="MSSQLSERVER";Platform="Windows"
  
        - 172.31.2.133,50626;MachineName="W12BOX-839";InstanceName="SQLEXPRESS";Platform="Windows"

        - 172.17.5.115;MachineName="ubuntu";InstanceName="MSSQLSERVER";Platform="Linux"

     When adding a Linux-based instance, connection tests fail if an IP address is specified as a connection string and the authentication type is **Windows AD credentials**. In this case, specify the machine name as the connection string.

    ![Configuring Agentless Monitoring Mode](./media/ssmp/authentication-type.png)

6. Click **OK** and wait until connection is established.

    **Monitoring Template Wizard** may show the following error when establishing connection: "An error occurred discovery: A connection was successfully established with the server, but then an error occurred during the login process".

    To workaround this issue, decrease intervals for both the **MSSQL: Generic Monitoring Pool Watcher Discovery** discovery and the **Discover All Management Servers Pool Watcher** discovery to force them to run right away, then restore the previous value.

    Once connection is established, you can view and edit properties of the instance by selecting the instance and clicking **Edit Instance**.

    ![Configuring Agentless Monitoring Mode](./media/ssmp/editing-instance-configuration.png)

    To skip connection testing and enter data manually, select the **Skip Test Connection and enter this data manually** checkbox.

7. At the **Summary** step, review summary information and click **Create**.

    ![Configuring Agentless Monitoring Mode](./media/ssmp/server-details-summary.png)

## Configuring Mixed Monitoring Mode

Use mixed monitoring mode when you want to switch monitoring from the agent to a SCOM pool.

In this monitoring mode, you do not need to configure connection strings manually. Instead, you can use overrides.

When enabling mixed monitoring mode, only a SQL Server seed is discovered locally by the SCOM agent. All other workflows are executed on a dedicated Management Server Pool.

To configure mixed monitoring, perform the following steps:

1. In the Operations Manager console, navigate to **Authoring** | **Management Pack Objects** and select **Object Discoveries**.

2. Right-click **MSSQL: Discover Local SQL Database Engines on Windows** and select **Overrides** > **Override the Object Discovery** > **For all objects of class: MSSQL on Windows: Local Discovery Seed**.

    ![Configuring Mixed Monitoring Mode](./media/ssmp/local-discovery-seed.png)

3. In the **Override Properties** window, enable the **Mixed Monitoring** override and in the **Override Value** field, specify instances that you want to switch to agentless monitoring.
  
    Use commas to separate instance names. If you want to add all instances, including instances that have the same name but are located on different servers, enter an asterisk character (\*).

    ![Configuring Mixed Monitoring Mode](./media/ssmp/override-properties.png)
