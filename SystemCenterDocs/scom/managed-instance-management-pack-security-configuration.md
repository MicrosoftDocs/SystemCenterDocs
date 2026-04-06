---
title: Security configuration in Management Pack for Azure SQL Managed Instance
description: Learn about the security configuration in Management Pack for Azure SQL Managed Instance.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.topic: concept-article
ms.service: system-center
ms.subservice: operations-manager
ms.custom: engagement-fy23
ms.update-cycle: 1095-days
---

# Security configuration in Management Pack for Azure SQL Managed Instance

Monitoring accounts, SQL accounts, and Microsoft Entra ID principals that Azure SQL Managed Instance Management Pack uses for monitoring should have enough permissions to access each managed instance that you specify in your monitoring templates.

## Configuring SQL Instance permissions

Every managed instance should have a sign-in account for the monitoring account. The account should be granted at least a minimum set of permissions to allow the management pack to operate (that is, in a least-privilege configuration).

> [!NOTE]
> While the sysadmin role provides all the necessary permissions for management pack operations, it is not recommended to assign this role to the monitoring user.

Create an Entra ID account for monitoring access. This account will be used by management pack to access Azure SQL Managed Instance.

For every Azure SQL Managed Instance create a login for the Entra ID account and use the script below as example to configure least-privilege monitoring. You don't need to run the script for each new database that you create after initial execution. The script updates the *model* database so that databases that you create later have the required user. But you do need to run this script for every database that was attached or restored after you initially executed the script.

```sql
--First script that:
-- - Grants server-level permissions to the monitoring account.
-- - Creates a user and role in the master, msdb, and model databases and grants the required permissions to it.
-- - Creates a user and role in all user databases.
USE [master];
SET NOCOUNT ON
DECLARE @accountname SYSNAME = 'example-account-name';
CREATE SERVER ROLE [MILowPriv_role];
GRANT VIEW ANY DEFINITION TO [MILowPriv_role];
GRANT VIEW ANY DATABASE TO [MILowPriv_role];
GRANT ALTER ANY DATABASE TO [MILowPriv_role];
GRANT VIEW SERVER STATE TO [MILowPriv_role];
EXEC sp_addsrvrolemember @loginame = @accountname, @rolename = 'MILowPriv_role';
DECLARE @createDatabaseUserAndRole nvarchar(max);
SET @createDatabaseUserAndRole = '';
SELECT @createDatabaseUserAndRole = @createDatabaseUserAndRole + 'USE ' + QUOTENAME(db.name) + ';
CREATE USER ' + QUOTENAME(@accountname) + ' FOR LOGIN ' + QUOTENAME(@accountname) + ';
CREATE ROLE [MILowPriv_role];
EXEC sp_addrolemember @rolename = ''MILowPriv_role'', @membername = ' + QUOTENAME(@accountname) + ''
FROM sys.databases db
WHERE db.database_id <> 2
AND db.user_access = 0
AND db.state = 0
AND db.is_read_only = 0;
EXEC (@createDatabaseUserAndRole);
GO
USE [master];
GRANT EXECUTE ON xp_readerrorlog TO [MILowPriv_role];
GRANT EXECUTE ON xp_instance_regread TO [MILowPriv_role];
GRANT EXECUTE ON xp_sqlagent_enum_jobs TO [MILowPriv_role];
GRANT EXECUTE ON sp_enumerrorlogs TO [MILowPriv_role];
USE [msdb];
GRANT EXECUTE ON sp_help_job TO [MILowPriv_role];
GRANT EXECUTE ON sp_help_jobactivity TO [MILowPriv_role];
GRANT SELECT ON sysjobschedules TO [MILowPriv_role];
GRANT SELECT ON backupset TO [MILowPriv_role];
EXEC sp_addrolemember @rolename='db_datareader', @membername='MILowPriv_role';
EXEC sp_addrolemember @rolename='db_owner', @membername='MILowPriv_role';
EXEC sp_addrolemember @rolename='SQLAgentReaderRole', @membername='MILowPriv_role';
```

This script adds the monitoring account to the db_owner role, which might not be allowed. The db_owner permissions are required to set management pack tasks to run Database Console Command (DBCC) checks. If you don't need these tasks, don't grant the permissions.

```sql
--Second script that adds MILowPriv user to db_owner role for master, msdb, model, and all user databases.
--This is only to enable running DBCC checks right on SCOM (Check Catalog, Check Database, Check Disk).
--If you don't need this functionality, don't run this script.
DECLARE @accountname sysname = 'example-account-name';
DECLARE @createDatabaseUserAndRole nvarchar(max);
SET @createDatabaseUserAndRole = '';
SELECT @createDatabaseUserAndRole = @createDatabaseUserAndRole + 'USE ' + QUOTENAME(db.name) + ';
EXEC sp_addrolemember @rolename = ''db_owner'', @membername = ' + QUOTENAME(@accountname) + ''
FROM sys.databases db
WHERE db.database_id <> 2
AND db.user_access = 0
AND db.state = 0
AND db.is_read_only = 0
EXEC (@createDatabaseUserAndRole);
GO
```

## Related Content

- [Automatic monitoring template with Service Principal Name](managed-instance-management-pack-automatic-monitoring-service-principal-name.md)

- [Manual monitoring template](managed-instance-management-pack-manual-monitoring.md)
