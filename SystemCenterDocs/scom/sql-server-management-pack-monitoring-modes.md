---
ms.assetid: 5be59923-32d6-4758-b078-a26bf85ae28b
title: Monitoring modes in Management Pack for SQL Server
description: This article explains monitoring modes in Management Pack for SQL Server
author: epomortseva
ms.author: v-gajeronika
ms.date: 11/26/2024
ms.topic: how-to
ms.service: system-center
ms.subservice: operations-manager
ms.custom: sfi-image-nochange
---

# Monitoring Modes

Management Pack for SQL Server provides the following monitoring modes:

- **Agent monitoring**

    Agent monitoring is performed by the System Center Operations Manager agent and supports SQL on Windows only. In this monitoring mode, the management pack automatically discovers standalone and clustered instances of SQL Server across all managed systems that run the System Center Operations Manager agent service.

    The following protocols are supported in this mode:

    - TCP/IP

    - Named Pipes

    - Shared Memory

- [**Agentless monitoring**](#configuring-agentless-monitoring-mode)

    This monitoring mode supports both SQL on Linux and SQL on Windows. In this monitoring mode, the management pack workflows run on Management Servers and Gateway Servers. Both servers are mapped to **SQL Server Monitoring Pool**. If SQL Server monitoring pool isn't configured, **All Management Servers Pool** is used. Custom management server resource pools are also supported.

    This monitoring mode doesn't provide automatic discovery of SQL Server instances. To discover SQL Server instances, add them to the monitoring list manually with the **Monitoring Wizard** management pack template. To make monitoring more efficient, configure a dedicated pool of Management Servers, as described in [Configuring SQL Server Monitoring Pool](sql-server-management-pack-sql-server-monitoring-pool.md).

    The following protocols are supported in this mode:

    - TCP/IP

    - Named Pipes

- [**Mixed monitoring**](#configuring-mixed-monitoring-mode)

    This monitoring mode supports SQL on Windows only. In this monitoring mode, the management pack places its seed on each computer that has the System Center Operations Manager agent. This seed is then used to automatically discover all SQL Server on Windows instances. The entire monitoring is performed by Management Servers and Gateway Servers that are members of the **SQL Server Monitoring Pool**.

    > [!NOTE]
    > For mixed monitoring mode only the **SQL Server Monitoring Pool** is supported. Custom management server resource pools are not supported.

    Only the TCP/IP protocol is supported in this mode.

Each of these modes supports both the SQL Server and the Windows authentication.

## Configuring Agentless Monitoring Mode

To configure agentless monitoring, perform the following steps:

1. In the Operations Manager console, navigate to **Authoring** | **Management Pack Templates**, right-click **Microsoft SQL Server**, and select **Add Monitoring Wizard**.

    ![Screenshot showing Running Add Monitoring Wizard.](./media/sql-server-management-pack/authoring-add-monitoring-wizard.png)

2. At the **Monitoring Type** step, select **Microsoft SQL Server**, and select **Next**.

    ![Screenshot showing selecting SQL Server.](./media/sql-server-management-pack/selecting-sql-server-template.png)

3. At the **General Properties** step, enter a new name and description.

4. From the **Select destination management pack** dropdown list, select a management pack that you want to use to store the template.

    ![Screenshot showing Entering name.](./media/sql-server-management-pack/entering-name-wizard.png)

    To create a new management pack, select **New**.

5. At the **Service Details** step, select **Add Instances** to add instances that you want to monitor.

    ![Screenshot showing Adding instances.](./media/sql-server-management-pack/adding-instances-wizard.png)

6. In the **Add Instances** window, perform the following steps:

    - Select a preferable authentication type, which can be either **SQL Credentials** or **Windows AD credentials**.

      Use the **Windows AD credentials** method when SQL Server instances run on Windows or Linux-based servers that are part of an Active Directory domain.

    - Select a common Run As Account created in the Operations Manager with appropriate credentials or create a new one by selecting **New**.

      When you create a new Run As account, enter a name and credentials to connect to the SQL Server that you want to monitor and select **OK**.

    - Specify the management server resource pool. By default, the **SQL Server Monitoring Pool** is selected. This option allows you to use the custom management server resource pools. If the latter is used, make sure that the selected Run As account is distributed to the corresponding management pool. Otherwise, the monitoring wizard runs the Run As account distribution automatically.


        ![Screenshot showing automatically distribution of the Run As account.](./media/sql-server-management-pack/run-as-account-distribution.png)

    - Specify data sources and/or connection strings. 

      Use the following format when specifying connection strings:

        - 192.0.2.17;MachineName="*server-name*";InstanceName="*instance-name*";Platform="Windows"

        - 192.0.2.17,50626;MachineName="*server-name*";InstanceName="*instance-name*";Platform="Windows"

        - 192.0.2.18;MachineName="*server-name*";InstanceName="*instance-name*";Platform="Linux"

    ![Screenshot showing Authentication type.](./media/sql-server-management-pack/authentication-type-agentless-wizard.png)

    > [!TIP]
    > The connection test may fail if an IP address of a Linux-based instance is specified as a connection string and the authentication type is **Windows AD credentials**. To avoid that, specify the machine name as the connection string.

7. Select **OK** and wait until the connection is established.

    ![Screenshot showing Decrease intervals.](./media/sql-server-management-pack/decrease-intervals-wizard.png)

    > [!NOTE]
    > **Monitoring Template Wizard** may show the following error when establishing connection: "An error occurred discovery: A connection was successfully established with the server, but then an error occurred during the login process". To work around this issue, decrease intervals for both the **MSSQL: Generic Monitoring Pool Watcher Discovery** and the **Discover All Management Servers Pool Watcher** discoveries to force them to run right away, and then restore the previous value.

    Once the connection is established, you can view and edit the properties of the instance. To view properties, select an instance and select **Edit Instance**.

    ![Screenshot showing Editing instance configuration.](./media/sql-server-management-pack/editing-instance-configuration-agentless-wizard.png)

    To skip connection testing and enter data manually, select the **Skip Test Connection and enter this data manually** checkbox.

8. At the **Summary** step, review summary information and select **Create**.

    ![Screenshot showing Server summary.](./media/sql-server-management-pack/server-details-summary-wizard.png)

    > [!IMPORTANT]
    > To avoid double monitoring of the SQL Server instance and additional burden eventually, don't add the instance to the monitoring template wizard for **Agentless mode** if it is already monitoring in **Agent mode**.

## Configuring Mixed Monitoring Mode

Use the mixed monitoring mode when you want to switch monitoring from the agent to a System Center Operations Manager pool.

In this monitoring mode, you don't need to configure the connection strings manually. Instead, you can use overrides.

When enabling the mixed monitoring mode, only a SQL Server seed is discovered locally by the System Center Operations Manager agent. All other workflows are executed on a dedicated **SQL Server Monitoring Pool**.

> [!IMPORTANT]
> Consider using at least one management server in the **SQL Server Monitoring Pool** for valid mixed monitoring mode settings.

To configure mixed monitoring, perform the following steps:

1. In the Operations Manager console, navigate to **Authoring** | **Management Pack Objects**, and select **Object Discoveries**.

2. Right-click **MSSQL: Discover Local SQL Database Engines on Windows** and select **Overrides** > **Override the Object Discovery** > **For all objects of class: MSSQL on Windows: Local Discovery Seed**.

    ![Screenshot showing Local discovery seed.](./media/sql-server-management-pack/local-discovery-seed.png)

3. In the **Override Properties** window, enable the **Mixed Monitoring** override.

4. In the **Override Value** field, specify instances that you want to switch to agentless monitoring.

    Use commas to separate instance names. To add all instances, including instances with the same name and instances that are located on different servers, use asterisk (\'*').

    ![Screenshot showing Override properties.](./media/sql-server-management-pack/override-properties.png)

## Viewing Monitoring Type

Management Pack for SQL Server allows you to customize views and configure auxiliary columns that show used monitoring types.

To view currently used monitoring types, perform the following steps:

1. Right-click the **Database Engines** view and select **Personalize View**.

2. In the **Columns to display** list, select the **Monitoring Type** checkbox.

    ![Screenshot showing Monitoring type personalization.](./media/sql-server-management-pack/monitoring-type-personalize-view.png)

    After enabling the **Monitoring Type** checkbox, used monitoring types become available in the **Database Engines** table.

    ![Screenshot showing Monitoring types view](./media/sql-server-management-pack/enabled-monitoring-types.png)
