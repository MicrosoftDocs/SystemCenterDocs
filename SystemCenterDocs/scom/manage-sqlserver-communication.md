---
ms.assetid: 61bb5a83-479f-4cc1-b67a-9cd02fc91d2f
title: Configure Operations Manager to communicate with SQL server
description: This article describes how to reconfigure Operations Manager if you change the SQL Server configuration or SQL Server instance hosting its databases.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.update-cycle: 365-days
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: how-to
---

# Configure Operations Manager to communicate with SQL Server

If after installing System Center Operations Manager, you move the Operations Manager operational or data warehouse database to a different SQL Server instance, move the databases to a SQL Server Always On availability group, or reconfigure the SQL Server instance, you need to follow the steps below to reconfigure the management group to reference the new TCP/IP Port, instance name, or computer name.  

**SQL Instance Naming**

For all of the steps below where a SQL instance network name is referenced, use the format `computername\instancename` followed by a comma, and then the SQL Server port number (`computername\instancename,portNumber`). If you're hosting the database on a SQL Server cluster, replace *computername* with the virtual network name of the SQL cluster resource group. If the database is part of a SQL Always On Availability Group, replace `computername\instancename` with the availability group listener name in the format of `AvalabilityGroupListenerName,portNumber`.

## Configure settings for the operational database

1. On each management server run **regedit** from an elevated **Command Prompt**, then edit:

   - `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\System Center\2010\Common\Database`
   Change **DatabaseServerName** with your operational database SQL instance network name.

   - `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Operations Manager\3.0\Setup`
   Change **DatabaseServerName** with your operational database SQL instance network name.  

2. On each management server, edit the following file: `%ProgramFiles%\System Center 2016\Operations Manager\Server\ConfigService.config` for System Center 2016 - Operations Manager, or for all later releases (2019, and 2022), `%ProgramFiles%\Microsoft System Center\Operations Manager\Server\ConfigService.config`:

   - Under the tag `<Category Name=”Cmdb”>`, change the value for *ServerName* to your operational database SQL instance network name and change the value for *PortNumber* to the SQL Server port number.

   - Under the tag ` <Name=”ConfigStore”>`, change the value for *ServerName* to your operational database SQL instance network name and change the value for *PortNumber* to the SQL Server port number.

3. On the SQL Server instance hosting the operational database, configure the following:

    a. Open SQL Server Management Studio.  

    b. In the Object Explorer pane, expand **Databases**, expand the operational database (for example, OperationsManager), expand **Tables**, right-click `dbo.MT_Microsoft$SystemCenter$ManagementGroup`, and select **Edit Top 200 Rows**. In the results pane, scroll to the right to the column titled `column.SQLServerName_<GUID>`.  

    c. In the first row, enter your operational database SQL instance network name.

    d. Right-click `dbo.MT_Microsoft$SystemCenter$OpsMgrDB$AppMonitoring ` and select **Edit Top 200 Rows**. In the results pane, scroll to the right to the column titled  `MainDatabaseServerName_<GUID>`.  

    e. In the first row, enter your operational database SQL instance network name.

    f. Right-click `dbo.MT_Microsoft$SystemCenter$OpsMgrDB$AppMonitoring_Log` and select **Edit Top 200 Rows**. In the results pane, scroll to the right to the column titled `Post_MainDatabaseServerName_<GUID>`.

    g. In the first row, enter your operational database SQL instance network name.

## Configure settings for the data warehouse database

1. On each management server, run **regedit** from an elevated **Command Prompt**, and then edit:

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Operations Manager\3.0\Setup`  
    Change **DataWarehouseDBServerName** to your data warehouse database SQL instance network name.

2. Open SQL Server Management Studio, connect to the SQL Server instance hosting the operational database.  

3. In the Object Explorer pane, expand **Databases**, expand the operational database (for example, OperationsManager), expand **Tables**, right-click `dbo.MT_Microsoft$SystemCenter$DataWarehouse`, and select **Edit Top 200 Rows**.  

4. In the results pane, scroll to the right to the column titled  `MainDatabaseServerName_<GUID>`.

5. In the first row, enter your data warehouse database SQL instance network name.

6. Right-click `dbo.MT_Microsoft$SystemCenter$DataWarehouse$AppMonitoring`, and select **Edit Top 200 Rows**.

7. In the results pane, scroll to the right to the column titled  `MainDatabaseServerName_<GUID>`.

8. In the first row, enter your data warehouse database SQL instance network name.  

9. Right-click `dbo.MT_Microsoft$SystemCenter$DataWarehouse$AppMonitoring_Log`, and select **Edit Top 200 Rows**.

10. In the results pane, scroll to the right to the column titled  `Post_MainDatabaseServerName_<GUID>`.

11. In the first row, enter your data warehouse database SQL instance network name.

12. Right-click `dbo.MT_Microsoft$SystemCenter$DataWarehouse_Log`, and select **Edit Top 200 Rows**.  

13. In the results pane, scroll to the right to the column titled  `Post_MainDatabaseServerName_<GUID>`.  

14. In the first row, enter your data warehouse database SQL instance network name.

15. Right-click `dbo.MT_Microsoft$SystemCenter$OpsMgrDWWatcher`, and select **Edit Top 200 Rows**.  

16. In the results pane, scroll to the right to the column titled  `DatabaseServerName_<GUID>`.  

17. In the first row, enter your data warehouse database SQL instance network name.

18. Right-click `dbo.MT_Microsoft$SystemCenter$OpsMgrDWWatcher_Log`, and select **Edit Top 200 Rows**.

19. In the results pane, scroll to the right to the column titled `Post_DatabaseServerName_<GUID>`.

20. In the first row, enter your data warehouse database SQL instance network name.

21. In the Object Explorer pane, expand **Databases**, expand the data warehouse database (for example, OperationsManagerDW), expand **Tables**, right-click `dbo.MemberDatabase`, and select **Edit Top 200 Rows**.  

22. In the results pane, scroll to the right to the column titled `column.ServerName`.  

23. In the first row, enter your data warehouse database SQL instance network name.

24. On the SQL Server instance hosting the operational database, configure the following:

    a. Open SQL Server Management Studio.

    b. In the Object Explorer pane, expand **Databases**, and select the operational database (for example, OperationsManager).

    c. Select **New Query** on the menu, run the following query to find the GUIDs corresponding to the property name called **MainDatabaseServerName**, and note the results (the query should return 2 records):
      ```SQL
      select * from [dbo].[ManagedTypeProperty]

      where [ManagedTypePropertyName] like 'MainDatabaseServerName'
      ```

    d. Expand the operational database (for example, OperationsManager), expand **Tables**, right-click `dbo.GlobalSettings`, and select **Edit Top 200 Rows**.

    e. In the results pane, scroll to the right of the column titled `column.ManagedTypePropertyId`.

    f. Find the row with a GUID that corresponds to one of those GUIDs returned by the query above (normally row number 8), and enter your data warehouse database SQL instance network name.

### Update Reporting server

Perform the following steps to modify the configuration of Operations Manager reporting server component after you've updated the configuration of the Reporting data warehouse database.  

1. Sign in to the computer hosting the Operations Manager Reporting server.

2. Run **regedit** from an elevated **Command Prompt**, then edit:

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Operations Manager\3.0\Reporting`.   Change **DWDBInstance** to `computer\<instance>` followed by a comma, and then the SQL Server port number `(computer\instance,portNumber)`. If you're hosting the data warehouse database on a SQL Server cluster, replace *computer* with the virtual network name of the cluster. If the database is part of a SQL Always On Availability Group, replace `computer\<instance>` with the availability group listener name in the format of `<AvalabilityGroupListenerName,portNumber>`.  

3. Select **OK**.

4. Open a browser and go to the reporting webpage, `http://localhost/reports_instancename`. If there's no named instance, go to `http://localhost/reports`.

5. Select **Show Details**, and select **Data Warehouse Main**. Locate **Connection string** and the line that reads `source=<computer>\<instance>;initial`.

6. Change the **Connection string** to contain your data warehouse database SQL instance network name.

    - Example Connection string:<br>
      `data source=YourSQLServer.contoso.com;initial catalog=OperationsManagerDW;Integrated Security=SSPI`
    - Example Connection string:<br>
      `data source=SQL1.contoso.com\SQLINST1,1234;initial catalog=OperationsManagerDW;Integrated Security=SSPI`

7. Select **Apply**.

8. To change the connection string for **AppMonitoringSource**, select **Application monitoring**, and select **.NET monitoring**.

9. Select **AppMonitoringSource**.

10. On the **AppMonitoringSource** page, select **Properties**, and change **Connection string** to contain your data warehouse database SQL instance network name.

11. Select **Apply**.

12. Close the browser.

## Next steps

- To understand the sequence and steps for moving the Operations Manager operational database to a new SQL Server instance, see [How to move the Operational database](manage-move-opsdb.md).  

- To understand the sequence and steps for moving the Operations Manager Reporting data warehouse database to a new SQL Server instance, see [How to move the Reporting data warehouse database](manage-move-omdwdb.md).
