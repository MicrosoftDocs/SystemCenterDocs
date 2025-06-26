---
ms.assetid: e357ab3b-45b3-417e-8a41-84c4cc66b4a0
title: Low-privilege monitoring in Management Pack for SQL Server
description: This article explains low-privilege monitoring
author: Anastas1ya
ms.author: v-fkornilov
manager: evansma
ms.date: 11/26/2024
ms.topic: concept-article
ms.service: system-center
ms.subservice: operations-manager
---

# Low-Privilege Monitoring

All workflows (discoveries, rules, monitors, and actions) in this management pack are bound to [Run As Profiles](sql-server-management-pack-run-as-profiles.md).

To enable low-privilege monitoring, grant appropriate permissions to Run As accounts and map these accounts to respective Run As Profiles.

> [!NOTE]
> The **Virtual Log File Count** monitor (VLF) doesn't support low-privilege monitoring on SQL Servers 2012 and 2014.

## Create Active Directory accounts

1. In Active Directory, create the following domain users for low-privilege access to the target SQL Server instances:

    - SQLTaskAction
    - SQLDiscovery
    - SQLMonitor

2. Create the **SQLMPLowPriv** domain group and add the following domain users to this group:

    - SQLDiscovery
    - SQLMonitor

3. Add the **SQLMPLowPriv** group to the [Read-only Domain Controllers](/windows-server/identity/ad-ds/manage/understand-security-groups#read-only-domain-controllers) Active Directory security group.

## Agent Monitoring

This section explains how to configure low-privilege agent monitoring.

### On Agents

1. Grant the **SQLTaskAction** user and the **SQLMPLowPriv** group the **Read** permission for the registry key:
    `HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server`

2. On each monitored instance, grant the **SQLMPLowPriv** group the **Read** permission for the registry key:
    `HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\[InstanceID]\MSSQLServer\Parameters`

3. Add the **SQLTaskAction** and **SQLMonitor** users to the [Event Log Readers](/windows-server/identity/ad-ds/manage/understand-security-groups#event-log-readers) Active Directory security local group.

4. Grant **Execute Methods**, **Enable Account**, **Remote Enable**, and **Read Security** permissions to **SQLTaskAction** and **SQLMPLowPriv** for the following WMI namespaces using the [WMI Control](/windows/win32/wmisdk/setting-namespace-security-with-the-wmi-control):

    - ROOT
    - ROOT\CIMV2
    - ROOT\DEFAULT
    - ROOT\Microsoft\SqlServer\ComputerManagement11 (if exists)
    - ROOT\Microsoft\SqlServer\ComputerManagement12 (if exists)
    - ROOT\Microsoft\SqlServer\ComputerManagement13 (if exists)
    - ROOT\Microsoft\SqlServer\ComputerManagement14 (if exists)
    - ROOT\Microsoft\SqlServer\ComputerManagement15 (if exists)
    - ROOT\Microsoft\SqlServer\ComputerManagement16 (if exists)

5. Configure the **Allow log on locally** local security policy to allow the **SQLTaskAction** user and the **SQLMPLowPriv** domain group users to log on locally.

    > [!NOTE]
    > If you're using System Center Operations Manager 2016, follow the steps above to provide **Allow log on locally** permission to Run As accounts. [Learn more](/windows/security/threat-protection/security-policy-settings/allow-log-on-locally).

6. Configure the **Log on as a Service** local security policy to allow the **SQLTaskAction** user and the **SQLMPLowPriv** domain group users to sign in as a service.

    > [!NOTE]
    > If you're using System Center Operations Manager 2019 or higher, follow the steps above to provide **Log on as a Service** permission to Run As accounts. [Learn more](./enable-service-logon.md).

7. In the **Microsoft Monitoring Agent** properties for the selected management group, set the **Local System** account to perform agent actions.

### Extra Steps for Cluster SQL Server Instances

1. Take the steps above for each cluster node.

2. Grant to **SQLMPLowPriv** and **SQLTaskAction** the **Remote Launch** and **Remote Activation** DCOM permissions using [DCOMCNFG](/windows/win32/com/setting-machine-wide-security-using-dcomcnfg).

3. Allow **Windows Remote Management** through Windows Firewall.

4. Grant the **SQLMPLowPriv** group **Full Control** to the cluster using Failover Cluster Manager.

5. Grant **Execute Methods**, **Enable Account**, **Remote Enable**, and **Read Security** permissions to **SQLTaskAction** and **SQLMPLowPriv** for the **root\MSCluster** WMI namespace using the [WMI Control](/windows/win32/wmisdk/setting-namespace-security-with-the-wmi-control).

### On SQL Server Instances

1. Open SQL Server Management Studio and connect to the SQL Server Database Engine instance.

2. In SQL Server Management Studio, for each instance of SQL Server Database Engine running on a monitored server, use the following SQL script to create and set the lowest privilege configuration for the **SQLMPLowPriv** domain account:

    ```SQL
    USE [master];
    SET NOCOUNT ON;
    /*The domain account that System Center Operations Manager will use
    to access the SQL Server instance*/
    DECLARE @accountname sysname = '<domainName>\<login_name>';
    /*In some cases, administrators change the 'sa' account default name.
    This will retrieve the name of the account associated to princicpal_id = 1*/
    DECLARE @sa_name sysname = 'sa';
    SELECT @sa_name = [name] FROM sys.server_principals WHERE principal_id = 1
    /*Create the server role with authorization to the account associated to principal id = 1.
    Create the role only if it does not already exist*/
    DECLARE @createSrvRoleCommand nvarchar(200);
    SET @createSrvRoleCommand = 'IF NOT EXISTS (SELECT 1 FROM sys.server_principals
        WHERE [name] = ''SCOM_SQLMPLowPriv'') BEGIN
        CREATE SERVER ROLE [SCOM_SQLMPLowPriv] AUTHORIZATION [' + @sa_name + ']; END'
    EXEC(@createSrvRoleCommand);
    GRANT VIEW ANY DATABASE TO [SCOM_SQLMPLowPriv];
    GRANT VIEW ANY DEFINITION TO [SCOM_SQLMPLowPriv];
    GRANT VIEW SERVER STATE TO [SCOM_SQLMPLowPriv];
    DECLARE @createLoginCommand nvarchar(200);
    SET @createLoginCommand = 'IF NOT EXISTS (SELECT 1 FROM sys.server_principals
        WHERE [name] = '''+ @accountname +''') BEGIN
        CREATE LOGIN '+ QUOTENAME(@accountname) +' FROM WINDOWS WITH DEFAULT_DATABASE=[master]; END'
    EXEC(@createLoginCommand);
    -- Add the login to the user-defined server role
    DECLARE @addServerMemberCommand nvarchar(200);
    SET @addServerMemberCommand = 'ALTER SERVER ROLE [SCOM_SQLMPLowPriv] ADD MEMBER '
    + QUOTENAME(@accountname) + ';'
    EXEC(@addServerMemberCommand);
    -- Add the login and database role to each database
    DECLARE @createDatabaseUserAndRole nvarchar(max);
    SET @createDatabaseUserAndRole = '';
    SELECT @createDatabaseUserAndRole = @createDatabaseUserAndRole + ' USE ' + QUOTENAME(db.name) + ';
        IF NOT EXISTS (SELECT 1 FROM sys.database_principals WHERE [name] = '''+ @accountname +''') BEGIN
        CREATE USER ' + QUOTENAME(@accountname) + ' FOR LOGIN ' + QUOTENAME(@accountname) + '; END;
        IF NOT EXISTS (SELECT 1 FROM sys.database_principals WHERE [name] = ''SCOM_SQLMPLowPriv'') BEGIN
        CREATE ROLE [SCOM_SQLMPLowPriv] AUTHORIZATION [dbo]; END;
        ALTER ROLE [SCOM_SQLMPLowPriv] ADD MEMBER ' + QUOTENAME(@accountname) + ';'
    FROM sys.databases db
        LEFT JOIN sys.dm_hadr_availability_replica_states hadrstate ON
            db.replica_id = hadrstate.replica_id
    WHERE db.database_id <> 2
        AND db.user_access = 0
        AND db.state = 0
        AND db.is_read_only = 0
        AND (hadrstate.role = 1 or hadrstate.role is null);
    EXEC(@createDatabaseUserAndRole);
    -- Add database specific permissions to database role
    USE [master];
    GRANT EXECUTE ON sys.xp_readerrorlog TO [SCOM_SQLMPLowPriv];
    GRANT EXECUTE ON sys.xp_instance_regread TO [SCOM_SQLMPLowPriv];
    GRANT SELECT ON [sys].[indexes] TO [SCOM_SQLMPLowPriv];
    GRANT SELECT ON [sys].[tables] TO [SCOM_SQLMPLowPriv];
    GRANT SELECT ON [sys].[dm_db_index_physical_stats] TO [SCOM_SQLMPLowPriv];
    USE [msdb];
    GRANT SELECT ON [dbo].[sysjobschedules] TO [SCOM_SQLMPLowPriv];
    GRANT SELECT ON [dbo].[sysschedules] TO [SCOM_SQLMPLowPriv];
    GRANT SELECT ON [dbo].[syscategories] TO [SCOM_SQLMPLowPriv];
    GRANT SELECT ON [dbo].[sysjobs_view] TO [SCOM_SQLMPLowPriv];
    GRANT SELECT ON [dbo].[sysjobactivity] TO [SCOM_SQLMPLowPriv];
    GRANT SELECT ON [dbo].[sysjobhistory] TO [SCOM_SQLMPLowPriv];
    GRANT SELECT ON [dbo].[syssessions] TO [SCOM_SQLMPLowPriv];
    GRANT SELECT ON [dbo].[log_shipping_primary_databases] TO [SCOM_SQLMPLowPriv];
    GRANT SELECT ON [dbo].[log_shipping_secondary_databases] TO [SCOM_SQLMPLowPriv];
    GRANT SELECT ON [dbo].[log_shipping_monitor_history_detail] TO [SCOM_SQLMPLowPriv];
    GRANT SELECT ON [dbo].[log_shipping_monitor_secondary] TO [SCOM_SQLMPLowPriv];
    GRANT SELECT ON [dbo].[log_shipping_monitor_primary] TO [SCOM_SQLMPLowPriv];
    GRANT EXECUTE ON [dbo].[sp_help_job] TO [SCOM_SQLMPLowPriv];
    GRANT EXECUTE ON [dbo].[agent_datetime] TO [SCOM_SQLMPLowPriv];
    GRANT EXECUTE ON [dbo].[SQLAGENT_SUSER_SNAME] TO [SCOM_SQLMPLowPriv];
    ALTER ROLE [SQLAgentReaderRole] ADD MEMBER [SCOM_SQLMPLowPriv];
    ```

### On SMB Shares

1. Grant share permissions by opening the share properties dialog for the share that hosts SQL Server data files or SQL Server transaction log files.

2. Grant the **Read** permission to **SQLMPLowPriv**.

3. Grant NTFS permissions by opening the properties dialog for the shared folder and navigating to the **Security** tab.

4. Grant the **Read** permission to **SQLMPLowPriv**.

### Optional Steps for Tasks on Agents

Some optional System Center Operations Manager tasks require a higher privilege on an agent machine and/or database to allow task execution.

Take the following steps on an agent machine or database only if you want to allow the System Center Operations Manager console operator to take remedial actions:

1. If the task is related to starting or stopping an NT service (such as DB Engine Service, SQL Server Agent service, SQL Full Text Search Service, Integration Services), on the agent machine, grant the **SQLTaskAction** user the permission to start or stop an NT service. This involves setting a service security descriptor. For more information, see [Sc sdset](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc742037(v=ws.10)).

    Read the existing privileges for the given service using **sc sdshow** and grant extra privileges to the **SQLTaskAction** user.

    For example, if the results of the **sdshow** command for SQL Server service are as follows:

    ```CONSOLE
    *D:(A;;CCLCSWRPWPDTLOCRRC;;;SY)(A;;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;BA)(A;;CCLCSWLOCRRC;;;IU)(A;;CCLCSWLOCRRC;;;SU)S:(AU;FA;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;WD)*
    ```

    In this case, the following command grants sufficient access to **SQLTaskAction** for starting and stopping the SQL Server service. Replace 'SQLServerServiceName' and 'SID for SQLTaskAction' with the appropriate values and keep everything on a single line.

    ```CONSOLE
    *sc sdset SQLServerServiceName D:(A;;GRRPWP;;;SID for SQLTaskAction)(A;;CCLCSWRPWPDTLOCRRC;;;SY)(A;;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;BA)(A;;CCLCSWLOCRRC;;;IU)(A;;CCLCSWLOCRRC;;;SU)S:(AU;FA;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;WD)*
    ```

2. In SQL Server Management Studio, for each instance of SQL Server Database Engine running on a monitored server, create a login for **SQLTaskAction**:

    ```sql
    USE [msdb];
    CREATE USER [SQLTaskAction] FOR LOGIN [SQLTaskAction];
    ```

3. Grant the **db_owner** database role for each database if the task is related to performing database checks:

    - Check Catalog (DBCC)
    - Check Database (DBCC)
    - Check Disk (DBCC) (invokes DBCC CHECKALLOC)

    ```sql
    USE [yourdatabase];
    ALTER ROLE [db_owner] ADD MEMBER [SQLTaskAction];
    ```

4. Grant the **ALTER ANY DATABASE** privilege to the **SQLTaskAction** login to run the task if the task is related to changing the database state:

    - Set Database Offline
    - Set Database Online
    - Set Database to Emergency State

    ```sql
    USE [master];
    GRANT ALTER ANY DATABASE TO [SQLTaskAction];
    ```

### In System Center Operations Manager

1. [Import SQL Server Management Pack](sql-server-management-pack-management-pack-delivery.md).

2. Create the following Windows-based Run As accounts:

    - SQLTaskAction
    - SQLDiscovery
    - SQLMonitor

3. In System Center Operations Manager console, configure Run As Profiles as follows:

    - Set the **Microsoft SQL Server Task** Run As Profile to use the **SQLTaskAction** Run As account.
    - Set the **Microsoft SQL Server Discovery** Run As Profile to use the **SQLDiscovery** Run As account.
    - Set the **Microsoft SQL Server Monitoring** Run As profile to use the **SQLMonitor** Run As account.

To prevent SQL Server monitoring issues, the **SQLTaskAction**, **SQLDiscovery**, and **SQLMonitor** Run As accounts should be used to manage the target as the **Windows Computer** object.

## Agentless Monitoring

[Applicable to SQL Server on Windows and on Linux]

This section explains how to configure low-privilege agentless monitoring.

### On SQL Server Instances

1. Open SQL Server Management Studio and connect to the SQL Server Database Engine instance.

2. In SQL Server Management Studio, for each instance of SQL Server Database Engine running on a monitored server, use the following SQL script to create and set the lowest privilege configuration for the **SQLMPLowPriv** account with Active Directory authentication:

     ```SQL
    USE [master];
    SET NOCOUNT ON;
    /*The user account with SQL Server authentication that System Center Operations Manager
    will use to access the SQL Server instance*/
    DECLARE @accountname sysname = '<domainName>\<login_name>';
    /*In some cases, administrators change the 'sa' account default name.
    This will retrieve the name of the account associated to princicpal_id = 1*/
    DECLARE @sa_name sysname = 'sa';
    SELECT @sa_name = [name] FROM sys.server_principals WHERE principal_id = 1
    /*Create the server role with authorization to the account associated to principal id = 1.
    Create the role only if it does not already exist*/
    DECLARE @createSrvRoleCommand nvarchar(200);
    SET @createSrvRoleCommand = 'IF NOT EXISTS (SELECT 1 FROM sys.server_principals
        WHERE [name] = ''SCOM_SQLMPLowPriv'') BEGIN
        CREATE SERVER ROLE [SCOM_SQLMPLowPriv] AUTHORIZATION [' + @sa_name + ']; END'
    EXEC(@createSrvRoleCommand);
    GRANT VIEW ANY DATABASE TO [SCOM_SQLMPLowPriv];
    GRANT VIEW ANY DEFINITION TO [SCOM_SQLMPLowPriv];
    GRANT VIEW SERVER STATE TO [SCOM_SQLMPLowPriv];
    DECLARE @createLoginCommand nvarchar(200);
    /*Create the login with SQL Server authentication using the password,
    and replace it with your value below*/
    SET @createLoginCommand = 'IF NOT EXISTS (SELECT 1 FROM sys.server_principals
        WHERE [name] = '''+ @accountname +''') BEGIN
        CREATE LOGIN '+ QUOTENAME(@accountname) +' FROM WINDOWS WITH DEFAULT_DATABASE=[master]; END'
    EXEC(@createLoginCommand);
    -- Add the login to the user-defined server role
    DECLARE @addServerMemberCommand nvarchar(200);
    SET @addServerMemberCommand = 'ALTER SERVER ROLE [SCOM_SQLMPLowPriv] ADD MEMBER '
    + QUOTENAME(@accountname) + ';'
    EXEC(@addServerMemberCommand);
    -- Add the login and database role to each database
    DECLARE @createDatabaseUserAndRole nvarchar(max);
    SET @createDatabaseUserAndRole = '';
    SELECT @createDatabaseUserAndRole = @createDatabaseUserAndRole + ' USE ' + QUOTENAME(db.name) + ';
        IF NOT EXISTS (SELECT 1 FROM sys.database_principals WHERE [name] = '''+ @accountname +''') BEGIN
        CREATE USER ' + QUOTENAME(@accountname) + ' FOR LOGIN ' + QUOTENAME(@accountname) + '; END;
        IF NOT EXISTS (SELECT 1 FROM sys.database_principals WHERE [name] = ''SCOM_SQLMPLowPriv'') BEGIN
        CREATE ROLE [SCOM_SQLMPLowPriv] AUTHORIZATION [dbo]; END;
        ALTER ROLE [SCOM_SQLMPLowPriv] ADD MEMBER ' + QUOTENAME(@accountname) + ';'
    FROM sys.databases db
        LEFT JOIN sys.dm_hadr_availability_replica_states hadrstate ON
            db.replica_id = hadrstate.replica_id
    WHERE db.database_id <> 2
        AND db.user_access = 0
        AND db.state = 0
        AND db.is_read_only = 0
        AND (hadrstate.role = 1 or hadrstate.role is null);
    EXEC(@createDatabaseUserAndRole);
    -- Add database specific permissions to database role
    USE [master];
    GRANT EXECUTE ON sys.xp_readerrorlog TO [SCOM_SQLMPLowPriv];
    GRANT EXECUTE ON sys.xp_instance_regread TO [SCOM_SQLMPLowPriv];
    USE [msdb];
    GRANT SELECT ON [dbo].[sysjobschedules] TO [SCOM_SQLMPLowPriv];
    GRANT SELECT ON [dbo].[sysschedules] TO [SCOM_SQLMPLowPriv];
    GRANT SELECT ON [dbo].[syscategories] TO [SCOM_SQLMPLowPriv];
    GRANT SELECT ON [dbo].[sysjobs_view] TO [SCOM_SQLMPLowPriv];
    GRANT SELECT ON [dbo].[sysjobactivity] TO [SCOM_SQLMPLowPriv];
    GRANT SELECT ON [dbo].[sysjobhistory] TO [SCOM_SQLMPLowPriv];
    GRANT SELECT ON [dbo].[syssessions] TO [SCOM_SQLMPLowPriv];
    GRANT SELECT ON [dbo].[log_shipping_primary_databases] TO [SCOM_SQLMPLowPriv];
    GRANT SELECT ON [dbo].[log_shipping_secondary_databases] TO [SCOM_SQLMPLowPriv];
    GRANT SELECT ON [dbo].[log_shipping_monitor_history_detail] TO [SCOM_SQLMPLowPriv];
    GRANT SELECT ON [dbo].[log_shipping_monitor_secondary] TO [SCOM_SQLMPLowPriv];
    GRANT SELECT ON [dbo].[log_shipping_monitor_primary] TO [SCOM_SQLMPLowPriv];
    GRANT EXECUTE ON [dbo].[sp_help_job] TO [SCOM_SQLMPLowPriv];
    GRANT EXECUTE ON [dbo].[agent_datetime] TO [SCOM_SQLMPLowPriv];
    GRANT EXECUTE ON [dbo].[SQLAGENT_SUSER_SNAME] TO [SCOM_SQLMPLowPriv];
    ALTER ROLE [SQLAgentReaderRole] ADD MEMBER [SCOM_SQLMPLowPriv];
    ```

Some optional System Center Operations Manager tasks require a higher privilege on an agent machine and/or database to allow task execution.

Take the following steps only if you want to allow the System Center Operations Manager console operator to take remedial actions on that target:

1. In SQL Server Management Studio, for each instance of SQL Server Database Engine running on a monitored server, create a login for **SQLTaskAction**:

    ```sql
    USE [msdb];
    CREATE USER [SQLTaskAction] FOR LOGIN [SQLTaskAction];
    ```

2. Grant the **db_owner** database role for each database if the task is related to performing database checks:

    - Check Catalog (DBCC)
    - Check Database (DBCC)
    - Check Disk (DBCC) (invokes DBCC CHECKALLOC)

    ```sql
    USE [yourdatabase];
    ALTER ROLE [db_owner] ADD MEMBER [SQLTaskAction];
    ```

3. Grant the **ALTER ANY DATABASE** privilege to the **SQLTaskAction** login to run the task if the task is related to changing the database state:

    - Set Database Offline
    - Set Database Online
    - Set Database to Emergency State

    ```sql
    USE [master];
    GRANT ALTER ANY DATABASE TO [SQLTaskAction];
    ```

### Using Monitoring Wizard

To configure low-privilege agentless monitoring using the monitoring wizard, perform the steps provided in the [Configuring Agentless Monitoring Mode](sql-server-management-pack-monitoring-modes.md#configuring-agentless-monitoring-mode) section, but with the following changes:

1. In the **Add Monitoring Wizard** window, select **Add Instances**.

2. In the **Add Instances** window, select a common Run As account with the appropriate SQL low-privilege login, and specify data sources and/or connection strings.

    For example:

     - 192.0.2.10;MachineName="_server-name_";InstanceName="_instance-name_";Platform="Windows"
     - 192.0.2.11,50626;MachineName="_server-name_";InstanceName="_instance-name_";Platform="Windows"
     - 192.0.2.15;MachineName="_server-name_";InstanceName="_instance-name_";Platform="Linux"

    You can also create a new Run As account. For that, in the **Add Instances** window, select **New**, enter a new name for the Run As account, and specify credentials to access the SQL Server that you want to monitor.

    ![Screenshot of Run As account.](./media/sql-server-management-pack/adding-run-as-account.png)

    After the connection is established, you can view and edit properties of the added instance.

    ![Screenshot of Instance properties.](./media/sql-server-management-pack/modifying-instance-properties.png)

## Mixed Monitoring

To configure low-privilege [mixed monitoring](sql-server-management-pack-monitoring-modes.md#configuring-mixed-monitoring-mode), perform the steps described in the [Agent Monitoring](#agent-monitoring) section and do the following:

- [Configure remote access to WMI](#managing-remote-access-to-wmi)

- [Grant permissions to get information about the services](#granting-service-permissions)

- [Use a registry key to manage the remote access to the registry](#managing-remote-access-to-the-registry)

### Managing Remote Access to WMI

To configure security for configurations with low-privilege accounts, perform the following steps on each mixed mode monitoring server:

1. Launch the **mmc.exe** console and add the following snap-ins:

    - Component Services
    - WMI Control (for a local computer)

2. Expand **Component Services**, right-click **My Computer**, and select **Properties**.

   ![Screenshot of opening properties.](./media/sql-server-management-pack/component-service-properties.png)

3. Open the **COM Security** tab.

4. In the **Launch and Activation Permissions** section, select **Edit Limits**.

   ![Screenshot of editing limits.](./media/sql-server-management-pack/editing-limits.png)

5. Grant the following permissions to the remote machine account:

    - Remote Launch
    - Remote Activation

   ![Screenshot of activating permissions.](./media/sql-server-management-pack/launch-activate-permissions.png)

6. Go to the **WMI Control** snap-in and open its properties.

7. Open the **Security** tab and select the following namespaces:

    - ROOT\CIMV2
    - ROOT\Microsoft\SqlServer
    - ROOT\Microsoft\SqlServer\ComputerManagement11 (if exists)
    - ROOT\Microsoft\SqlServer\ComputerManagement12 (if exists)
    - ROOT\Microsoft\SqlServer\ComputerManagement13 (if exists)
    - ROOT\Microsoft\SqlServer\ComputerManagement14 (if exists)
    - ROOT\Microsoft\SqlServer\ComputerManagement15 (if exists)
    - ROOT\Microsoft\SqlServer\ComputerManagement16 (if exists)

8. Select **Security**.

9. Grant the following permissions to the target computer:

    - Enable Account
    - Remote Enable

   ![Screenshot of security permissions.](./media/sql-server-management-pack/security-permissions.png)

10. Select **Advanced**.

11. Select the target account and select **Edit**.

12. From the **Applies to** dropdown list, select **This namespace only**.

13. In the **Permissions** section, enable the following checkboxes:

    - Enable Account
    - Remote Enable

    ![Screenshot of configuring CIMV permissions.](./media/sql-server-management-pack/permissions-cimv.png)

### Granting Service Permissions

To get information about the services, grant required permissions according to the following steps:

1. Open the PowerShell console.

2. Run the following command to retrieve a **Spotlight User** SID.

    ```powershell
    function GetSidByName($userName){
    $objUser = New-Object System.Security.Principal.NTAccount($userName)
    $strSID = $objUser.Translate([System.Security.Principal.SecurityIdentifier])
    return $strSID.Value
    }
    GetSidByName 'domainName\userName'
    ```

    Replace **domainName\userName** with the domain and user names for the **Spotlight User** account.

    ![Screeshot of replacing spotlite user.](./media/sql-server-management-pack/ps-spotlight-user.png)

3. From the Windows command prompt, run the following command to retrieve the current SDDL for the Services Control Manager:

    ```CONSOLE
    sc sdshow scmanager > file.txt
    ```

    The SDDL is saved to the **file.txt** file and looks similar to the following one:

    ```CONSOLE
    D:(A;;CC;;;AU)(A;;CCLCRPRC;;;IU)(A;;CCLCRPRC;;;SU)(A;;CCLCRPWPRC;;;SY)(A;;KA;;;BA)S:(AU;FA;KA;;;WD)(AU;OIIOFA;GA;;;WD).
    ```

4. Modify the SDDL string by copying the SDDL section that ends in **IU** (Interactive Users).

    This section is enclosed in parentheses (that is, A;;CCLCRPRC;;;IU). Paste this clause directly after the clause you've copied.

    Replace the IU string with the **Spotlight User** SID in the following text.

    The new SDDL looks similar to the following one:

    ```CONSOLE
    D:(A;;CC;;;AU)(A;;CCLCRPRC;;;IU) (A;;CCLCRPRC;;;A-1-22-3-4444444444-5555555555-6666666-7777777777)(A;;CCLCRPRC;;;SU)(A;;CCLCRPWPRC;;;SY)(A;;KA;;;BA) S:(AU;FA;KA;;;WD)(AU;OIIOFA;GA;;;WD)
    ```

5. Set the security credentials to access the Service Control Manager by using the **sdset** command.

    ```CONSOLE
    sc sdset scmanager "D:(A;;CC;;;AU)(A;;CCLCRPRC;;;IU)(A;;CCLCRPRC;;;SU)(A;;CCLCRPWPRC;;;SY)(A;;KA;;;BA)(A;;CCLCRPRC;;;A-1-22-3-4444444444-5555555555-6666666-7777777777)S:(AU;FA;KA;;;WD)(AU;OIIOFA;GA;;;WD)"
    ```

6. Set rights for SQL Server, SQL agent, and SQL Full-text Filter Daemon Launcher services by using the **Command-Line Tool SubInACL** utility for the **Spotlight User** SID.

    Run the utility with the following options:

    ```CONSOLE
    subinacl.exe /service mssqlserver /GRANT= A-1-22-3-4444444444-5555555555-6666666-7777777777=LQSEI

    subinacl.exe /service sqlserveragent /GRANT= A-1-22-3-4444444444-5555555555-6666666-7777777777=LQSEI

    subinacl.exe /service mssqlfdlauncher /GRANT= A-1-22-3-4444444444-5555555555-6666666-7777777777=LQSEI
    ```

    ![Screenshot of running subinacl.](./media/sql-server-management-pack/subinacl-run.png)

    The following rights can be read as:

      - L: Read contro
      - Q: Query Service Configuration
      - S: Query Service Status
      - E: Enumerate Dependent Services
      - I: Interrogate Service

7. Set the rights for **ClusSvc** (Cluster Service) using the **Command-Line Tool SubInACL** utility for the **Spotlight User** SID.

    Run the utility with the following options:

    ```CONSOLE
    subinacl.exe /service clussvc /GRANT= A-1-22-3-4444444444-5555555555-6666666-7777777777=LQSEI
    ```

### Managing Remote Access to the Registry

Create a registry key to manage remote access to the registry.

To create a key, perform the following steps:

1. Open **Registry Editor**, and locate the following key `HKLM\SYSTEM\CurrentControlSet\Control`

2. In the **Edit** menu, select **Add Key** and enter the following values:

    - **Key Name:** SecurePipeServers
    - **Class:** REG_SZ

3. Locate the following key `HKLM\SYSTEM\CurrentControlSet\Control\SecurePipeServers`

4. In the **Edit** menu, select **Add Key** and enter the following values:

    - **Key Name:** winreg
    - **Class:** REG_SZ

5. Locate the following key: `HKLM\SYSTEM\CurrentControlSet\Control\SecurePipeServers\winreg`

6. In the **Edit** menu, select **Add Key** and enter the following values:

    - **Value Name:** Description
    - **Data Type:** REG_SZ
    - **String:** Registry Server

7. Locate the following key: `HKLM\SYSTEM\CurrentControlSet\Control\SecurePipeServers\winreg`

8. Right-click **winreg**, select **Permissions**, and edit the current permissions, or add users or groups you want to grant access to.

9. Quit **Registry Editor** and restart Windows.
