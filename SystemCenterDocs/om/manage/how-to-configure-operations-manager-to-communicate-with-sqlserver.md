---
ms.assetid: 61bb5a83-479f-4cc1-b67a-9cd02fc91d2f
title: How to Configure Operations Manager to Communicate with SQL Server
description: This article describes how to reconfigure Operations Manager if you change the SQL Server configuration or SQL Server instance hosting its databases.  
author: mgoedtel
ms.author: magoedte
manager: cfreeman
ms.date: 11/01/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# How to configure Operations Manager to communicate with SQL Server

>Applies To: System Center 2016 - Operations Manager

If after installing System Center 2016 - Operations Manager, you move the Operations Manager operational or data warehouse database to a different SQL Server instance, move the databases to a SQL Server Always On availability group, or reconfigure the SQL Server instance, you will need to follow the steps below to reconfigure the management group to reference the new TCP/IP Port, instance name, or computer name.  

## How to configure the Operations Manager operational database

1.	On each management server run **regedit** from an elevated **Command Prompt**, then edit:

 -	`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\System Center\2010\Common\Database` 
	Change **DatabaseServerName** to `computer\<instance>` followed by a comma, and then the SQL Server port number `(computer\instance,portNumber)`.  If you are hosting the database on a SQL Server cluster, replace *computer* with the virtual network name of the cluster.  If the database is part of a SQL Always On Availability Group, replace `computer\<instance>` with the availability group listener name in the format of '<AvalabilityGroupListnerName,portNumber>`.    

 -	`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Operations Manager\3.0\Setup` 
	Change **DatabaseServerName** to `computer\<instance>` followed by a comma, and then the SQL Server port number `(computer\instance,portNumber)`.  If you are hosting the database on a SQL Server cluster, replace *computer* with the virtual network name of the cluster.  If the database is part of a SQL Always On Availability Group, replace `computer\<instance>` with the availability group listener name in the format of `<AvalabilityGroupListnerName,portNumber>`.  

2.	On each management server, edit the following file: `%ProgramFiles%\System Center 2016\Operations Manager\Server\ConfigService.config`:

 -	Under the tag `<Category Name=”Cmdb”>`, change the value for *ServerName* to `computer\<instance>` and change the value for *PortNumber* to the SQL Server port number.

 -	Under the tag ` <Name=”ConfigStore”>`, change the value for *ServerName* to `computer\<instance>` and change the value for *PortNumber* to the SQL Server port number.

3. On the SQL Server instance hosting the operational database, configure the following:

    a. Open SQL Server Management Studio.  
    b. In the Object Explorer pane, expand **Databases**, expand the operational database (for example, OperationsManager), expand **Tables**, right-click `dbo.MT_ManagementGroup`, and then click **Edit Top 200 Rows**.  In the results pane, scroll to the right to the column titled `SQLServerName_<guid>`.  
    d. In the first row, enter `computer\<instance>` followed by a comma, and then the SQL Server port number `(computer\instance,portNumber)`.  If you are hosting the database on a SQL Server cluster, replace *computer* with the virtual network name of the cluster.  If the database is part of a SQL Always On Availability Group, replace `computer\<instance>` with the availability group listener name in the format of `<AvalabilityGroupListnerName,portNumber>`.  
    e. Right-click `dbo.MT_Microsoft$SystemCenter$ManagementGroup` and then click **Edit Top 200 Rows**. In the results pane, scroll to the right to the column titled  `column.SQLServerName_<GUID>`.  
    f. In the first row, enter `computer\<instance>` followed by a comma, and then the SQL Server port number `(computer\instance,portNumber)`.  If you are hosting the database on a SQL Server cluster, replace *computer* with the virtual network name of the cluster.  If the database is part of a SQL Always On Availability Group, replace `computer\instance` with the availability group listener name in the format of `<AvalabilityGroupListnerName,portNumber>`.  
    g. Right-click `dbo.MT_Microsoft$SystemCenter$OpsMgrDB$AppMonitoring ` and then click **Edit Top 200 Rows**. In the results pane, scroll to the right to the column titled  `column.SQLServerName_<GUID>`.  
    h. In the first row, enter `computer\<instance>` followed by a comma, and then the SQL Server port number `(computer\instance,portNumber)`.  If you are hosting the database on a SQL Server cluster, replace *computer* with the virtual network name of the cluster.  If the database is part of a SQL Always On Availability Group, replace `computer\instance` with the availability group listener name in the format of `<AvalabilityGroupListnerName,portNumber>`.   


## How to configure the Operations Manager Reporting data warehouse database

1. On each management server run **regedit** from an elevated **Command Prompt**, then edit:

-	`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Operations Manager\3.0\Setup`  
    Change **DataWarehouseDBServerName** to `computer\<instance>` followed by a comma, and then the SQL Server port number `(computer\instance,portNumber)`.  If you are hosting the database on a SQL Server cluster, replace *computer* with the virtual network name of the cluster.  If the database is part of a SQL Always On Availability Group, replace `computer\<instance>` with the availability group listener name in the format of `<AvalabilityGroupListnerName,portNumber>`.  

2. On the SQL Server instance hosting the Reporting data warehouse database, configure the following:  

    a. Open SQL Server Management Studio.  
    b. In the Object Explorer pane, expand **Databases**, expand the operational database (for example, OperationsManager), expand **Tables**, right-click `dbo.MT_Microsoft$SystemCenter$DataWarehouse`, and then click **Edit Top 200 Rows**.  
    c. In the results pane, scroll to the right to the column titled  `MainDatabaseServerName_<GUID>`.  
    d. In the first row, enter `computer\<instance>` followed by a comma, and then the SQL Server port number `(computer\instance,portNumber)`.  If you are hosting the database on a SQL Server cluster, replace *computer* with the virtual network name of the cluster.  If the database is part of a SQL Always On Availability Group, replace `computer\instance` with the availability group listener name in the format of `<AvalabilityGroupListnerName,portNumber>`.  
    e. Right-click `dbo.MT_Microsoft$SystemCenter$DataWarehouse$AppMonitoring`, and then click **Edit Top 200 Rows**.  
    f. In the results pane, scroll to the right to the column titled  `MainDatabaseServerName_<GUID>`.  
    g. In the first row, enter `computer\<instance>` followed by a comma, and then the SQL Server port number `(computer\instance,portNumber)`.  If you are hosting the database on a SQL Server cluster, replace *computer* with the virtual network name of the cluster.  If the database is part of a SQL Always On Availability Group, replace `computer\instance` with the availability group listener name in the format of `<AvalabilityGroupListnerName,portNumber>`.  
    h. Right-click `dbo. MT_Microsoft$SystemCenter$DataWarehouse$AppMonitoring_Log`, and then click **Edit Top 200 Rows**.  
    i. In the results pane, scroll to the right to the column titled  `Post_MainDatabaseServerName_<GUID>`.  
    j. In the first row, enter `computer\<instance>` followed by a comma, and then the SQL Server port number `(computer\instance,portNumber)`.  If you are hosting the database on a SQL Server cluster, replace *computer* with the virtual network name of the cluster.  If the database is part of a SQL Always On Availability Group, replace `computer\instance` with the availability group listener name in the format of `<AvalabilityGroupListnerName,portNumber>`.  
    k. Right-click `dbo. MT_Microsoft$SystemCenter$DataWarehouse$`, and then click **Edit Top 200 Rows**.  
    l. In the results pane, scroll to the right to the column titled  `MainDatabaseServerName_<GUID>`.  
    m. In the first row, enter `computer\<instance>` followed by a comma, and then the SQL Server port number `(computer\instance,portNumber)`.  If you are hosting the database on a SQL Server cluster, replace *computer* with the virtual network name of the cluster.  If the database is part of a SQL Always On Availability Group, replace `computer\instance` with the availability group listener name in the format of `<AvalabilityGroupListnerName,portNumber>`.  
    n. Right-click `dbo. MT_Microsoft$SystemCenter$DataWarehouse_Log$`, and then click **Edit Top 200 Rows**.  
    o. In the results pane, scroll to the right to the column titled  `Post_MainDatabaseServerName_<GUID>`.  
    p. In the first row, enter `computer\<instance>` followed by a comma, and then the SQL Server port number `(computer\instance,portNumber)`.  If you are hosting the database on a SQL Server cluster, replace *computer* with the virtual network name of the cluster.  If the database is part of a SQL Always On Availability Group, replace `computer\instance` with the availability group listener name in the format of `<AvalabilityGroupListnerName,portNumber>`.
    q. Right-click `dbo.MT_Microsoft$SystemCenter$OpsMgrDWWatcher`, and then click **Edit Top 200 Rows**.  
    r. In the results pane, scroll to the right to the column titled  `MainDatabaseServerName_<GUID>`.  
    s. In the first row, enter `computer\<instance>` followed by a comma, and then the SQL Server port number `(computer\instance,portNumber)`.  If you are hosting the database on a SQL Server cluster, replace *computer* with the virtual network name of the cluster.  If the database is part of a SQL Always On Availability Group, replace `computer\instance` with the availability group listener name in the format of `<AvalabilityGroupListnerName,portNumber>`.  
    t. In the Object Explorer pane, expand **Databases**, expand the data warehouse database (for example, OperationsManagerDW), expand **Tables**, right-click `dbo.MemberDatabase`, and then click **Edit Top 200 Rows**.  
    u. In the results pane, scroll to the right to the column titled `column.ServerName`.  
    v. In the first row, enter `computer\<instance>` followed by a comma, and then the SQL Server port number `(computer\instance,portNumber)`.  If you are hosting the database on a SQL Server cluster, replace *computer* with the virtual network name of the cluster.  If the database is part of a SQL Always On Availability Group, replace `computer\instance` with the availability group listener name in the format of `<AvalabilityGroupListnerName,portNumber>`.


### Update Reporting server

Perform the following steps to modify the configuration of Operations Manager Reporting server after you have updated the configuration of the Reporting data warehouse database.  

1. Log on to the computer hosting the management server.
2. On each management server run **regedit** from an elevated **Command Prompt**, then edit:

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Operations Manager\3.0\Reporting`.   Change **DWDBInstance** to `computer\<instance>` followed by a comma, and then the SQL Server port number `(computer\instance,portNumber)`.  If you are hosting the database on a SQL Server cluster, replace *computer* with the virtual network name of the cluster.  If the database is part of a SQL Always On Availability Group, replace `computer\<instance>` with the availability group listener name in the format of `<AvalabilityGroupListnerName,portNumber>`.  

3. Click **OK**.
4. Open a browser and go to the reporting webpage, http://localhost/reports_instancename. If there is no named instance, go to http://localhost/reports.
5. Click **Show Details** and then click **Data Warehouse Main**. Locate **Connection string** and the line that reads `source=<computer>\<instance>;initial`.
6. Change the **Connection string** to contain the new data warehouse server name.  For example, `computer\<instance>` followed by a comma, and then the SQL Server port number `(computer\instance,portNumber)`.  If you are hosting the database on a SQL Server cluster, replace *computer* with the virtual network name of the cluster.  If the database is part of a SQL Always On Availability Group, replace `computer\<instance>` with the availability group listener name in the format of `<AvalabilityGroupListnerName,portNumber>`.
7. Click **Apply**.
8. Change the connection string for **AppMonitoringSource**.
9. Click **Application monitoring**, and then click **.NET monitoring**.
10. Click **AppMonitoringSource**.
11. On the **AppMonitoringSource** page, click **Properties** and change **Connection string** to contain the new data warehouse main data source server name.  For example, `computer\<instance>` followed by a comma, and then the SQL Server port number `(computer\instance,portNumber)`.  If you are hosting the database on a SQL Server cluster, replace *computer* with the virtual network name of the cluster.  If the database is part of a SQL Always On Availability Group, replace `computer\<instance>` with the availability group listener name in the format of `<AvalabilityGroupListnerName,portNumber>`.  
12. Click **Apply**.
13. Close the browser.

## Next steps


- See [How to move the Operational database](how-to-move-the-operational-database.md) to understand the sequence and steps for moving the Operations Manager operational database to a new SQL Server instance.  

- See [How to move the Reporting data warehouse database](how-to-move-the-reporting-data-warehouse-database.md) to understand the sequence and steps for moving the Operations Manager Reporting data warehouse database to a new SQL Server instance.
