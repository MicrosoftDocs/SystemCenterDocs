---
title: Moving Data Warehouse Databases
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 85180b6f-afda-4940-a9f3-3473ad84f30b
translation.priority.ht: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# Moving Data Warehouse Databases
The following high\-level steps are required to move the Data Warehouse databases. Each step in this list links to an associated procedure later in this document.  
  
1.  [Locate user accounts and instances of SQL Server](../../../sm/deploy/deploy-guide/Moving-Data-Warehouse-Databases.md#bkmk_locating)  
  
2.  [Stop Service Manager services](../../../sm/deploy/deploy-guide/Moving-Data-Warehouse-Databases.md#BKMK_stop)  
  
3.  [Back up the data warehouse databases](../../../sm/deploy/deploy-guide/Moving-Data-Warehouse-Databases.md#BKMK_backup)  
  
4.  [Take the data warehouse databases offline](../../../sm/deploy/deploy-guide/Moving-Data-Warehouse-Databases.md#BKMK_offline)  
  
5.  [Restore the data warehouse databases on the new computer running SQL Server](../../../sm/deploy/deploy-guide/Moving-Data-Warehouse-Databases.md#BKMK_restore)  
  
6.  [Prepare the data warehouse databases on the new database server](../../../sm/deploy/deploy-guide/Moving-Data-Warehouse-Databases.md#BKMK_prepareDB)  
  
7.  [Update data warehouse management Server with the new database server name](../../../sm/deploy/deploy-guide/Moving-Data-Warehouse-Databases.md#BKMK_updatename)  
  
8.  [Update the data sources on the reporting server](../../../sm/deploy/deploy-guide/Moving-Data-Warehouse-Databases.md#BKMK_updateDS)  
  
9. [Update the data sources for the Analysis Services](../../../sm/deploy/deploy-guide/Moving-Data-Warehouse-Databases.md#BKMK_updateDSAS)  
  
10. [Start Service Manager Services on the data warehouse management server](../../../sm/deploy/deploy-guide/Moving-Data-Warehouse-Databases.md#BKMK_StartSer)  
  
> [!IMPORTANT]  
>  After you move the **DWStagingAndConfig** and **DWRepository**databases, they have to be restored on the same instance of SQL Server. Restoring them on a separate instances of SQL Server is not supported.  
>   
>  The collation on the new instance of SQL Server has to match the collation of the original instances of SQL Server where the data warehouse databases were originally hosted.  
  
##  <a name="bkmk_locating"></a> Locate user accounts and instances of SQL Server  
 Use the following procedures to locate the user accounts and instances of SQL Server that are used by the data warehouse management server.  
  
#### To identify the SQL Server database and instance names used by the data warehouse management server  
  
1.  Log on to the data warehouse management server as a user with administrative credentials.  
  
2.  On the Windows desktop, click **Start**, and then click **Run**.  
  
3.  In the **Run** dialog box, in the **Open** box, type **regedit**, and then click **OK**.  
  
4.  In the Registry Editor window, expand **HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\System Center\\2010\\Common\\Database**, and then make note of the following registry values:  
  
    -   DatabaseName  
  
    -   DatabaseServerName  
  
    -   DataMartDatabaseName  
  
    -   DataMartSQLInstance  
  
    -   RepositoryDatabaseName  
  
    -   RepositorySQLInstance  
  
    -   StagingDatabaseName  
  
    -   StagingSQLInstance  
  
    -   OMDataMartDatabaseName  
  
    -   OMDataMartSQLInstance  
  
    -   CMDataMartDatabaseName  
  
    -   CMDataMartSQLInstance  
  
#### To identify the reporting server and instance names used by data warehouse management server  
  
1.  Log on to the data warehouse management server as a user with administrative credentials.  
  
     On the Windows desktop, click **Start**, and then click **Run**.  
  
     In the **Run** dialog box, in the **Open** box, type **regedit**, and then click **OK**.  
  
     In the Registry Editor window, expand **HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\System Center\\2010\\Common\\Reporting**, and then make note of the following registry values:  
  
    -   Server  
  
    -   ServerInstance  
  
    -   WebServiceURL  
  
#### To identify the service account used by the data warehouse management server  
  
1.  On the Windows desktop, click **Start**, and then click **Run**.  
  
2.  In the **Run** dialog box, in the **Open** box, type **services.msc**, and then click **OK**.  
  
3.  Locate the service System Center Data Access Service, and double\-click it.  
  
4.  In the **Properties** window, click the **Log On** tab.  
  
5.  Make a note of the user account name under **This account:**.  
  
6.  Repeat Steps 3 through 5 for the **System Center Management Configuration** service.  
  
#### To identify the reporting account used by the data warehouse management server  
  
1.  > [!NOTE]  
    >  The account that is configured by using the names in the following data sources in SQL Server Reporting Services is called the **Reporting account**.  
  
     Log on to the server with SQL Server Reporting Services that are hosting the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] reports.  
  
    > [!NOTE]  
    >  In this procedure, you will use values that you noted in the "To identify the SQL Server database and instance names used by the data warehouse management server" procedure.  
  
2.  In SQL Server Reporting Services, click **Start**, click **All Programs**, click the program group for the version of SQL Server you are running, click **Configuration Tools**, and then click **Reporting Services Configuration Manager**.  
  
3.  In the **Reporting Services Configuration Connection** dialog box, connect to the **SQL Reporting instance** that you noted in a previous procedure.  
  
4.  In **Reporting Services Configuration Manager**, click **Reporting Manager URL**.  
  
5.  On the **Reporting Manager URL** page, click the hyperlink that resembles http:\/\/\<Servername\>:portnumber\/Reports to open it in your web browser.  
  
6.  Open the **System Center** folder and then open the **Service Manager** folder.  
  
7.  Click the **DWDataMart** data source and make a note of the **User name** value under **Credentials stored securely in the report server**.  
  
8.  In your browser, click **Back** to return to the **Service Manager** folder.  
  
9. Click the **DWStagingAndConfig** data source and make a note of the **User name** value under **Credentials stored securely in the report server**.  
  
10. In your browser, click **Back** to return to the **Service Manager** folder.  
  
11. Click the **ConfigurationManager** data source and make a note of the **User name** value under **Credentials stored securely in the report server**.  
  
12. In your browser, click **Back** to return to the **Service Manager** folder.  
  
13. Click the **MultiMartDatasource** data source and make a note of the **User name** value under **Credentials stored securely in the report server**.  
  
14. In your browser, click **Back** to return to the **Service Manager** folder.  
  
15. Click the **OperationsManager** data source and make a note of the **User name** value under **Credentials stored securely in the report server**.  
  
16. Close the browser window.  
  
#### To identify the OLAP Account used by the data warehouse management server  
  
1.  Log on to the Service Manager server, click **Start**, click **All Programs**, click **Microsoft System Center 2012**, click **Service Manager**, and then click **Service Manager Shell**.  
  
2.  In the Windows PowerShell command prompt, copy the following command, and then press ENTER.  
  
    > [!NOTE]  
    >  Replace \<DWServerName\> with the name of your data warehouse management server.  
  
    ```  
    $class= get-scclass –Name Microsoft.SystemCenter.ResourceAccessLayer.ASResourceStore –ComputerName <DWServerName>  
    $OLAPServer= get-scclassinstance –class $class –ComputerName <DWServerName>  
    $OLAPServer.Server  
    ```  
  
    > [!NOTE]  
    >  The $OLAPServer.Server cmdlet  returns the name of the OLAP server that is hosting the DWASDataBase, and it contains the OLAP Account.  
  
3.  On a server where you have **SQL Server Management Studio** installed, do the following:  
  
    1.  Open SQL Server Management Studio.  
  
    2.  In the **Connect to Server** window, select **Analysis Services** in the **Server type** list.  
  
    3.  In the **Server name** list, type or select the name you noted from the output of the $OLAPServer.Server cmdlet in previous step, and then click **Connect**.  
  
    4.  In the **Object Explorer** pane, expand **Databases**, and then expand the **DWASDataBase** OLAP database.  
  
    5.  Expand the **Data Sources** folder, and then double\-click **CMDataMart**.  
  
    6.  In the **Data Source Properties – CMDataMart** dialog box, note the value of **Connection String**.  
  
    7.  Under **Security Settings**, click **Impersonation Account**, and then click the properties button \(…\), to open the **Impersonation Information** dialog box.  
  
    8.  In the **Impersonation Information** dialog box, note the user name.  
  
    9. Click **Cancel** twice to close the dialog boxes.  
  
    10. Repeat the steps above to note the Connection string and the User name for the DWDataMart and OMDataMart databases.  
  
##  <a name="BKMK_stop"></a> Stop Service Manager services  
 Use the following procedure to stop the Service Manager services on the data warehouse management server.  
  
#### To stop Service Manager services on the data warehouse management server  
  
1.  In the **Run** dialog box, in the **Open** text field, type **services.msc**, and then click **OK**.  
  
2.  In the **Services** window, in the **Services \(Local\)** pane, locate the following three services, and for each one, click **Stop**:  
  
    1.  System Center Data Access Service  
  
    2.  System Center Management  
  
        > [!NOTE]  
        >  For [!INCLUDE[smblue_1](../../../sm/deploy/deploy-guide/includes/smblue_1_md.md)], the System Center Management service was renamed to Microsoft Monitoring Agent.  
  
    3.  System Center Management Configuration  
  
##  <a name="BKMK_backup"></a> Back up the data warehouse databases  
 Use the following procedure to back up the data warehouse databases on the original computer running SQL Server.  
  
#### To back up the data warehouse databases  
  
1.  Log on to the original computer running SQL Server that is hosting the data warehouse databases, and open **SQL Server Management Studio**.  
  
2.  In the **Connect to Server** dialog box, follow these steps:  
  
    1.  In the **Server Type** list, select **Database Engine**.  
  
    2.  In the **Server Name** list, select the server name for your data warehouse database.  
  
    3.  In the **Authentication** list, select **Windows Authentication**, and then click **Connect**.  
  
3.  In the **Object Explorer** pane, expand **Databases**.  
  
4.  Right\-click the **DWStagingAndConfig** database, click **Tasks**, and then click **Back Up**.  
  
5.  In the **Back Up Database** dialog box, type a path and a file name in the **Destination on disk** text box, and then click **OK**.  
  
    > [!IMPORTANT]  
    >  The destination location must have enough available free disk space to store the backup files.  
  
6.  Click **OK** in the **Back Up Database** dialog box to start the back up.  
  
7.  Repeat these steps for the DWRepository, CMDWDataMart, OMDWDataMart, and DWDataMart databases.  
  
##  <a name="BKMK_offline"></a> Take the data warehouse databases offline  
 Use the following procedure to take the data warehouse databases offline on the original computer running SQL Server.  
  
#### To take the data warehouse databases offline  
  
1.  Log on to the original computer running SQL Server that is hosting the data warehouse databases, and open **SQL Server Management Studio**.  
  
2.  In the **Connect to Server** dialog box, follow these steps:  
  
    1.  In the **Server Type** list, select **Database Engine**.  
  
    2.  In the **Server Name** list, select the server name for your data warehouse database.  
  
    3.  In the **Authentication** list, select **Windows Authentication**, and then click **Connect**.  
  
3.  In the **Object Explorer** pane, expand **Databases**.  
  
4.  Right\-click the **DWStagingAndConfig** database, click **Tasks**, and then click **Take Offline**.  
  
5.  In the **Take database offline** dialog box, click **Close**.  
  
6.  Repeat the previous steps for the DWRepository, CMDWDataMart, OMDWDataMart, and DWDataMart databases.  
  
##  <a name="BKMK_restore"></a> Restore the data warehouse databases on the new computer running SQL Server  
 Use the following procedure to restore the data warehouse databases on the new computer running SQL Server.  
  
#### To restore the data warehouse databases  
  
1.  On the new computer running SQL Server, open **SQL Server Management Studio**.  
  
2.  In the **Connect to Server** dialog box, follow these steps:  
  
    1.  In the **Server Type** list, select **Database Engine**.  
  
    2.  In the **Server Name** list, select the server name for your Service Manager services database.  
  
    3.  In the **Authentication** list, select **Windows Authentication**, and then click **Connect**.  
  
3.  In the **Object Explorer** pane, right\-click the **Databases** folder, and then click **Restore Database**.  
  
4.  In the **Restore Database** dialog box, under the **To a point in time** text box, retain the default, **Most recent possible**, or select a specific date and time by clicking the browse button to open the **Point in Time Restore** dialog box.  
  
5.  To specify the source and location of the backup sets to restore, click **From Device**.  
  
6.  Click **Browse** to open the **Specify Backup** dialog box.  
  
7.  In the **Backup media** list box, select one of the listed device types. To select more devices for the Backup location, click **Add**.  
  
8.  In the **Select the backup sets to restore** grid, select the backups to restore. \(This grid displays the backups that are available for the specified location.\)  
  
9. On the **General** page, the name of the restoring database appears in the **To database** list. Select the **DWStagingAndConfig** database from the list.  
  
10. In the **Restore options** panel, select **Overwrite the existing database**.  
  
11. In the **Restore the database files as** options panel, verify that the original database file name and path are correct.  
  
12. For the **Recovery state** option, select **Leave the databases ready to use by rolling back the uncommitted transactions. Additional transaction logs cannot be restored \(RESTORE WITH RECOVERY\)**.  
  
13. Click **OK** to restore the database.  
  
14. Repeat the previous steps for the DWRepository, CMDWDataMart, OMDWDataMart, and DWDataMart databases.  
  
##  <a name="BKMK_prepareDB"></a> Prepare the data warehouse databases on the new database server  
 Use the following three procedures to prepare the data warehouse databases on the new database server:  
  
1.  To configure the DWStagingAndConfig database on the new computer running SQL Server  
  
2.  To configure the service account database permissions  
  
3.  To configure the DWStagingAndConfig tables  
  
#### To configure the DWStagingAndConfig database on the new computer running SQL Server  
  
1.  On the new computer running SQL Server, open **SQL Server Management Studio**.  
  
2.  In the **Connect to Server** dialog box, follow these steps:  
  
    1.  In the **Server Type** list, select **Database Engine**.  
  
    2.  In the **Server Name** list, select the name of the new computer running SQL Server that hosts the **DWStagingAndConfig** database.  
  
    3.  In the **Authentication** list, select **Windows Authentication**, and then click **Connect**.  
  
3.  In the **Object Explorer** pane, expand **Databases**, and then click **DWStagingAndConfig**.  
  
4.  In the toolbar, click **New Query**.  
  
5.  In the center pane, copy the following command, and then click **Execute**.  
  
    ```  
    sp_configure 'clr enabled', 1  
    go  
    reconfigure  
    go  
    ```  
  
6.  In the center pane, remove the command you typed in the previous step, copy the following command, and then click **Execute**.  
  
    ```  
    ALTER DATABASE DWStagingAndConfig SET SINGLE_USER WITH ROLLBACK IMMEDIATE  
    ```  
  
7.  In the center pane, remove the command you typed in the previous step, copy the following command, and then click **Execute**.  
  
    ```  
    ALTER DATABASE DWStagingAndConfig SET ENABLE_BROKER  
    ```  
  
8.  In the center pane, remove the command you typed in the previous step, type the following command, and then click **Execute**.  
  
    ```  
    ALTER DATABASE DWStagingAndConfig SET MULTI_USER  
    ```  
  
#### To configure the service account database permissions  
  
1.  In the **Object Explorer** pane, expand **Security**, and then expand **Logins**. Right\-click **Logins**, and then click **New Login**.  
  
2.  Click **Search**.  
  
3.  Type the user name by using the domain\\user name format for the data warehouse service account, click **Check Names**, and then click **OK**.  
  
    > [!NOTE]  
    >  If the Data Access Account is running as LocalSystem, use the format \<domain\\computername$\> in SQL Logins, where \<computername\> is the name of the management server.  
  
4.  In the **Select a page** pane, click **User Mapping**.  
  
5.  In the **Users mapped to this login** area, in the **Map** column, select the row that represents the name of the DWStagingAndConfig database. DWStagingAndConfig is the default database name.  
  
6.  In the **Database role membership for: DWStagingAndConfig** area, ensure that the following entries are selected:  
  
    -   **configsvc\_users**  
  
    -   **db\_accessadmin**  
  
    -   **db\_datareader**  
  
    -   **db\_datawriter**  
  
    -   **db\_ddladmin**  
  
    -   **db\_securityadmin**  
  
    -   **dbmodule\_users**  
  
    -   **public**  
  
    -   **sdk\_users**  
  
    -   **sql\_dependency\_subscriber**  
  
    -   **db\_owner**  
  
7.  In the **Database role membership for: DWRepository** area, ensure that the following entries are selected:  
  
    -   **db\_owner**  
  
    -   **public**  
  
8.  In the **Database role membership for: DWDataMart** area, ensure that the following entries are selected:  
  
    -   **db\_owner**  
  
    -   **public**  
  
9. Click **OK**.  
  
10. In the **Object Explorer** pane, expand **Security**, and then expand **Logins**.  
  
11. Right\-click **Logins**, and then **click New  Login**.  
  
12. Click **Search**.  
  
13. Type the user name in the domain\\user name format for the reporting account, click **Check Names**, and then click **OK**.  
  
14. In the **Select a page** pane, click **User Mapping**.  
  
15. In the **Users mapped to this login** area, in the **Map** column, select the row that represents the name of the DWStagingAndConfig. DWStagingAndConfig is the default database name.  
  
16. In **the Database role membership for: DWStagingAndConfig** area, ensure that the following entries are selected:  
  
    -   **db\_datareader**  
  
    -   **public**  
  
17. In the **Database role membership for: DWRepository** area, ensure that the following entries are selected:  
  
    -   **db\_datareader**  
  
    -   **public**  
  
    -   **reportuser**  
  
18. In the **Database role membership for: DWDataMart** area, ensure that the following entries are selected:  
  
    -   **db\_datareader**  
  
    -   **public**  
  
    -   **reportuser**  
  
19. In the **Database role membership for: OMDWDataMart** area, ensure that the following entries are selected:  
  
    -   **db\_datareader**  
  
    -   **public**  
  
    -   **reportuser**  
  
20. In the **Database role membership for: CMDWDataMart** area, ensure that the following entries are selected:  
  
    -   **db\_datareader**  
  
    -   **public**  
  
    -   **reportuser**  
  
21. Click **OK**.  
  
22. In the **Object Explorer** pane, expand **Security**, and then expand **Logins**.  
  
23. Right\-click **Logins**, and then click **New  Login**.  
  
24. Click **Search**.  
  
25. Type the user name in the domain\\user name format for the **OLAP account**, click **Check Names**, and then click **OK**.  
  
26. In the **Select a page** pane, click **User Mapping**.  
  
27. In the **Database role membership for: DWDataMart** area, ensure that the following entries are selected:  
  
    -   **db\_datareader**  
  
    -   **public**  
  
    -   **reportuser**  
  
28. In the **Database role membership for: OMDWDataMart** area, ensure that the following entries are selected:  
  
    -   **db\_datareader**  
  
    -   **public**  
  
    -   **reportuser**  
  
29. In the **Database role membership for: CMDWDataMart** area, ensure that the following entries are selected:  
  
    -   **db\_datareader**  
  
    -   **public**  
  
    -   **reportuser**  
  
30. Click **OK**.  
  
#### To configure the DWStagingAndConfig tables  
  
1.  In the **Object Explorer** pane, expand **Databases**, expand **DWStagingAndConfig**, and then expand **Tables**.  
  
2.  Right\-click **dbo.MT\_Microsoft$SystemCenter$ManagementGroup**, and then click **Edit Top 200 Rows**.  
  
3.  In the center pane, locate the column **SQLServerName\_ 43FB076F\_7970\_4C86\_6DCA\_8BD541F45E3A**, and then in the first row of the column, type the name of the new computer running SQL Server that is hosting the DWStagingAndConfig database. In the case of named instances, type **ComputerName\\InstanceName**.  
  
4.  Right\-click **dbo. MT\_Microsoft$SystemCenter$ResourceAccessLayer$SqlResourceStore**, and then click **Edit Top 200 Rows**.  
  
5.  Update the column **Server\_48B308F9\_CF0E\_0F74\_83E1\_0AEB1B58E2FA** for rows representing DWStagingAndConfig, DWRepository, CMDWDataMart, OMDWDataMart, and DWDataMart by typing the name of the new computer running SQL Server that is hosting the respective databases. In the case of named instances, type **ComputerName\\InstanceName**.  
  
6.  Right\-click **dbo.MT\_Microsoft$SystemCenter$ResourceAccessLayer$CMDBResourceStore**, and then click **Edit Top 200 Rows**.  
  
7.  In the center pane, locate the column **Server\_48B308F9\_CF0E\_0F74\_83E1\_0AEB1B58E2FA**, and in the first row of the column, type the name of the new computer running SQL Server that is hosting the DWStagingAndConfig database. In the case of named instances, type **ComputerName\\InstanceName**.  
  
8.  Right\-click **LFX.DataSource**, and then click **Edit Top 200 Rows**.  
  
9. In the center pane, locate the **DataSourceAddress** column, and in the first row of the column, locate the entry that starts with **Data Source \= \<server name\>; Initial Catalog \= DWStagingAndConfig; Persist Security Info\=False**. Replace **\<server name\>** with the name of the new computer running SQL Server.  
  
10. Ensure that the values you typed were saved by querying the tables specified in the previous steps.  
  
11. Close **Microsoft SQL Server Management Studio**.  
  
##  <a name="BKMK_updatename"></a> Update data warehouse management Server with the new database server name  
 Use the following procedure to update the data warehouse management server to use the new database server name.  
  
#### To update the data warehouse management server to use the new database server name  
  
1.  Log on to the computer as a user with administrative credentials.  
  
2.  On the Windows desktop, click **Start**, and then click **Run**.  
  
3.  In the **Run** dialog box, in the **Open** box, type **regedit**, and then click **OK**.  
  
    > [!CAUTION]  
    >  Incorrectly editing the registry might severely damage your system; therefore, before making changes to the registry, back up any valued data on the computer.  
  
4.  In the Registry Editor window, expand **HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\System Center\\2010\\Common\\Database**.  
  
5.  In the right pane, double\-click **DatabaseServerName**.  
  
6.  In the **Edit String** box, in the **Value data** box, type the name of the new computer running SQL Server that hosts the DWStagingAndConfig database. If you are using a named instance of SQL Server, use the Computer Name\\Instance name format.  
  
7.  Click **OK**.  
  
8.  Repeat the previous steps for the registry values to reflect the new name of the computer running SQL Server for the DWDataMart, OMDWDataMart, CMDWDataMart, DWRepository, and DWStagingAndConfig databases.  
  
    -   DataMartSQLInstance  
  
    -   RepositorySQLInstance  
  
    -   StagingSQLInstance  
  
    -   OMDataMartSQLInstance  
  
    -   CMDataMartSQLInstance  
  
##  <a name="BKMK_updateDS"></a> Update the data sources on the reporting server  
 Use the following procedure to update data sources on the reporting server to point to the new computer running SQL Server.  
  
#### To update the data sources on the reporting server  
  
1.  Log on to the Service Manager reporting server, and start **Reporting Services Configuration Manager**.  
  
2.  In the **Reporting Services Configuration Connection** dialog box, connect to the correct reporting server instance as noted in the section To identify the reporting server and instance name used by data warehouse management server.  
  
3.  In the Reporting Services Configuration Manager list, select **Report Manager URL**.  
  
4.  On the **Report Manager URL** page, click the hyperlink that resembles **http:\/\/\<Servername\>:portnumber\/Reports** to open the **Reports** home page in your Internet browser.  
  
5.  On the home page, open the **System Center** folder, and then open the **Service Manager** folder.  
  
6.  Open the list of Service Manager items, and then click the **DWDataMart** data source.  
  
7.  In the **Connection string** box, the string resembles `data source=<server name>;initial catalog=DWDataMart`. Replace the existing name of the computer running SQL Server by typing the name of the new computer running SQL Server.  
  
8.  Go back to the previous Service Manager folder webpage, and click the **DWStagingAndConfig** data source.  
  
9. In the **Connection string** box, the string resembles `data source=<server name>;initial catalog= DWStagingAndConfig`. Replace the existing name of the computer running SQL Server by typing the name of the new computer running SQL Server.  
  
10. Go back to the previous Service Manager folder webpage and click the **ConfigurationManager** data source.  
  
11. In the **Connection string** box, the string resembles `data source=<server name>;initial catalog= CMDWDataMart`. Replace the existing name of the computer running SQL Server by typing the name of the new computer running SQL Server.  
  
12. Go back to the previous Service Manager folder webpage and click the **MultiMartDatasource** data source.  
  
13. In the **Connection string** box, the string resembles `<root><source id='DWDataMart' connectionString='Data Source=<Server name>;Initial Catalog=DWDataMart;Integrated Security=True' /><source id='OMDataMart' connectionString='Data Source=<Server name>;Initial Catalog=OMDWDataMart;Integrated Security=True' /><source id='CMDataMart' connectionString='Data Source=<Server name>;Initial Catalog=CMDWDataMart;Integrated Security=True' /></root>`. Replace the existing name of the computer running SQL Server by typing the name of the new computer running SQL Server.  
  
14. Go back to the previous Service Manager folder webpage and click the **Operations Manager** data source.  
  
15. In the **Connection string** box, the string resembles `data source=<server name>;initial catalog= OMDWDataMart`. Replace the existing name of the computer running SQL Server by typing the name of the new computer running SQL Server.  
  
16. Close your web browser.  
  
##  <a name="BKMK_updateDSAS"></a> Update the data sources for the Analysis Services  
 Use the following procedure to update the connection strings for the data sources on the server that hosts the Analysis Services database.  
  
#### To update the data sources for the Analysis services  
  
1.  Log on to the server that hosts the SQL Server Analysis Services database.  
  
2.  Open **SQL Server Management Studio**.  
  
3.  In the **Connect to Server** dialog box, in the **Server Type** list, select **Analysis Services**.  
  
4.  In the **Server name** list, type the server name that you received as output from the $OLAPServer.Server cmdlet. \(You noted this information in the To identify the OLAP Account used by the data warehouse management server section earlier in this topic.\)  
  
5.  In the **Object Explorer** pane, expand **Databases**, and then expand **DWASDataBase**.  
  
6.  Expand **Data Sources**, and then double\-click **CMDataMart**.  
  
7.  In the **Data Source Properties – CMDataMart** dialog box, select **Connection string Provider\=SQLNCLI10.1;Data Source\=\<servername\>;Integrated Security\=SSPI;Initial Catalog\=CMDWDataMart**.  
  
8.  Replace \<servername\> with the name of the computer running SQL Server that hosts the CMDWDataMart database.  
  
9. You need to re\-enter the impersonation account password when you’ve completed updating the Data Source server. Select the ellipsis button to the right of **ImpersonateAccount** and then add the password in the **Impersonation Information** dialog box. Click **OK** to accept the changes.  
  
10. Repeat the previous steps to update the connection strings for the DWDataMart and OMDataMart data sources.  
  
##  <a name="BKMK_StartSer"></a> Start Service Manager Services on the data warehouse management server  
 Use the following procedure to start the Service Manager services on the data warehouse management server.  
  
#### To start Service Manager services on the data warehouse management server  
  
1.  In the **Run** dialog box, in the **Open** text field, type **services.msc**, and then click **OK**.  
  
2.  In the **Services** window, in the **Services \(Local\)** pane, locate the following three services, and for each one, click **Start**:  
  
    1.  System Center Data Access Service  
  
    2.  System Center Management  
  
        > [!NOTE]  
        >  For [!INCLUDE[smblue_1](../../../sm/deploy/deploy-guide/includes/smblue_1_md.md)], the System Center Management service was renamed to Microsoft Monitoring Agent.  
  
    3.  System Center Management Configuration  
  
## See also  
 [Appendix B \- Guidance for Moving the Service Manager and Data Warehouse Databases](../../../sm/deploy/deploy-guide/Appendix-B---Guidance-for-Moving-the-Service-Manager-and-Data-Warehouse-Databases.md)