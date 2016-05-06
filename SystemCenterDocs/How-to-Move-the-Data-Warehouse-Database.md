---
title: How to Move the Data Warehouse Database
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 038b11bb-2e70-413b-a51c-1e60c380b978
---
# How to Move the Data Warehouse Database
After the initial deployment of [!INCLUDE[om12long](Token/om12long_md.md)], you might need to move the data warehouse database from one Microsoft SQL Server\-based computer to another.

> [!CAUTION]
> This procedure can result in data loss if it is not performed correctly and within a reasonable length of time of the failure. Ensure that you follow all steps precisely, without unnecessary delays between the steps.

This procedure requires Microsoft SQL Server configuration. You need to back up a database, restore a database, update a database table, add new Logins, and modify User Mapping settings for Logins. For more information, see [SQL Server documentation](http://go.microsoft.com/fwlink/p/?linkID=162007).

## Data Warehouse Database Relocation Procedure
Use the procedure below to move the data warehouse database to a different system.

#### To move the data warehouse database

1.  Stop the Operations Manager services \(System Center Data Access Service, System Center Management Service, and System Center Management Configuration Service\) on all management servers in the management group.

2.  On the current Data Warehouse server, use SQL Server Management Studio to create a full backup of the data warehouse database. The default name is OperationsManagerDW. We recommend that you also back up the associated master database.

    For more information, see [How to: Back Up a Database \(SQL Server Management Studio\)](http://go.microsoft.com/fwlink/p/?linkID=206259).

3.  On the new SQL Server, copy the backup file to a local drive or map a local drive to the folder that contains the backup file.

4.  Optionally, on the current Data Warehouse server, delete the data warehouse database.

5.  On the new Data Warehouse server, use SQL Management Studio to restore the OperationsManagerDW database that you previously backed up.

    For more information, see [How to: Restore a Database Backup \(SQL Server Management Studio\)](http://go.microsoft.com/fwlink/p/?linkID=245795).

6.  Update the registry on each management server in the management group to refer to the new SQL Server\-based computer.

    1.  Log on to the management server with Administrator permissions.

    2.  Click **Start**, select **Run**, type regedit in the **Open** box, and then click **OK** to start Registry Editor.

    3.  HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\Microsoft Operations Manager\\3.0\\Setup\\DataWarehouseDBServerName \- \(change this to the new SQL server hosting the DW\).

    4.  Go to the Reporting server.

    5.  HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\System Center Operations Manager\\3.0\\Reporting,\\ DWDBInstance double\-click the name and change the value to the hostname of the SQL Server\-based computer now hosting the operations manager DW database, and then click **OK** to save your change.

    6.  Close the Registry Editor.

7.  Start the System Center Data Access Service on the management server associated with the reporting server. This is needed to access the reports page.

8.  On reporting server, change the connection strings.

    1.  Open a browser and go to the reporting webpage, http:\/\/localhost\/reports\_instancename. If there is no named instance, go to http:\/\/localhost\/reports.

    2.  Click **Show Details** and then click **Data Warehouse Main**. Change the Connection String to contain the new data warehouse server name, and then click **Apply**.

    3.  Change the connection string for AppMonitoringSource.

    4.  Click **Application** monitoring, and then click **.NET monitoring**.

    5.  Click **AppMonitoringSource**.

    6.  On the **AppMonitoringSource** page, click **Properties** and change Connection string to contain the new data warehouse main data source server name, and then click **Apply**.

    7.  Close the browser.

9. On the server hosting the operational database, update the OperationsManager database table.

    1.  Open SQL Server Management Studio.

    2.  Expand **Databases**, **OperationsManager**, and **Tables**.

    3.  Right\-click **dbo.MT\_Microsoft$SystemCenter$DataWarehouse**, and then click **Edit Top 200 Rows**.

    4.  Change the value in the **MainDatabaseServerName\_2C77AA48\_DB0A\_5D69\_F8FF\_20E48F3AED0F** column to reflect the name of the new SQL Server for the DW database.

    5.  Update the OperationsManager database for Application Performance Monitoring functionality.

    6.  Right\-click **dbo.MT\_Microsoft$SystemCenter$DataWarehouse$AppMonitoring**, and then click **Edit Top 200 Rows**.

    7.  Change the value in the **MainDatabaseServerName\_5C00C79B\_6B71\_6EEE\_4ADE\_80C11F84527A** column to reflect the name of the new SQL Server for the DW database.

    8.  Do the same for the following tables.

    9. Right\-click **dbo. MT\_Microsoft$SystemCenter$DataWarehouse$AppMonitoring\_Log** and then click **Edit Top 200 Rows**. Change the value of column **Post\_MainDatabaseServerName\_5C00C79B\_6B71\_6EEE\_4ADE\_80C11F84527A** to reflect the name of the new SQL Server for the DW database.

    10. Right\-click **dbo.MT\_Microsoft$SystemCenter$DataWarehouse\_Log** and then click **Edit Top 200 Rows**. Change the value of **column.Pre\_MainDatabaseServerName\_2C77AA48\_DB0A\_5D69\_F8FF\_20E48F3AED0F**.

    11. Close SQL Server Management Studio.

10. On the new data warehouse server, update the member database.

    1.  Open SQL Server Management Studio.

    2.  Expand **Databases**, **OperationsManagerDW**, and **Tables**.

    3.  Right\-click **dbo.MemberDatabase**, and then click **Edit Top 200 Rows**.

    4.  Change the value in the **ServerName** column to reflect the name of the new SQL Server.

    5.  Close SQL Server Management Studio.

11. On the new server hosting the operational database, expand **Security**, then expand **Logins**, and then add the data writer account.

    For more information, see [How to: Create a SQL Server Login](http://go.microsoft.com/fwlink/p/?linkID=245796).

12. Also in **Logins**, add the data reader account.

13. Also in **Logins**, add the Data Access Service computer account, using the form “domain\\computername$”.

14. For the Data Access Service \(DAS\) computer account, add the following user mappings:

    -   db\_datareader

    -   OpsMgrReader

    -   apm\_datareader

    > [!NOTE]
    > If an account has not existed before in the SQL instance in which you are adding it, the mapping will be picked up by SID automatically from the restored data warehouse database. If the account has existed in that SQL instance before, you receive an error indicating failure for that login, although the account appears in **Logins**. If you are creating a new login, ensure the User Mapping for that login and database are set to the same values as the previous login:
    > 
    > DW Data Writer: db\_owner, OpsMgrWriter, apm\_datareader, apm\_datawriter
    > 
    > DW Data Reader: db\_datareader, OpsMgrReader, apm\_datareader
    > 
    > DAS\/Config account: db\_datareader, OpsMgrReader, apm\_datareader
    > 
    > If DAS\/Config uses the LocalSystem account, specify computer account in form “<domain>\\<computername>$”.

15. Start the Operations Manager services \(System Center Management, System Center Data Access, and System Center Management Configuration\) on all the management servers in the management group.

#### To verify a successful move of the data warehouse database

1.  Verify that you can successfully run a report from the console.

2.  Ensure that the health state of all management servers in the management group are **Healthy**.

    If the health state of any management server is **Critical**, open **Health Explorer**, expand **Availability \- <***server name***>**, and then continue to expand until you can navigate to **Data Warehouse SQL RS Deployed Management Pack List Request State**. Check the associated events to determine if there is an issue accessing the data warehouse database.

3.  Check operating system events:

    1.  Open the operating system's Event viewer. Navigate to **Event Viewer**, and then to **Operations Manager**.

    2.  In the **Operations Manager** pane, search for events with a **Source** of **Health Service Module** and a **Category** of **Data Warehouse**.

        The move was successful if event number 31570, 31558, or 31554 exists.

        There is an issue accessing the data warehouse database if event numbers 31563, 31551, 31569, or 31552 exists.

4.  Check events in Operations Manager:

    1.  In the Operations console, select **Monitoring**.

    2.  Navigate to **Monitoring**, **Operations Manager**, **Health Service Module Events**, and then to **Performance Data Source Module Events**.

    3.  Search the **Performance Data Source Module Events**  pane for events with a **Date and Time** that is later than the move.

        There is a problem with the data warehouse database if events have a **Source** of **Health Service Module** and an **Event Number** of 10103.


