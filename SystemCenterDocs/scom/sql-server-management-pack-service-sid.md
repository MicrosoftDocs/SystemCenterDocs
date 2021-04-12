---
ms.assetid: 8f280433-6981-402e-b94d-ba2e9ae97b81
title: Service SID in Management Pack for SQL Server
description: This article explains how to configure monitoring with serivce SID
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Service SID

Below are the steps to configure monitoring using Service SIDs for SQL Server on a Windows Server instance. These steps were first published by Kevin Holman in [his blog](https://kevinholman.com/2016/08/25/sql-mp-run-as-accounts-no-longer-required/). The SQL scripts to configure lowest-privilege access were developed by Brandon Adams.

To configure monitoring using Service Security Identifier, perform the following steps:

1. Open the command prompt as administrator and run the **sc sidtype HealthService unrestricted** command.

2. Restart the Health Service.

3. Run the **sc showsid HealthService** command. 

    The **STATUS** parameter should be active.

    ![Running HealthService](./media/sql-server-management-pack/health-service-command.png)

4. Open **Registry Editor** and check that the **ServiceSidType** key is set to 1 at *HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\HealthService*.

5. Create the NT SERVICE\HealthService login for the HealthService SID on every SQL Server Instance and grant it SA rights. 

    If you cannot grant SA rights, use the following SQL scripts to set the lowest privilege configuration for the account.

    ```sql
    USE [master]
    SET NOCOUNT ON
    /*User account that System Center Operations Manager will use to access
        Default is the Service SID for the HealthService*/
    DECLARE @accountname sysname = 'NT SERVICE\HealthService'
    -- Create the server role and grant permissions
    CREATE SERVER ROLE [SCOM_HealthService]
    GRANT VIEW ANY DATABASE TO [SCOM_HealthService];
    GRANT ALTER ANY DATABASE TO [SCOM_HealthService];
    GRANT VIEW ANY DEFINITION TO [SCOM_HealthService];
    GRANT VIEW SERVER STATE TO [SCOM_HealthService]
    DECLARE @createLoginCommand nvarchar(200)
    SET @createLoginCommand = '
      CREATE LOGIN '+ QUOTENAME(@accountname) +
      ' FROM WINDOWS WITH DEFAULT_DATABASE=[master];'
    EXEC(@createLoginCommand);
    -- Add the login to the user-defined server role
    EXEC sp_addsrvrolemember @loginame = @accountname
      , @rolename = 'SCOM_HealthService'
    DECLARE @createDatabaseUserAndRole nvarchar(max)
    SET @createDatabaseUserAndRole = '';
    SELECT @createDatabaseUserAndRole = @createDatabaseUserAndRole + '
      USE ' + QUOTENAME(db.name) + ';
      CREATE USER ' + QUOTENAME(@accountname) +
      ' FOR LOGIN ' + QUOTENAME(@accountname) + ';
      CREATE ROLE [SCOM_HealthService];
      EXEC sp_addrolemember @rolename =
      ''SCOM_HealthService'', @membername
      = '+ QUOTENAME(@accountname) + ''
    -- 'ALTER ROLE [SCOM_HealthService] ADD MEMBER '
      -- '+ QUOTENAME(@accountname) + ';'
    FROM sys.databases db
    LEFT JOIN sys.dm_hadr_availability_replica_states hadrstate ON
        db.replica_id = hadrstate.replica_id
    WHERE db.database_id <> 2
        AND db.user_access = 0
        AND db.state = 0
        AND db.is_read_only = 0
        AND (hadrstate.role = 1 or hadrstate.role is null);
    EXEC(@createDatabaseUserAndRole)
    GO
    USE [master];
    GRANT EXECUTE ON sys.xp_readerrorlog
      TO [SCOM_HealthService]
    USE [msdb];
    GRANT SELECT on [dbo].[sysjobschedules]
      TO [SCOM_HealthService];
    GRANT SELECT on [dbo].[sysschedules]
      TO [SCOM_HealthService];
    GRANT SELECT on [dbo].[sysjobs_view]
      TO [SCOM_HealthService];
    GRANT SELECT on [dbo].[log_shipping_primary_databases]
      TO [SCOM_HealthService];
    GRANT SELECT on [dbo].[log_shipping_secondary_databases]
      TO [SCOM_HealthService];
    GRANT SELECT on [dbo].[log_shipping_monitor_history_detail]
      TO [SCOM_HealthService];
    GRANT SELECT on [dbo].[log_shipping_monitor_secondary]
      TO [SCOM_HealthService];
    GRANT SELECT on [dbo].[log_shipping_monitor_primary]
      TO [SCOM_HealthService];
    GRANT EXECUTE on [dbo].[sp_help_job]
      TO [SCOM_HealthService];
    GRANT EXECUTE on [dbo].[sp_help_jobactivity]
      TO [SCOM_HealthService];
    EXEC sp_addrolemember @rolename='PolicyAdministratorRole'
      , @membername='SCOM_HealthService';
    EXEC sp_addrolemember @rolename='SQLAgentReaderRole'
      , @membername='SCOM_HealthService';
    ```

6. To run SQL Server MP tasks, such as **Set database Offline**, **Set database Online**, and **Set database to Emergency state**, grant HealthService SID account the **ALTER ANY DATABASE** permission.

    ```sql
    USE [master]
    GRANT ALTER ANY DATABASE TO [SCOM_HealthService];
    ```

The NT AUTHORITY\SYSTEM account needs to be present as a SQL login and must not be disabled. This login must also be present and enabled for cluster nodes and Always On.

## Service SID for SQL Server Cluster Instances and AG

To configure HealthService Service SID for monitoring of SQL Server failover cluster, perform the following steps for each cluster node:

1. Launch **mmc.exe** and add the following snap-ins:

    - Component Services
    - WMI Control (for the local computer)

2. Expand **Component Services**, right-click **My Computer**, select **Properties**, and open the **Security** tab.

3. In the **Launch and Activation Permissions** section, click **Edit Limits**.

    ![Editing limits](./media/sql-server-management-pack/editing-limits.png)

4. In the **Launch and Activation Permission** window, enable the following permissions for the NT SERVICE\\HealthService account:

    - Remote Launch
    - Remote Activation

    ![Allowing permissions](./media/sql-server-management-pack/allowing-permissions.png)

5. Go to the WMI Control snap-in and open its properties.

6. Open the **Security** tab, select the **Root\\CIMV2** namespace, and click **Security**.

7. Enable the following permissions for the NT SERVICE\\HealthService account:

    - Enable Account
    - Remote Enable

    ![HealthService permissions](./media/sql-server-management-pack/health-service-permissions.png)

8. Click **Advanced**.

9. In the **Permissions Entry for CIMV2** window, select a HealthService account, and click **Edit**. 

10. From the **Applies to** drop-down list, select **This namespace only**.

11. In the **Permissions** section, enable the following checkboxes:

    - Enable Account
    - Remote Enable

    ![CIMV permissions](./media/sql-server-management-pack/permissions-cimv.png)