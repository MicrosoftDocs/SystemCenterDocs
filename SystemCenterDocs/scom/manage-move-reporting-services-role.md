---
ms.assetid: 
title:  How to move the Reporting Server role
description: This article describes the steps required to move the Reporting server role to a new computer.
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 02/11/2018
ms.custom: na
ms.prod: system-center-2016
ms.technology: operations-manager
ms.topic: article
---

# How to Move the Reporting Server Role

You can move the System Center Operations Manager Reporting server component to a new server, or reinstall the component on the original server.  

During this move, Operations Manager stops storing data in the OperationsManagerDW database until you complete the Operations Manager reporting server reinstall.

Use the procedures in this article to move the reporting server to a new server and verify the success of the move. You must back up any custom reports authored outside of Operations Manager, favorites, and schedules which are stored in the report server database.  For more information about the preparation and steps required to move the SQL Server reporting services installation, see [Moving the Report Server Databases to Another Computer (SSRS Native Mode)](https://docs.microsoft.com/sql/reporting-services/report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode).

>[!NOTE]
>Ensure that you follow all steps precisely, as not doing so might result in data corruption.

## Migration Overview
The migration process for Reporting Services includes manual and automated steps. The following tasks are part of a report server migration: 

- Back up databases and configuration files, such as **Web.config** if you configured report server to enable FIPS compliance. 
- Back up the encryption key. 
- Install a new instance of SQL Server. If you are using the same hardware, you can install SQL Server side-by-side with your existing installation if it was one of the supported versions. 
- Configure the report server. 
- Install Operations Manager Reporting server component. 
- Move the report server database from your existing installation to your new SQL Server installation. 
- Restore settings defined in **Web.config ** to include custom settings enabled in the previous configuration. 

## Backup data

1. Create a full backup of the data warehouse database. The default name is **OperationsManagerDW**.  Also create a full backup of the **ReportServer** and **ReportServerTempDB** database.  For more information, see [Create a Full Database Backup (SQL Server)](https://docs.microsoft.com/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server).
2. On the current Operations Manager reporting server, backup the SSRS encryption key.  For more information, see [SSRS Encryption Keys - Back Up and Restore Encryption Keys](https://docs.microsoft.com/sql/reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys).
3. Back up the report server configuration files. Files to back up include: 
   - Web.config 

## Uninstall Operations Manager reporting server

1. On the current Operations Manager reporting server, uninstall the Operations Manager reporting server component as follows:  
   a. Open Control Panel, and then click **Programs and Features**.  
   b. In **Programs and Features**, select **System Center 2016 Operations Manager**, and then click **Uninstall/Change**.  
   c. In the **Operations Manager Setup** wizard, click **Remove a feature**.  
   d. In the **Select features to remove** page, select **Reporting server**, and then click **Uninstall**. Click **Close** when the wizard finishes.  

2. On the SQL Server instance hosting the data warehosue database, restore the data warehouse database you previously backed up.  For more information, see [Restore a Database Backup (SQL Server Management Studio)](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms).  

## Install SQL Server Reporting Services

1. If you are installing the Operations Manager reporting server component on a new server, perform a [new install SQL Server Reporting Services](https://docs.microsoft.com/sql/reporting-services/install-windows/install-reporting-services-native-mode-report-server).   
2. If you are reinstalling the Operations Manager reporting server component on the original server, you must remove any data that is left from the original installation by doing the following:  
   a. Copy the ResetSRS.exe tool from the SupportTools folder on the product source media to a local folder.  
   b. Open a command prompt window using the Run as Administrator option and run the tool as follows: `ResetSRS.exe <SQL Server instance name>`.  Here, SQL Server instance name is the SQL Server instance that SQL Reporting Services is installed on, such as **Instance1**. If SQL Server is using the default instance, enter **MSSQLSERVER**.  
   d. Configure the report server Web service and portal URL, and report server database using the Reporting Services Configuration tool.  For more information, see [Configure a Report Server (Reporting Services Native Mode)](https://docs.microsoft.com/sql/reporting-services/report-server/configure-a-report-server-reporting-services-native-mode).  

## Verify the installation of your report server

1. Run the Reporting Services Configuration tool and connect to the report server instance you just installed. The Web Service URL page includes a link to the Report Server Web service. Click the link to verify you can access the server. 
2. Open a browser and type the report server URL in the address bar. The address consists of the server name and the virtual directory name that you specified for the report server during setup. By default, the report server virtual directory is named **ReportServer**. You can use the following URL to verify report server installation: *http://<computer name>/ReportServer<_instance name>*. The URL will be different if you installed the report server as a named instance. 
3. To verify that the web portal is installed and running, open a browser and type the Web Portal URL in the address bar. The address consists of the server name and the virtual directory name that you specified for the web portal during setup or in the Web Portal URL page in the Reporting Services Configuration tool. By default, the web portal virtual directory is **Reports**. You can use the following URL to verify the web portal installation: *http://<computer name>/Reports<_instance name>*. 

## Install Operations Manager Reporting server

1. On the new Operations Manager reporting server, install the Operations Manager Reporting server component as follows: 
   a. On the **Configuration, SQL Server instance for reporting services** page, make sure the SQL Server instance refers to the new SQL Server instance.  
   b. On the **Configuration, Configure Operation Manager accounts** page, be sure the Data Reader account is the same account previously used for the report server.  

If you are restoring the original configuration on a new SQL Server reporting services instance, restore the original **ReportServer** and **ReportServerTempDB** databases for SQL Server Reporting services to preserve your custom reports, favorites, schedules from the original reporting services deployment.  
   a. Verify the **RSExecRole** is a database role with the report server database and temporary database. **RSExecRole** must have **select, insert, update, delete, and reference** permissions in the report server database tables, and **execute** permissions on the stored procedures.  
   b. On the new Reporting Services server, open **Report Services Configuration Tool** and connect to the new instance.  Select the original report server database and click **Apply**.  
   c. Restore the encryption keys you backed up in step 2.  For more information, see [SSRS Encryption Keys - Back Up and Restore Encryption Keys](https://docs.microsoft.com/sql/reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys).  

After completing the installation and post-configuration steps, perform the following to confirm Operations Manager reporting is working correctly.

1. Verify that you can successfully run a report from the Operations console.
2. Ensure that the health state of all Management servers is **Healthy**.

## Next steps

* See [How to move the Operational database](manage-move-opsdb.md) to understand the sequence and steps for moving the Operations Manager operational database to a new SQL Server instance.  

* See [How to move the Reporting data warehouse database](manage-move-omdwdb.md) to understand the sequence and steps for moving the Operations Manager Reporting data warehouse database to a new SQL Server instance.