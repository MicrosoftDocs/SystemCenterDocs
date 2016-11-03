---
ms.assetid: 033e12cc-1265-48a2-848c-acbc316d8ad5
title: How to Move the Operational Database
description: This article describes how to move the Operations Manager operational database to a different SQL Server instance after initial deployment.  
author: mgoedtel
ms.author: magoedte
manager: cfreeman
ms.date: 11/02/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# How to Move the Operational Database

>Applies To: System Center 2016 - Operations Manager

After the initial deployment of System Center 2016 – Operations Manager, you might need to move the operational database from one Microsoft SQL Server-based computer to another.

During the move, you need to stop services on your management servers, back up the database, restore the database, update the registry and configuration file on management servers, update database tables, add new Logins, and modify User Mapping settings for Logins. For more information, see [SQL Server documentation](https://msdn.microsoft.com/library/mt590198%28v=sql.1%29.aspx).

> [!CAUTION]
> This procedure can result in data loss if it is not performed correctly and within a reasonable length of time of the failure. Ensure that you follow all steps precisely, without unnecessary delays between the steps.

## Summary of steps

1. Stop Operation Manager services on all management servers in the management group
2. Create a backup of the operational database and move it to the new SQL server instance
3. Restore the operational database on the new SQL Server instance
4. Update the registry and configuration files on all management servers
5. Update the operational database with the new database server name and instance
6. Update the operational database with the new database server name to specify the location of the Application Performance Monitoring tables
7. Update security credentials on the new SQL Server instance hosting the operational database
8. Start Operation Manager services on all management servers

## Moving the Operational database

### Stop the Operations Manager services

1. On all the management servers in the management group, stop the Operations Manager services: 
  - System Center Data Access
  - Microsoft Monitoring Agent
  - System Center Management Configuration

### Backup the Operational database on the old SQL Server instance

2. On the original SQL Server instance hosting the operational database, use Microsoft SQL Server Management Studio to create a full backup of the database. The default name is OperationsManager.
  
    For more information, see [How to: Back Up a Database (SQL Server Management Studio)](https://technet.microsoft.com/library/ms187510.aspx).

3. Copy the backup file to a local drive of the new SQL Server instance.

### Restore the Operational database on the new SQL Server instance

1. Use Microsoft SQL Server Management Studio to restore the operational database. (In the previous step, you moved the database backup file to a local drive of the new SQL Server instance.) In this step, you can change the name of the database and choose the file location.
  
    For more information, see [How to: Restore a Database Backup (SQL Server Management Studio)](https://technet.microsoft.com/library/ms177429.aspx).

2. In SQL Server Management Studio, verify that the database is online.

### Update the registry and configuration files on the management servers, and Operational database

After moving the Operations Manager operational database to a different SQL Server instance, you will need to follow the steps below to reconfigure all management servers in the management group to reference the new computer name and instance.  This requires modifying the registry, the configuration service configuration file, and several tables in the operational database.  The steps are detailed in the [How to configure Operations Manager to communicate with SQL Server](how-to-configure-operations-manager-to-communicate-with-sqlserver.md#how-to-configure-the-operations-manager-database).

### Update security credentials on the new SQL Server instance hosting the operational database 

1.	On the new SQL Server instance hosting the operational database, open SQL Management Studio.  
2.	Expand **Security**, then expand **Logins**, and add the data writer account name. 
3.	Under **Logins**, add the data writer account. For more information, see [How to Create a SQL Server Login](https://technet.microsoft.com/library/aa337562.aspx).
4.	Under **Logins**, add the management server action account.  
5.	Under **Logins**, add the Data Access Service (DAS) user account, using the format "domain\user".
6.	For the DAS user account, add the following user mappings:
  -	ConfigService
  -	db_accessadmin
  -	db_datareader
  -	db_datawriter
  -	db_ddladmin
  -	db_securityadmin
  -	sdk_users
  -	sql_dependency_subscriber

7. If an account has not existed before in the SQL Server instance in which you are adding it, the mapping will be picked up by SID automatically from the restored operational  database. If the account has existed in that SQL Server instance before, you receive an error indicating failure for that login, although the account appears under **Logins**. If you are creating a new login, ensure the User Mapping for that log in and database are set to the same values as the previous login as follows:

    | Login | Database| 
    |-------|----------|
    | DW Data Writer | - apm_datareader<br>- apm_datawriter<br>- db_datareader<br>-  dwsynch_users|
    | Action account | - db_datareader<br>- db_datawriter<br>- db_ddladmin<br>- dbmodule_users|
    | DAS/Configuration account | - ConfigService<br>- db_accessadmin<br>- db_datareader<br>- db_datawriter<br>- db_ddladmin<br>- db_securityadmin<br>- sdk_users<br>- sql_dependency_subscriber|

    > [!NOTE] 
    > If the DAS/Configuration account uses the LocalSystem account, specify computer account in the form <domain>\<computername>$.

8. Run the following command on the new SQL Server instance hosting the Operations Manager operational database.  
   ```
    sp_configure 'show advanced options', 1;
    GO
    RECONFIGURE;
    GO
    sp_configure 'clr enabled', 1;
    GO
    RECONFIGURE;
    GO
   ```

9. Run the following SQL query:
   `SELECT is_broker_enabled FROM sys.databases WHERE name='OperationsManager'`

    If the result of this query was an is_broker_enabled value of 1, skip this step. Otherwise, run the following SQL queries:

    `ALTER DATABASE OperationsManager SET SINGLE_USER WITH ROLLBACK IMMEDIATE`  
    `ALTER DATABASE OperationsManager SET ENABLE_BROKER`  
    `ALTER DATABASE OperationsManager SET MULTI_USER`  

###  Start the Operations Manager services

1. On all the management servers in the management group, start the Operations Manager services: 
  - System Center Data Access
  - Microsoft Monitoring Agent
  - System Center Management Configuration
 
## Next steps

- See [How to move the Reporting data warehouse database](how-to-move-the-reporting-data-warehouse-database.md) to understand the sequence and steps for moving the Operations Manager Reporting data warehouse database to a new SQL Server instance.
