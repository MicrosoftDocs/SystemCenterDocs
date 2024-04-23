---
ms.assetid: 96f00b98-1044-41d5-abce-41d9dd67e11c
title: Security configuration in Management Pack for Azure SQL Managed Instance
description: This article explains a security configuration in Management Pack for Azure SQL Managed Instance
author: Anastas1ya
ms.author:v-fkornilov
manager: evansma
ms.date: 01/24/2023
ms.topic: article
ms.service: system-center
ms.subservice: operations-manager
ms.custom: engagement-fy23
---

# Security Configuration

Monitoring accounts, SQL accounts, and Azure Active Directory principles used by this management pack for monitoring should have enough permissions to access each managed instance specified in your monitoring templates.

Every managed instance should have a sign-in for the monitoring account. This sign-in should be granted either of the following permissions:

- Sysadmin rights

- Minimum level of permissions that allows the management pack to operate (that is, least-privilege configuration).

To configure least-privilege monitoring, use the following scripts as an example.

The following script should be run against every managed instance. When deploying new managed instances, ensure to run this script for each of these instances. You don't need to run the script for each new database that you've created after the initial execution. The script updates the **model** database so that later created databases will have the required user, but you need to run this script for every database that was attached or restored after the initial execution of this script.

```SQL
--First script that:
-- - Grants server-level permissions to the monitoring account.
-- - Creates a user and role in the master, msdb, and model databases and grants the required permissions to it.
-- - Creates a user and role in all user databases.
--Don't forget to replace 'YOURPASSWORD' with your value in @createLoginCommand variable.
USE [master];
SET NOCOUNT ON
DECLARE @accountname SYSNAME = 'MILowPriv';
CREATE SERVER ROLE [MILowPriv_role];
GRANT VIEW ANY DEFINITION TO [MILowPriv_role];
GRANT VIEW ANY DATABASE TO [MILowPriv_role];
GRANT ALTER ANY DATABASE TO [MILowPriv_role];
GRANT VIEW SERVER STATE TO [MILowPriv_role];
DECLARE @createLoginCommand nvarchar(200);
SET @createLoginCommand = 'CREATE LOGIN '+ QUOTENAME(@accountname) + ' WITH PASSWORD=N''YOURPASSWORD'', DEFAULT_DATABASE=[master];'
EXEC (@createLoginCommand);
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

This script adds the monitoring account to the **db_owner** role, which may not be allowed. The **db owner** permissions are required to enable the management pack tasks to run DBCC checks. If you don't need these tasks, don't give these permissions.

```SQL
--Second script that adds MILowPriv user to db_owner role for master, msdb, model, and all user databases.
--This is only to enable running DBCC checks right on SCOM (Check Catalog, Check Database, Check Disk).
--If you don't need this functionality, don't run this script.
DECLARE @accountname sysname = 'MILowPriv';
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
