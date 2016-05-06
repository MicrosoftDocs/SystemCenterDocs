---
title: Moving the Operational Database
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3b15fd01-1be5-433d-afa0-30dce77d505a
---
# Moving the Operational Database
Hardware and software updates often mean that it’s time to make changes to your Operations Manager configuration. Moving the operational database is such a change. If your current hardware is failing or out of date and newer hardware is available—or perhaps your organizational policy requires that you move the database to a newer operating system and server—then it’s likely time to move the operational database. In either case, when you move the operational database, you move it to a newer operating system and server. Here’s how to do it.

Moving the operational database requires Microsoft SQL Server configuration. During the move, you need to back up a database, restore a database, update a database table, add new Logins, and modify User Mapping settings for Logins. For more information, see [SQL Server documentation](http://go.microsoft.com/fwlink/p/?linkID=162007).

## In this topic
[Stop Operation Manager services](assetId:///44cb1aa4-2bef-417d-a0c9-f23d84e2192b#bkmk_Step1_StopSvcs)

[Create a backup of the old operational database and move it to the new server](assetId:///44cb1aa4-2bef-417d-a0c9-f23d84e2192b#bkmk_Step2_BkupOldMoveNew)

[Restore the operational database on the new server](assetId:///44cb1aa4-2bef-417d-a0c9-f23d84e2192b#bkmk_Step3_RestoreDB)

[Update the registries and configuration files on the management servers](assetId:///44cb1aa4-2bef-417d-a0c9-f23d84e2192b#bkmk_Step4_UpdateRegConfig)

[Update the operational database with the new database server name](assetId:///44cb1aa4-2bef-417d-a0c9-f23d84e2192b#bkmk_Step5_UpdateOpDb)

[On the new server, update the operational database with the new database server name to specify the location of the Application Performance Monitoring tables](assetId:///44cb1aa4-2bef-417d-a0c9-f23d84e2192b#bkmk_Step6_UpdateAppPeftbl)

[Update security credentials on the new server hosting the operational database](assetId:///44cb1aa4-2bef-417d-a0c9-f23d84e2192b#bkmk_Step7_UpdateCredentials)

[Start Operation Manager services](assetId:///44cb1aa4-2bef-417d-a0c9-f23d84e2192b#bkmk_Step8_StartSvcs)

## To move the operational database

### <a name="bkmk_Step1_StopSvcs"></a>1.  Stop Operation Manager services
On all the management servers in the management group, stop the Operations Manager services:

-   System Center Data Access

-   System Center Management

-   System Center Management Configuration

### <a name="bkmk_Step2_BkupOldMoveNew"></a>2. Create a backup of the old operational database and move it to the new server

1.  On the original operational database server, use Microsoft SQL Server Management Studio to create a full backup of the operational database. The default name is OperationsManager.

    For more information, see [How to: Back Up a Database \(SQL Server Management Studio\)](http://go.microsoft.com/fwlink/p/?linkID=206259).

2.  Copy the backup file to a local drive of the new database server.

3.  Optionally, on the old server that hosts the operational database, delete the operational database.

### <a name="bkmk_Step3_RestoreDB"></a>3.  Restore the operational database on the new server
Do these steps on the new SQL Server:

1.  Use Microsoft SQL Server Management Studio to restore the operational database. \(In the previous step, you moved the database backup file to a local drive of the new server.\) In this step, you can change the name of the database and choose the file location.

    For more information, see [How to: Restore a Database Backup \(SQL Server Management Studio\)](http://go.microsoft.com/fwlink/p/?linkID=245795).

2.  In the SQL Server Management Studio, verify that the database is online.

### <a name="bkmk_Step4_UpdateRegConfig"></a>4.  Update the registries and configuration files on the management servers
Do these steps on each management server in the management group:

1.  Update the registry to refer to the new SQL Server\-based computer.

    > [!NOTE]
    > Before editing the registry, follow your organization’s backup policies with regard to the registry.

    1.  Log on to the management server with Administrator permissions.

    2.  Click **Start**, select **Run**, type **regedit** in the **Open** box, and then click **OK** to start Registry Editor.

    3.  Navigate to **HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\Microsoft Operations Manager\\3.0\\Setup**.

    4.  For each of the following keys, double\-click the name, change the value to the hostname of the SQL Server\-based computer now hosting the operational database, and then click **OK** to save your changes.

        -   DatabaseName

        -   DatabaseServerName

            > [!NOTE]
            > If you are using a named instance of SQL Server, be sure to use the ServerName\\Instance name format.

    5.  Navigate to **HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\System Center\\2010\\Common\\Database** and repeat step **d**.

    6.  Close the Registry Editor.

2.  On each management server, edit the following file:

    `%ProgramFiles%\System Center 2012\Operations Manager\Server\ConfigService.config`

    In the `<Category>` tags named “Cmdb” and “ConfigStore”, change the value for `ServerName` to the name of the new SQL server.

### <a name="bkmk_Step5_UpdateOpDb"></a>5.  Update the operational database with the new database server name

1.  Open SQL Server Management Studio.

2.  Expand **Databases**, **OperationsManager**, and **Tables**.

3.  Right\-click **dbo.MT\_Microsoft$SystemCenter$ManagementGroup**, and then click **Edit Top 200 Rows**.

4.  Change the value in the **SQLServerName\_6B1D1BE8\_EBB4\_B425\_08DC\_2385C5930B04** column to reflect the name of the new SQL Server\-based computer.

5.  Save the change.

### <a name="bkmk_Step6_UpdateAppPeftbl"></a>6.  On the new server, update the operational database with the new database server name to specify the location of the Application Performance Monitoring tables

1.  Open SQL Server Management Studio.

2.  Expand **Databases**, **OperationsManager**, and **Tables**.

3.  Right\-click **dbo.MT\_Microsoft$SystemCenter$OpsMgrDB$AppMonitoring**, and then click **Edit Top 200 Rows**.

4.  Change the value in the **MainDatabaseServerName\_5C00C79B\_6B71\_6EEE\_4ADE\_80C11F84527A** column to reflect the name of the new SQL Server\-based computer.

5.  Save the change.

### <a name="bkmk_Step7_UpdateCredentials"></a>7.  Update security credentials on the new server hosting the operational database

1.  Expand **Security**, expand **Logins**, and then do the following:

    1.  Add the data writer account. For more information, see [How to Create a SQL Server Login](http://go.microsoft.com/fwlink/p/?linkID=245796).

    2.  Add the action account.

    3.  Add the Data Access Service \(DAS\) computer account, using the form “domain\\computername$”.

    4.  For the DAS computer account, add the following user mappings:

        -   ConfigService

        -   db\_accessadmin

        -   db\_datareader

        -   db\_datawriter

        -   db\_ddladmin

        -   db\_securityadmin

        -   sdk\_users

        -   sql\_dependency\_subscriber

    5.  **If an account has not existed before in the SQL instance** in which you are adding it, the mapping will be picked up by SID automatically from the restored operations database. If the account has existed in that SQL instance before, you receive an error indicating failure for that login, although the account appears in Logins. If you are creating a new login, ensure the User Mapping for that log in and database are set to the same values as the previous login as follows:

        |||
        |-|-|
        |**Log in**|**Database**|
        |DW Data Writer|-   apm\_datareader<br /><br />-   apm\_datawriter<br /><br />-   db\_datareader<br /><br />-   dwsynch\_users|
        |Action account|-   db\_datareader<br /><br />-   db\_datawriter<br /><br />-   db\_ddladmin<br /><br />-   dbmodule\_users|
        |DAS\/Configuration account **Note:** If DAS\/Configuration uses the LocalSystem account, specify computer account in form <domain>\\<computername>$.|-   ConfigService<br /><br />-   db\_accessadmin<br /><br />-   db\_datareader<br /><br />-   db\_datawriter<br /><br />-   db\_ddladmin<br /><br />-   db\_securityadmin<br /><br />-   sdk\_users<br /><br />-   sql\_dependency\_subscriber|

2.  Execute these SQL commands on new Operations database instance:

    **sp\_configure ‘show advanced options’,1**

    **reconfigure**

    **sp\_configure ‘clr enabled’,1**

    **reconfigure**

3.  Run the following SQL query:

    **SELECT is\_broker\_enabled FROM sys.databases WHERE name\='OperationsManager'**

    If the result of this query was an **is\_broker\_enabled** value of 1, skip this step. Otherwise, run the following SQL queries:

    **ALTER DATABASE OperationsManager SET SINGLE\_USER WITH ROLLBACK IMMEDIATE**

    **ALTER DATABASE OperationsManager SET ENABLE\_BROKER**

    **ALTER DATABASE OperationsManager SET MULTI\_USER**

### <a name="bkmk_Step8_StartSvcs"></a>8.  Start Operation Manager services
On all the management servers in the management group, start the Operations Manager services:

-   System Center Data Access

-   System Center Management

-   System Center Management Configuration

## See Also
[Making Changes to an Operations Manager  Environment](assetId:///22675bc3-1668-44c7-bc40-484e06a01946)
[How to Move the Data Warehouse Database](assetId:///73498030-fc5a-44cf-b040-ffae71c1f3f3)

