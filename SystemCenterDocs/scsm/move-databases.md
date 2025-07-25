---
title: Move the Service Manager and data warehouse databases
description: This article helps you move the Service Manager and data warehouse databases to different servers after you have deployed Service Manager.
ms.custom: na, UpdateFrequency3, engagement-fy23, engagement-fy24
ms.service: system-center
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.reviewer: na
ms.suite: na
ms.subservice: service-manager
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: 8b6c406a-7cb3-4be7-902b-5a09be71ad98
---

# Move the Service Manager and data warehouse databases to different servers


After you've deployed Service Manager, you might need to move the Service Manager or data warehouse databases from one computer running Microsoft SQL Server to another for reasons such as the following:

- You need to replace hardware that is experiencing issues and is no longer considered reliable.  

- You need to add additional hardware to improve scalability and performance.  

- You need to move a database and log file to a different volume because of space or performance reasons.  

- You need to change hardware that is leased and is due to expire soon.  

- You need to change or upgrade hardware to comply with new hardware standards.  

- You initially installed multiple Service Manager components on a single server, and you need to distribute some components to other servers.  

- You need to restore functionality in a failure scenario.  

If you want the move the data warehouse database, and if you've installed Service Manager within the last 90 days, it might be easier for you to unregister the data warehouse, install a new data warehouse, and register the new database. If the data hasn't been groomed from the Service Manager database, there will be no data loss in the data warehouse database because it will be synchronized. By default, the grooming interval for work items is 90 days from the last time a work item was modified. Using this process is simpler than using the following guidance, which details how to move your databases from one server to another and requires many steps.  

## Move the Service Manager database

You must use the following high-level steps to move the Service Manager database.  

> [!NOTE]  
> - These steps link to content in the Service Manager Upgrade Guide.
> - After deploying Service Manager on the SQL server nodes participating in SQL Always On, to enable [CLR strict security](/sql/database-engine/configure-windows/clr-strict-security?preserve-view=true&view=sql-server-2017), run the [SQL script](system-requirements.md#enable-clr-strict-security) on each Service Manager database.

1. Open the inbound SQL Port on new Service Manager database server. The default port is 1433.  

2. Stop the System Center services on all the management servers.  

3. Back up the Service Manager database, as described in [How to Back Up the Production Service Manager Database](prod-env.md#back-up-the-production-service-manager-database-for-future-recovery).  

4. Restore the Service Manager database on the target computer that is running Microsoft SQL Server, as described in [How to Restore the Service Manager Database in the Lab Environment](lab-env.md#restore-the-service-manager-database-in-the-lab-environment).  

5. Configure the Service Manager database, as described in [How to Prepare the Service Manager Database in the Lab Environment](lab-env.md#prepare-the-service-manager-database-in-the-lab-environment).  

    > [!IMPORTANT]  
    > Don't perform step 17 in the procedure for configuring tables.  

6. After you move the ServiceManager database, ensure that you manually change all the Service Manager database and data warehouse registration information in the DWStagingAndConfig database. Old information about where the ServiceManager database is located remains in the DWStagingAndConfig database in the following tables:  

    - MT\_Microsoft$Systemcenter$Datawarehouse$CMDBSource  

        - In the corresponding entry with DataSourceName\_GUID \= \<Service Manager Data Source Name\>, change the field DatabaseServer\_GUID with the new name of the SQLServer\\Instance where the ServiceManager database has moved to.  

    - MT\_Microsoft$Systemcenter$ResourceAccessLayer$SqlResourceStore  

        - In the corresponding entry with DataService\_GUID \= ServiceManager, change the field Server\_GUID to the new name of the SQLServer\\Instance where the ServiceManager database has moved to.  

7. Configure the registry on all the management servers that will access the new SQL Server instance by using the following steps:  

    1. Open Registry Editor.  

    2. Browse to **HKEY\_LOCAL\_MACHINE\\Software\\Microsoft\\System Center\\\<version\>\\Common\\Database**.  

    3. Configure two keys: one for the server name \(DatabaseServerName\) and one for the database name \(DatabaseName\). Set values to the new server name and database name if they're different from the original values.  

8. If you're also upgrading the SQL server while moving, then upgrade the following SQL Server prerequisites for the Service Manager Management server. There are 2 SQL Server prerequisites:  

    - SQL Native Client  

    - Analysis Management Objects (AMO)  

9. Start the System Center services on all the management servers, as described in [How to Start Service Manager Services on the Secondary Management Server](lab-env.md#start-service-manager-services-on-the-secondary-management-server).  

10. Install another Service Manager database that has a different name on the same computer that is running SQL Server by installing another Service Manager management server and choosing to create a new database. This step will populate the master database with error message text so that if an error occurs in the future, the error message can describe the specific problem instead of displaying generic text. After the database is installed, you can drop it from the computer that is running SQL Server and uninstall the additional, temporary management server.  

     \-Or\-  

     Run the following query on the source Service Manager database server and copy the output script, and then run it on new Service Manager database server.  

    ```  
    DECLARE @crlf char(2);  
    DECLARE @tab char(1);  
    SET @crlf = CHAR(13) + CHAR(10);  
    SET @tab = CHAR(9);  

    SELECT   
           'EXEC sp_addmessage ' + @crlf + @tab  
            + '@msgnum = ' + CAST(m.message_id AS varchar(30))  
                  + ', ' + @crlf + @tab  
          + '@severity = ' + CAST(m.severity AS varchar(3))    
                  + ', ' + @crlf + @tab  
          + '@msgtext = N''' + REPLACE(m.[text],'''','''''')    
                  + ''''  + ', ' + @crlf + @tab  
            + '@lang = ''' +   
                  (SELECT TOP 1 alias   
                   FROM master.sys.syslanguages l   
                   WHERE l.lcid = m.language_id)   
                   + ''', ' + @crlf + @tab  
          + '@with_log = ''' +   
                  CASE WHEN m.is_event_logged = 1   
                   THEN 'TRUE' ELSE 'FALSE' END   + ''', ' +  @crlf + @tab  
                  -- Uncomment ONLY if you want to replace:  
            + '@replace = ''replace'';'   
            + @crlf + 'GO' + @crlf + @crlf   
    FROM   
            master.sys.messages m  
    WHERE   
           m.message_id > 50000;  

    GO  
    ```  

## Move data warehouse databases

The following high-level steps are required to move the data warehouse databases. Each step in this list links to an associated procedure later in this article.  

1. Locate user accounts and instances of SQL Server
2. Stop Service Manager services
3. Back up the data warehouse databases
4. Take the data warehouse databases offline
5. Restore the data warehouse databases on the new computer running SQL Server
6. Prepare the data warehouse databases on the new database server
7. Update data warehouse management Server with the new database server name
8. Update the data sources on the reporting server
9. Update the data sources for the Analysis Services
10. Start Service Manager Services on the data warehouse management server

> [!IMPORTANT]  
> After you move the **DWStagingAndConfig** and **DWRepository** databases, they have to be restored on the same instance of SQL Server. Restoring them on separate instances of SQL Server isn't supported.  
>
> The collation on the new instance of SQL Server has to match the collation of the original instances of SQL Server where the data warehouse databases were originally hosted.  

### Locate user accounts and instances of SQL Server

 Use the following procedures to locate the user accounts and instances of SQL Server that are used by the data warehouse management server to identify the:

# [SQL Server database and instance names](#tab/SQLServerDB)

Follow these steps to identify the SQL Server database and instance names used by the data warehouse management server:

1. Sign in to the data warehouse management server as a user with administrative credentials.  

2. On the Windows desktop, select **Start**, and select **Run**.  

3. In the **Run** dialog, in the **Open** box, enter **regedit**, and select **OK**.  

4. In the Registry Editor window, expand **HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\System Center\\\<version\>\\Common\\Database**, and then make note of the following registry values:  

    - DatabaseName  

    - DatabaseServerName  

    - DataMartDatabaseName  

    - DataMartSQLInstance  

    - RepositoryDatabaseName  

    - RepositorySQLInstance  

    - StagingDatabaseName  

    - StagingSQLInstance  

    - OMDataMartDatabaseName  

    - OMDataMartSQLInstance  

    - CMDataMartDatabaseName  

    - CMDataMartSQLInstance  

# [Reporting server and instance names](#tab/ReportingServer)

Follow these steps to identify the reporting server and instance names used by data warehouse management server:

1. Sign in to the data warehouse management server as a user with administrative credentials.  
2. On the Windows desktop, select **Start**, and select **Run**.  
3. In the **Run** dialog, in the **Open** box, enter **regedit**, and select **OK**.  
4. In the Registry Editor window, expand **HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\System Center\\\<version\>\\Common\\Reporting**, and then make note of the following registry values:  

    - Server  
    - ServerInstance  
    - WebServiceURL  

# [Service account](#tab/ServiceAccount)

Follow these steps to identify the service account used by the data warehouse management server:

1. On the Windows desktop, select **Start**, and select **Run**.  

2. In the **Run** dialog, in the **Open** box, enter **services.msc**, and select **OK**.  

3. Locate the service System Center Data Access Service, and double\-click it.  

4. In the **Properties** window, select the **Log On** tab.  

5. Make a note of the user account name under **This account:**.  

6. Repeat Steps 3 through 5 for the **System Center Management Configuration** service.  

# [Reporting account](#tab/ReportingAccount)

Follow these steps to identify the reporting account used by the data warehouse management server:

1. > [!NOTE]  
    > The account that is configured by using the names in the following data sources in SQL Server Reporting Services is called the **Reporting account**.  

     Sign in to the server with SQL Server Reporting Services that are hosting the Service Manager reports.  

    > [!NOTE]  
    > In this procedure, you'll use values that you noted in the **To identify the SQL Server database and instance names used by the data warehouse management server** procedure.  

2. In SQL Server Reporting Services, select **Start**, select **All Programs**, select the program group for the version of SQL Server you're running, select **Configuration Tools**, and select **Reporting Services Configuration Manager**.  

3. In the **Reporting Services Configuration Connection** dialog, connect to the **SQL Reporting instance** that you noted in a previous procedure.  

4. In **Reporting Services Configuration Manager**, select **Reporting Manager URL**.  

5. On the **Reporting Manager URL** page, select the hyperlink that resembles `http://Servername:portnumber/Reports` to open it in your web browser.  

6. Open the **System Center** folder and then open the **Service Manager** folder.  

7. Select the **DWDataMart** data source and make a note of the **User name** value under **Credentials stored securely in the report server**.  

8. In your browser, select **Back** to return to the **Service Manager** folder.  

9. Select the **DWStagingAndConfig** data source and make a note of the **User name** value under **Credentials stored securely in the report server**.  

10. In your browser, select **Back** to return to the **Service Manager** folder.  

11. Select the **ConfigurationManager** data source and make a note of the **User name** value under **Credentials stored securely in the report server**.  

12. In your browser, select **Back** to return to the **Service Manager** folder.  

13. Select the **MultiMartDatasource** data source and make a note of the **User name** value under **Credentials stored securely in the report server**.  

14. In your browser, select **Back** to return to the **Service Manager** folder.  

15. Select the **OperationsManager** data source and make a note of the **User name** value under **Credentials stored securely in the report server**.  

16. Close the browser window.  

# [OLAP Account](#tab/OLAPAccount)

Follow these steps to identify the OLAP Account used by the data warehouse management server:

1. Sign in to the Service Manager server, select **Start**, select **All Programs**, select **Microsoft System Center \<version\>**, select **Service Manager**, and select **Service Manager Shell**.  

2. In the Windows PowerShell command prompt, copy the following command, and then press ENTER.  

   > [!NOTE]  
   > Replace \<DWServerName\> with the name of your data warehouse management server.  

   ```  
   $class= get-scclass -Name Microsoft.SystemCenter.ResourceAccessLayer.ASResourceStore -ComputerName <DWServerName>  
   $OLAPServer= get-scclassinstance -class $class -ComputerName <DWServerName>  
   $OLAPServer.Server  
   ```  

   > [!NOTE]  
   > The $OLAPServer.Server cmdlet  returns the name of the OLAP server that is hosting the DWASDataBase, and it contains the OLAP Account.  

3. On a server where you have **SQL Server Management Studio** installed, do the following:  

   1. Open SQL Server Management Studio.  

   2. In the **Connect to Server** window, select **Analysis Services** in the **Server type** list.  

   3. In the **Server name** list, enter or select the name you noted from the output of the $OLAPServer.Server cmdlet in previous step, and select **Connect**.  

   4. In the **Object Explorer** pane, expand **Databases**, and then expand the **DWASDataBase** OLAP database.  

   5. Expand the **Data Sources** folder, and then double\-click **CMDataMart**.  

   6. In the **Data Source Properties - CMDataMart** dialog, note the value of **Connection String**.  

   7. Under **Security Settings**, select **Impersonation Account**, and select the properties button (...) to open the **Impersonation Information** dialog.  

   8. In the **Impersonation Information** dialog, note the user name.  

   9. Select **Cancel** twice to close the dialogs.  

   10. Repeat the steps above to note the Connection string and the User name for the DWDataMart and OMDataMart databases.
---

### Stop Service Manager services

 Use the following procedure to stop the Service Manager services on the data warehouse management server.

#### Stop Service Manager services on the data warehouse management server  

Follow these steps to stop Service Manager services on the data warehouse management server:

1. In the **Run** dialog, in the **Open** text field, enter **services.msc**, and select **OK**.  

2. In the **Services** window, in the **Services \(Local\)** pane, locate the following three services, and for each one, select **Stop**:  

    1. System Center Data Access Service  

    2. Microsoft Monitoring Agent  

    3. System Center Management Configuration  

### Back up the data warehouse databases  

 Use the following procedure to back up the data warehouse databases on the original computer running SQL Server:

1. Sign in to the original computer running SQL Server that is hosting the data warehouse databases, and open **SQL Server Management Studio**.  

2. In the **Connect to Server** dialog, follow these steps:  

    1. In the **Server Type** list, select **Database Engine**.  

    2. In the **Server Name** list, select the server name for your data warehouse database.  

    3. In the **Authentication** list, select **Windows Authentication**, and select **Connect**.  

3. In the **Object Explorer** pane, expand **Databases**.  

4. Right-click the **DWStagingAndConfig** database, select **Tasks**, and select **Back Up**.  

5. In the **Back Up Database** dialog, enter a path and a file name in the **Destination on disk** text box, and select **OK**.  

    > [!IMPORTANT]  
    > The destination location must have enough available free disk space to store the backup files.  

6. Select **OK** in the **Back Up Database** dialog to start the backup.  

7. Repeat these steps for the DWRepository, CMDWDataMart, OMDWDataMart, and DWDataMart databases.  

### Take the data warehouse databases offline  

 Use the following procedure to take the data warehouse databases offline on the original computer running SQL Server:

1. Sign in to the original computer running SQL Server that is hosting the data warehouse databases, and open **SQL Server Management Studio**.  

2. In the **Connect to Server** dialog, follow these steps:  

    1. In the **Server Type** list, select **Database Engine**.  

    2. In the **Server Name** list, select the server name for your data warehouse database.  

    3. In the **Authentication** list, select **Windows Authentication**, and select **Connect**.  

3. In the **Object Explorer** pane, expand **Databases**.  

4. Right-click the **DWStagingAndConfig** database, select **Tasks**, and select **Take Offline**.  

5. In the **Take database offline** dialog, select **Close**.  

6. Repeat the previous steps for the DWRepository, CMDWDataMart, OMDWDataMart, and DWDataMart databases.  

### Restore the data warehouse databases on the new computer running SQL Server  

 Use the following procedure to restore the data warehouse databases on the new computer running SQL Server:

1. On the new computer running SQL Server, open **SQL Server Management Studio**.  

2. In the **Connect to Server** dialog, follow these steps:  

    1. In the **Server Type** list, select **Database Engine**.  

    2. In the **Server Name** list, select the server name for your Service Manager services database.  

    3. In the **Authentication** list, select **Windows Authentication**, and select **Connect**.  

3. In the **Object Explorer** pane, right-click the **Databases** folder, and select **Restore Database**.  

4. In the **Restore Database** dialog, under the **To a point in time** text box, retain the default, **Most recent possible**, or select a specific date and time by selecting the browse button to open the **Point in Time Restore** dialog.  

5. To specify the source and location of the backup sets to restore, select **From Device**.  

6. Select **Browse** to open the **Specify Backup** dialog.  

7. In the **Backup media** list box, select one of the listed device types. To select more devices for the Backup location, select **Add**.  

8. In the **Select the backup sets to restore** grid, select the backups to restore. \(This grid displays the backups that are available for the specified location.\)  

9. On the **General** page, the name of the restoring database appears in the **To database** list. Select the **DWStagingAndConfig** database from the list.  

10. In the **Restore options** panel, select **Overwrite the existing database**.  

11. In the **Restore the database files as** options panel, verify that the original database file name and path are correct.  

12. For the **Recovery state** option, select **Leave the databases ready to use by rolling back the uncommitted transactions. Additional transaction logs cannot be restored \(RESTORE WITH RECOVERY\)**.  

13. Select **OK** to restore the database.  

14. Repeat the previous steps for the DWRepository, CMDWDataMart, OMDWDataMart, and DWDataMart databases.  

### Prepare the data warehouse databases on the new database server  

 Use the following three procedures to prepare the data warehouse databases on the new database server:  

1. To configure the DWStagingAndConfig database on the new computer running SQL Server  

2. To configure the service account database permissions  

3. To configure the DWStagingAndConfig tables  

#### Configure the DWStagingAndConfig database on the new computer running SQL Server  

Follow these steps to configure the DWStagingAndConfig database on the new computer running SQL Server:

1. On the new computer running SQL Server, open **SQL Server Management Studio**.  

2. In the **Connect to Server** dialog, follow these steps:  

    1. In the **Server Type** list, select **Database Engine**.  

    2. In the **Server Name** list, select the name of the new computer running SQL Server that hosts the **DWStagingAndConfig** database.  

    3. In the **Authentication** list, select **Windows Authentication**, and select **Connect**.  

3. In the **Object Explorer** pane, expand **Databases**, and select **DWStagingAndConfig**.  

4. In the toolbar, select **New Query**.  

5. In the center pane, copy the following command, and select **Execute**.  

    ```  
    sp_configure&nbsp;'clr enabled',&nbsp;1  
    go  
    reconfigure  
    go  
    ```  

6. In the center pane, remove the command you typed in the previous step, copy the following command, and select **Execute**.  

    ```  
    ALTER DATABASE DWStagingAndConfig SET SINGLE_USER WITH ROLLBACK IMMEDIATE  
    ```  

7. In the center pane, remove the command you entered in the previous step, copy the following command, and select **Execute**.  

    ```  
    ALTER DATABASE DWStagingAndConfig SET ENABLE_BROKER  
    ```  

8. In the center pane, remove the command you entered in the previous step, enter the following command, and select **Execute**.  

    ```  
    ALTER DATABASE DWStagingAndConfig SET MULTI_USER  
    ```  

#### Configure the service account database permissions  

Follow these steps to configure the service account database permissions:

1. In the **Object Explorer** pane, expand **Security**, and then expand **Logins**. Right-click **Logins**, and select **New Login**.  

2. Select **Search**.  

3. Enter the user name by using the domain\\user name format for the data warehouse service account, select **Check Names**, and select **OK**.  

    > [!NOTE]  
    > If the Data Access Account is running as LocalSystem, use the format *domain\computername$* in SQL Logins, where *computername* is the name of the management server.  

4. In the **Select a page** pane, select **User Mapping**.  

5. In the **Users mapped to this login** area, in the **Map** column, select the row that represents the name of the DWStagingAndConfig database. DWStagingAndConfig is the default database name.  

6. In the **Database role membership for: DWStagingAndConfig** area, ensure that the following entries are selected:  

    - **configsvc\_users**  

    - **db\_accessadmin**  

    - **db\_datareader**  

    - **db\_datawriter**  

    - **db\_ddladmin**  

    - **db\_securityadmin**  

    - **dbmodule\_users**  

    - **public**  

    - **sdk\_users**  

    - **sql\_dependency\_subscriber**  

    - **db\_owner**  

7. In the **Database role membership for: DWRepository** area, ensure that the following entries are selected:  

    - **db\_owner**  

    - **public**  

8. In the **Database role membership for: DWDataMart** area, ensure that the following entries are selected:  

    - **db\_owner**  

    - **public**  

9. Select **OK**.  

10. In the **Object Explorer** pane, expand **Security**, and then expand **Logins**.  

11. Right-click **Logins**, and then **click New  Login**.  

12. Select **Search**.  

13. Enter the user name in the domain\\user name format for the reporting account, select **Check Names**, and select **OK**.  

14. In the **Select a page** pane, select **User Mapping**.  

15. In the **Users mapped to this login** area, in the **Map** column, select the row that represents the name of the DWStagingAndConfig. DWStagingAndConfig is the default database name.  

16. In **the Database role membership for: DWStagingAndConfig** area, ensure that the following entries are selected:  

    - **db\_datareader**  

    - **public**  

17. In the **Database role membership for: DWRepository** area, ensure that the following entries are selected:  

    - **db\_datareader**  

    - **public**  

    - **reportuser**  

18. In the **Database role membership for: DWDataMart** area, ensure that the following entries are selected:  

    - **db\_datareader**  

    - **public**  

    - **reportuser**  

19. In the **Database role membership for: OMDWDataMart** area, ensure that the following entries are selected:  

    - **db\_datareader**  

    - **public**  

    - **reportuser**  

20. In the **Database role membership for: CMDWDataMart** area, ensure that the following entries are selected:  

    - **db\_datareader**  

    - **public**  

    - **reportuser**  

21. Select **OK**.  

22. In the **Object Explorer** pane, expand **Security**, and then expand **Logins**.  

23. Right-click **Logins**, and select **New  Login**.  

24. Select **Search**.  

25. Enter the user name in the domain\\user name format for the **OLAP account**, select **Check Names**, and select **OK**.  

26. In the **Select a page** pane, select **User Mapping**.  

27. In the **Database role membership for: DWDataMart** area, ensure that the following entries are selected:  

    - **db\_datareader**  

    - **public**  

    - **reportuser**  

28. In the **Database role membership for: OMDWDataMart** area, ensure that the following entries are selected:  

    - **db\_datareader**  

    - **public**  

    - **reportuser**  

29. In the **Database role membership for: CMDWDataMart** area, ensure that the following entries are selected:  

    - **db\_datareader**  

    - **public**  

    - **reportuser**  

30. Select **OK**.  

#### Configure the DWStagingAndConfig tables  

Follow these steps to configure the DWStagingAndConfig tables:

1. In the **Object Explorer** pane, expand **Databases**, expand **DWStagingAndConfig**, and then expand **Tables**.  

2. Select **dbo.MT\_Microsoft$SystemCenter$ManagementGroup**, and select **Edit Top 200 Rows**.  

3. In the center pane, locate the column **SQLServerName\_ 43FB076F\_7970\_4C86\_6DCA\_8BD541F45E3A**, and then in the first row of the column, enter the name of the new computer running SQL Server that is hosting the DWStagingAndConfig database. For named instances, enter **ComputerName\\InstanceName**.  

4. Right-click **dbo. MT\_Microsoft$SystemCenter$ResourceAccessLayer$SqlResourceStore**, and select **Edit Top 200 Rows**.  

5. Update the column **Server\_48B308F9\_CF0E\_0F74\_83E1\_0AEB1B58E2FA** for rows representing DWStagingAndConfig, DWRepository, CMDWDataMart, OMDWDataMart, and DWDataMart by entering the name of the new computer running SQL Server that is hosting the respective databases. For named instances, enter **ComputerName\\InstanceName**.  

6. Right-click **dbo.MT\_Microsoft$SystemCenter$ResourceAccessLayer$CMDBResourceStore**, and select **Edit Top 200 Rows**.  

7. In the center pane, locate the column **Server\_48B308F9\_CF0E\_0F74\_83E1\_0AEB1B58E2FA**, and in the first row of the column, enter the name of the new computer running SQL Server that is hosting the DWStagingAndConfig database. For named instances, enter **ComputerName\\InstanceName**.  

8. Right-click **LFX.DataSource**, and select **Edit Top 200 Rows**.  

9. In the center pane, locate the **DataSourceAddress** column, and in the first row of the column, locate the entry that starts with **Data Source = *server name*; Initial Catalog = DWStagingAndConfig; Persist Security Info=False**. Replace ***server name*** with the name of the new computer running SQL Server.  

10. Ensure that the values you entered were saved by querying the tables specified in the previous steps.  

11. Close **Microsoft SQL Server Management Studio**.  

### Update data warehouse management Server with the new database server name  

 Use the following procedure to update the data warehouse management server to use the new database server name:

1. Sign in to the computer as a user with administrative credentials.  

2. On the Windows desktop, select **Start**, and select **Run**.  

3. In the **Run** dialog, in the **Open** box, enter **regedit**, and select **OK**.  

    > [!CAUTION]  
    > Incorrectly editing the registry might severely damage your system; therefore, before making changes to the registry, back up any valued data on the computer.  

4. In the Registry Editor window, expand **HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\System Center\\\<version\>\Common\\Database**.  

5. In the right pane, double\-click **DatabaseServerName**.  

6. In the **Edit String** box, in the **Value data** box, enter the name of the new computer running SQL Server that hosts the DWStagingAndConfig database. If you're using a named instance of SQL Server, use the Computer Name\\Instance name format.  

7. Select **OK**.  

8. Repeat the previous steps for the registry values to reflect the new name of the computer running SQL Server for the DWDataMart, OMDWDataMart, CMDWDataMart, DWRepository, and DWStagingAndConfig databases.  

    - DataMartSQLInstance  

    - RepositorySQLInstance  

    - StagingSQLInstance  

- OMDataMartSQLInstance  

    - CMDataMartSQLInstance  

### Update the data sources on the reporting server  

 Use the following procedure to update data sources on the reporting server to point to the new computer running SQL Server:

1. Sign in to the Service Manager reporting server, and start **Reporting Services Configuration Manager**.  

2. In the **Reporting Services Configuration Connection** dialog, connect to the correct reporting server instance as noted in the section To identify the reporting server and instance name used by data warehouse management server.  

3. In the Reporting Services Configuration Manager list, select **Report Manager URL**.  

4. On the **Report Manager URL** page, select the hyperlink that resembles `http://Servername/:portnumber/Reports` to open the **Reports** home page in your Internet browser.  

5. On the home page, open the **System Center** folder, and then open the **Service Manager** folder.  

6. Open the list of Service Manager items, and select the **DWDataMart** data source.  

7. In the **Connection string** box, the string resembles `data source=<server name>;initial catalog=DWDataMart`. Replace the existing name of the computer running SQL Server by typing the name of the new computer running SQL Server.  

8. Go back to the previous Service Manager folder webpage, and select the **DWStagingAndConfig** data source.  

9. In the **Connection string** box, the string resembles `data source=<server name>;initial catalog= DWStagingAndConfig`. Replace the existing name of the computer running SQL Server by typing the name of the new computer running SQL Server.  

10. Go back to the previous Service Manager folder webpage and select the **ConfigurationManager** data source.  

11. In the **Connection string** box, the string resembles `data source=<server name>;initial catalog= CMDWDataMart`. Replace the existing name of the computer running SQL Server by entering the name of the new computer running SQL Server.  

12. Go back to the previous Service Manager folder webpage and select the **MultiMartDatasource** data source.  

13. In the **Connection string** box, the string resembles `<root><source id='DWDataMart' connectionString='Data Source=<Server name>;Initial Catalog=DWDataMart;Integrated Security=True' /><source id='OMDataMart' connectionString='Data Source=<Server name>;Initial Catalog=OMDWDataMart;Integrated Security=True' /><source id='CMDataMart' connectionString='Data Source=<Server name>;Initial Catalog=CMDWDataMart;Integrated Security=True' /></root>`. Replace the existing name of the computer running SQL Server by entering the name of the new computer running SQL Server.  

14. Go back to the previous Service Manager folder webpage and select the **Operations Manager** data source.  

15. In the **Connection string** box, the string resembles `data source=<server name>;initial catalog= OMDWDataMart`. Replace the existing name of the computer running SQL Server by typing the name of the new computer running SQL Server.  

16. Close your web browser.  

### Update the data sources for the Analysis Services  

 Use the following procedure to update the connection strings for the data sources on the server that hosts the Analysis Services database:

1. Sign in to the server that hosts the SQL Server Analysis Services database.  

2. Open **SQL Server Management Studio**.  

3. In the **Connect to Server** dialog, in the **Server Type** list, select **Analysis Services**.  

4. In the **Server name** list, enter the server name that you received as output from the $OLAPServer.Server cmdlet. \(You noted this information in the To identify the OLAP Account used by the data warehouse management server section earlier in this topic.\)  

5. In the **Object Explorer** pane, expand **Databases**, and then expand **DWASDataBase**.  

6. Expand **Data Sources**, and then double\-click **CMDataMart**.  

7. In the **Data Source Properties - CMDataMart** dialog, select **Connection string Provider=SQLNCLI10.1;Data Source=servername;Integrated Security=SSPI;Initial Catalog=CMDWDataMart**.  

8. Replace \<servername\> with the name of the computer running SQL Server that hosts the CMDWDataMart database.  

9. You need to re\-enter the impersonation account password when you've completed updating the Data Source server. Select the ellipsis button to the right of **ImpersonateAccount** and then add the password in the **Impersonation Information** dialog. Select **OK** to accept the changes.  

10. Repeat the previous steps to update the connection strings for the DWDataMart and OMDataMart data sources.  

### Start Service Manager Services on the data warehouse management server  

 Use the following procedure to start the Service Manager services on the data warehouse management server:

1. In the **Run** dialog, in the **Open** text field, enter **services.msc**, and select **OK**.  

2. In the **Services** window, in the **Services \(Local\)** pane, locate the following three services, and for each one, select **Start**:  

    1. System Center Data Access Service  

    2. Microsoft Monitoring Agent  

    3. System Center Management Configuration  

## Next steps

To learn about upgrading Service Manager, review [Upgrade System Center 2012 R2 - Service Manager to System Center - Service Manager](./upgrade-service-manager.md).
