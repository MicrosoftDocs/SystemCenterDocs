---
title: Create a lab environment for upgrade
description: To prepare for upgrade, create a lab environment and prepare it for production data.
ms.service: system-center
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.subservice: service-manager
ms.topic: upgrade-and-migration-article
ms.custom: UpdateFrequency2, engagement-fy23, engagement-fy24
---

# Set up a lab environment for upgrade testing

Use the following procedures to prepare for Service Manager upgrade by creating a lab environment and preparing it for production data for the purpose of upgrade testing.

Many of the procedures in this article are lengthy and might take a considerable amount of time to complete. As long as you complete the procedures in order, you don't need to complete them without stopping.

## Restore the Service Manager database in the lab environment

Use the following procedure to restore the production Service Manager database using Microsoft SQL Server 2016 or later.  

1. After connecting to the appropriate instance of the Microsoft SQL Server Database Engine, in Object Explorer, select the server name to expand the server tree.  
2. Expand **Databases**, and depending on the database, either select a user database or expand **System Databases**, and select a system database.  
3. Right-click the database, point to **Tasks**, and select **Restore**. The Back Up Database dialog appears.  
4. Select **Database**, which opens the **Restore Database** dialog.  
5. On the **General** page, the name of the restoring database appears in the **To database** list box. To create a new database, enter its name in the list box.  
6. In the **To a point in time** text box, either retain the default (Most recent possible) or select a specific date and time by selecting the browse button, which opens the **Point in Time Restore** dialog. For more information, see [How to: Restore to a Point in Time \(SQL Server Management Studio\)](/sql/relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model).  
7. To specify the source and location of the backup sets to restore, select either **From database** or **From device**.  
8. In the **Select the backup sets to restore** grid, select the backups to restore. For more information, see [Restore Database \(General Page\)](/sql/relational-databases/backup-restore/restore-database-general-page).  
9. To view or select the advanced options, select **Options** in the **Select a page pane**.  
10. In the **Restore options** panel, choose one of the following options most appropriate for your situation:  
    - Overwrite the existing database  
    - Preserve the replication settings  
    - Prompt before restoring each backup  
    - Restrict access to the restored database  

      For more information, see [Restore Database \(Options Page\)](/sql/relational-databases/backup-restore/restore-database-options-page)  
11. Optionally, you can restore the database to a new location by specifying a new restore destination for each file in **Restore the database files as**. For more information, see [Restore Database \(Options Page\)](/sql/relational-databases/backup-restore/restore-database-options-page).  
12. In the **Recovery state** panel, select one of the following options most appropriate for your environment:  
    - **Leave the database ready to use by rolling back the uncommitted transactions. Additional transaction logs cannot be restored. \(RESTORE WITH RECOVERY\)**  

      > [!NOTE]  
      > Choose this option only if you're restoring all the necessary backups at this time.  

    - **Leave the database non\-operational, and do not roll back the uncommitted transactions. Additional transaction logs can be restored. \(RESTORE WITH NORECOVERY\)**  
    - **Leave the database in read\-only mode. Undo uncommitted transactions, but save the undo actions in a standby file so that recovery effects can be reverted. \(RESTORE WITH STANDBY\)**  

      For more information, see [Restore Database \(Options Page\)](/sql/relational-databases/backup-restore/restore-database-options-page).

## Prepare the Service Manager database in the lab environment

Use the following procedure to prepare the Service Manager database in the lab environment. Perform this procedure on the computer that is hosting the Service Manager database that is being used by the secondary management server, the management server in your lab environment.  

### Configure the database  

1. On the computer hosting the Service Manager database for the secondary management server, select **Start**, select **All Programs**, select **Microsoft SQL Server 2016**, and select **SQL Server Management Studio**.  
2. In the **Connect to Server** dialog, follow these steps:  
    1. In the **Server Type** list, select **Database Engine**.  
    2. In the **Server Name** list, select the server name for your Service Manager or data warehouse databases.  
    3. In the **Authentication** list, select **Windows Authentication**, and select **Connect**.  
3. In the **Object Explorer** pane, expand **Databases**, and select **ServiceManager**.  
4. In the toolbar, select **New Query**.  
5. In the center pane, enter the following commands, and select **Execute**.  

    ```powershell
    sp_configure 'clr enabled', 1  
    go  
    reconfigure  
    go   
    ```  

6. In the center pane, remove the commands you entered in the previous step, enter the following commands, and select **Execute**.  

    ```powershell
    ALTER DATABASE ServiceManager SET SINGLE_USER WITH ROLLBACK IMMEDIATE  
    ```  

7. In the center pane, remove the commands you entered in the previous step, enter the following commands, and select **Execute**.  

    ```powershell    
    ALTER DATABASE ServiceManager SET ENABLE_BROKER  
    ```  

8. In the center pane, remove the commands you entered in the previous step, enter the following commands, and select **Execute**.  

    ```powershell
    ALTER DATABASE ServiceManager SET MULTI_USER  
    ```  

### Configure the service account  

1. In the **Object Explorer** pane, expand **Security**, and then expand **Logins**.  
2. Right-click **Logins**, and select **New Login**  
3. Perform the following procedures in the **Login - New** wizard:  
    1. Select **Search**.  
    2. Enter the username \(domain\\username\) for the service account for Service Manager database in the lab environment, select **Check Names**, and select **OK**.  

        > [!NOTE]  
        > If the Data Access Account is running as LocalSystem, use the format \<domain\\computername$\> in SQL Logins, where \<computername\> is the name of the management server.  

    3. In the **Select a page** pane, select **User Mapping**.  
    4. In the **Users mapped to this login** area, in the **Map** column, select the row that represents the name of the Service Manager database \(**ServiceManager** is the default database name\).  
    5. In the **Database role membership for: ServiceManager** area, ensure that the following entries are selected:  
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
    6. Select **Ok**  

### Configure Service Manager tables  

1. In the **Object Explorer** pane, expand **Databases**, expand **ServiceManager**, and then expand **Tables**.  
2. Right-click **dbo.MT\_Microsoft$SystemCenter$ManagementGroup**, and select **Edit Top 200 Rows**.  
3. In the center pane, locate the column **SQLServerName\_43FB076F\_7970\_4C86\_6DCA\_8BD541F45E3A**.  
4. In the first row and second rows of this column, enter the computer name of the computer hosting the Service Manager database in the lab environment. For named instances, enter computer name\\instance name.  
5. Right-click **dbo. MT\_Microsoft$SystemCenter$ResourceAccessLayer$SqlResourceStore**, and select **Edit Top 200 Rows**.  
6. In the center pane, locate the column **Server\_43FB076F\_7970\_4C86\_6DCA\_8BD541F45E3A**.  
7. In the first row of this column, enter the computer name of the computer hosting the SQL Server for the Service Manager database in the lab environment. For named instances, enter computer name\\instance name.  
8. Right-click **LFX.DataSource**, and select **Edit Top 200 Rows**.  
9. In the center pane, locate the column **DataSourceAddress**.  
10. In the first row of this column, locate the entry that starts with **Data Source \= \<server name\>; Initial Catalog \= ServiceManager; Persist Security Info\=False**. Enter the name of the computer hosting SQL Server in the lab environment in place of **\<server name\>**.  
11. Right-click **dbo. MT\_Microsoft$SystemCenter$ResourceAccessLayer$SdkResourceStore**, and select **Edit Top 200 Rows**.  
12. In the center pane, locate the column **Server\_48B308F9\_CF0E\_0F74\_83E1\_0AEB1B58E2FA**.  
13. In all the rows in this column, enter the name of the computer hosting the Service Manager management server in the lab environment.  
14. Right-click **\[dbo\].\[MT\_Microsoft$SystemCenter$ResourceAccessLayer$CmdbResourceStore\]**, and select **Edit Top 200 Rows**.  
15. In all the rows, update the column **Server\_48B308F9\_CF0E\_0F74\_83E1\_0AEB1B58E2FA**, enter the name of the SQL computer hosting the Service Manager database in the lab environment  
16. In the toolbar, select **New Query**.  
17. In the center pane, enter the following command, and select **Execute**.  

    ```powershell     
    Delete from dbo.MT_Microsoft$SystemCenter$ResourceAccessLayer$DwSdkResourceStore  
    ```  

18. Close **Microsoft SQL Server Management Studio**.  

### Configure the lab Service Manager management server

- Using Registry Editor, expand the following path and update **DatabaseServerName** :  

     HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\System Center\\2010\\Common\\Database

## Edit the registry on the Service Manager Management Server in the lab environment

Use the following procedure to edit the registry on the Service Manager management server in the lab environment.

> [!CAUTION]
> Incorrectly editing the registry might severely damage your system; therefore, before making changes to the registry, back up any valued data on the computer.

### Edit the registry

1. On the computer hosting the Service Manager management server in the lab environment, sign in to the computer as a user with administrative credentials.
2. On the Windows desktop, select **Start**, and select **Run**.
3. In the **Run** dialog, in the **Open** box, enter *regedit*, and select **OK**.
4. In the Registry Editor window, expand **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\System Center\2012\Common\Database**.
5. In the right pane, double-click **DatabaseServerName**.
6. In the **Edit String** box, in the **Value data** box, enter the name of the computer hosting the Service Manager database SQL Server in the lab environment. If you're using a named instance of SQL Server, use the Computer Name\Instance name format.
7. Select **OK**, and then close the Registry Editor.

## Start Service Manager services on the secondary management server

Use the following procedure to start the Service Manager services.  

### Start Service Manager services  

1. On the Windows desktop, select **Start**, and select **Run**.  
2. In the **Run** dialog, in the **Open** field, enter **services.msc**, and select **OK**.  
3. In the **Services** window, in the **Services \(Local\)** pane, locate the following three services and for each one, and select **Start**:  
    - System Center Data Access Service  
    - System Center Management  
    - System Center Management Configuration

## Promote a secondary management server in a lab environment

Use the following procedure to promote the secondary management server.  

1. On the secondary management server, do the following:  
    1. Close the Service Manager console.  
    2. On the Windows desktop, select **Start**, and select **Run**.  
    3. In the **Run** dialog, in the **Open** text field, enter **services.msc**, and select **OK**.  
    4. In the **Services** window, in the **Services \(Local\)** pane, locate the following three services and for each one, and select **Stop**:  
        - System Center Data Access Service  
        - System Center Management  
        - System Center Management Configuration  
    5. Leave the **Services** window open.  
    6. Open Windows Explorer. Locate the \\Program Files\\Microsoft System Center\\Service Manager folder.  
    7. In this folder, delete the Health Service State folder and all of its contents.  
2. Do the following on the ServiceManager database on the Test SQL Server instance:  
    1. On the Windows desktop, select **Start**, point to **Programs**, point **to Microsoft SQL Server 2016**, and select **SQL Server Management Studio**.  
    2. In the Connect to Database Engine dialog, follow these steps:  
        1. In the **Server name** box, enter the name of the server that hosts the ServiceManager database.  
        2. In the **Authentication** box, select **Windows Authentication**.  
        3. Select **Connect**.  
    3. In the **Object Explorer** pane, expand **Databases**, and select **ServiceManager**.  
    4. On the toolbar, select **New Query**.  
    5. In the **SQLQuery1.sql** pane \(center pane\), enter the following, where \<FQDN of your server\> is the FQDN of the management server that you're promoting:  
         **EXEC p\_PromoteActiveWorkflowServer '\<FQDN of your server\>'**  
         On the toolbar, select **Execute**.  
    6. At the bottom of the **SQLQuery1.sql** pane \(center pane\), observe that **Query executed successfully** is displayed.  
    7. Exit Microsoft SQL Server Management Studio.  
3. Do the following on the secondary management server:  
    1. On the Windows desktop, select **Start**, and select **Run**.  
    2. In the **Run** dialog, in the **Open** field, enter **services.msc**, and select **OK**.  
    3. In the **Services** window, in the **Services \(Local\)** pane, locate the following three services and for each one, select **Start**.  
        - System Center Data Access Service  
        - System Center Management  
        - System Center Management Configuration  

Your secondary management server is now the primary management server for the management group.

## Enable the connectors in the lab environment

Use the following procedure to enable the Service Manager connectors in the lab environment. In this procedure, you won't be enabling the Operations Manager connector.  

> [!WARNING]  
> Don't enable or delete the Operations Manager alert connector in the lab environment. Doing so will cause the alert connector in the production environment to fail.  

### Enable a connector  

1. In the Service Manager console, select **Administration**.  
2. In the **Administration** pane, expand **Administration**, and select **Connectors**.  
3. In the **Connectors** pane, select the connector that you want to enable.  
4. In the **Tasks** pane, under the connector name, select **Enable**.

## Install a new data warehouse server in the lab environment

Use the following procedure to install a new data warehouse server in the lab environment.  

### Install a data warehouse management server and data warehouse databases  

1. Sign in to the computer by using an account that has administrative rights.  
2. On the Service Manager installation media, double-click the **Setup.exe** file.  
3. On the **Microsoft System Center Service Manager 2016** page, select **Install a Service Manager data warehouse management server**.  
4. On the **Product registration** page, enter information in the boxes. In the **Product key** boxes, enter the product key you received with Service Manager, or alternatively, select **Install as an evaluation edition \(180 day trial\)?.** Read the Microsoft Software License Terms, and, if applicable, select **I have read, understood, and agree with the terms of the license agreement**, and select **Next**.  
5. On the **Installation location** page, verify that sufficient free disk space is available, and select **Next**. If necessary, select **Browse** to change the location in which the Service Manager data warehouse management server will be installed.  
6. On the **System check results** page, ensure that prerequisites passed or at least passed with warnings, and select **Next**.  
7. On the **Configure data warehouse databases** page, Service Manager checks the computer you're using to see if it can host the data warehouse databases. For this configuration, confirm that the database server is the computer on which you're installing the data warehouse management server, and then select **Next**.  

    > [!WARNING]  
    > A warning message appears if you're using the default collation \(SQL\_Latin1\_General\_CP1\_CI\_AS\). Support for multiple languages in Service Manager isn't possible when you're using the default collation. If later you decide to support multiple languages using a different collation, you've to reinstall SQL Server.  

8. On the **Configure the data warehouse management group** page, follow these steps:  
    1. In the **Management group name** box, enter a unique name for the group.  

        > [!WARNING]  
        > Management group names must be unique. Don't use the same management group name when you deploy a Service Manager management server and a Service Manager data warehouse management server. Furthermore, don't use the management group name that is used for Operations Manager.  

    2. Select **Browse**, enter the user account or group to which you want to give Service Manager administrative rights, and select **Next**.  
9. Service Manager will use the existing computer if SQL Server Reporting Services is present. On the **Configure the reporting server for the data warehouse** page, accept the defaults, and select **Next**.  
10. On the **Configure the account for Service Manager services** page, select **Domain account**, specify the user name, password, and domain for the account, and select **Test Credentials**. After you receive a **The credentials were accepted** message, select **Next**.  
11. On the **Configure the reporting account** page, specify the user name, password, and domain for the account, and select **Test Credentials**. After you receive a **The credentials were accepted** message, select **Next**.  
12. On the **Diagnostic and usage data** page, indicate your preference for sharing your Service Manager diagnostic and usage data with Microsoft. As an option, select **Privacy statement for System Center Service Manager**, and select **Next**.  
13. On the **Use Microsoft Update to help keep your computer secure and up\-to\-date** page, indicate your preference for using Microsoft Update to check for Service Manager updates, and select **Next**.  
14. On the **Installation summary** page, select **Install**.  

## Validate a data warehouse management server installation  

1. On the computer hosting the data warehouse management server \(the server you ran Setup on\), run services.msc, and verify that the following services have been installed:  
    - System Center Data Access Service  
    - System Center Management  
    - System Center Management configuration  
2. On the computer hosting the data warehouse databases, select **Start**, point to **Programs**, point to **Microsoft SQL Server**, and select **SQL Server Management Studio**.  
3. In the **Connect to Server** dialog, select the following:  
    1. In the **Server Type** list, select **Database Engine**.  
    2. In the Server Name list, select the server and instance for your Service Manager data warehouse database. For example, select **Computer 4**.  
    3. In the **Authentication** list, select **Windows Authentication**, and select **Connect**.  
4. In the **Object Explorer** pane, expand **Databases**.  
5. Verify that the **DWDataMart**, **DWRepository**, and **DWStagingAndConfig** databases are listed.

## Register the data warehouse server in the lab environment

Use the following procedure to register the newly installed data warehouse server with the lab Service Manager environment.  

### Register a data warehouse  

1. Sign in to the computer that hosts the Service Manager console. Use an account that is a member of the Service Manager and data warehouse management administrators group.  
2. In the Service Manager console, select **Administration**.  
3. In the **Administration** pane, expand **Administration**.  
4. In the **Administration** view, in the **Register with Service Manager's Data Warehouse** area, select **Register with Service Manager Data Warehouse**.  
5. In the Data Warehouse Registration wizard, on the **Before You Begin** page, select **Next**.  
6. On the **Data Warehouse** page, in the **Server name** box, enter the fully qualified domain name of the computer hosting the data warehouse management server, and select **Test Connection**. If the test is successful, select **Next**.  
7. On the **Credentials** page, you can accept the default entry in the **Run as account** list, and select **Next**, or you can enter credentials from a user or group of your own choosing.  

   > [!IMPORTANT]  
   > The account you specify will be assigned administrative credentials on the Service Manager management server and granted Read permission on the Service Manager database. You can specify different credentials from other Service Manager management groups when registering with the data warehouse.  

8. On the **Summary** page, select **Create**.  
9. On the **Completion** page, when **The data warehouse registration succeeded** is displayed, select **Close**.  
10. A dialog states that the report deployment process hasn't finished. This is to be expected. On the **System Center Service Manager** dialog, select **OK**.  
11. In a few minutes, after closing the Data Warehouse Registration wizard, the **Data Warehouse** button will be added to the Service Manager console. In the Service Manager console, select the arrow at the lower right corner of the Service Manager console buttons, and select **Show More Buttons**.  

    You can use a Windows PowerShell command to complete this task. For information about how to use Windows PowerShell to register Service Manager management groups with the data warehouse, see [Add\-SCDWMgmtGroup](/previous-versions/system-center/service-manager-2010-sp1/ff951619(v=technet.10)).  

### Validate the registration

1. On the computer hosting the data warehouse management server, start Windows PowerShell with administrative credentials.  
2. At the Windows PowerShell command prompt, enter the following commands, and then press ENTER:  

    ```powershell
    Set-ExecutionPolicy RemoteSigned  
    Import-Module .\Microsoft.EnterpriseManagement.Warehouse.Cmdlets.psd1  
    ```  

3. Enter the following command, and then press ENTER.  

    ```powershell
    Get-SCDWMgmtGroup  

    ```  

4. If the registration is successful, a table with two rows of data is displayed. One row displays data for the data warehouse management group, and a second row displays data for the Service Manager management group. If the registration fails, only the data for the data warehouse management group is displayed.  

### Determine when the deployment is complete

 Because you need to allow enough time for the management pack deployment process to be completed, you'll have to determine when that process is complete. You can use the following procedure in Service Manager to determine when the process is complete.  

#### Determine when management pack deployment has completed  

1. Start the Service Manager console.  
2. In the Service Manager console, select **Data Warehouse**.  
3. In the **Data Warehouse** pane, expand **Data Warehouse**, and select **Data Warehouse Jobs**.  
4. In the **Data Warehouse Jobs** pane, select **MPSyncJob**.  
5. In the **Tasks** pane, under **Synchronization**, select **Details**.  
6. In the **MP Sync Job** dialog, scroll to the right and examine the **Status** column.  

    > [!NOTE]  
    > In the **MP Sync Job** dialog, select **Status** to alphabetically sort the status column.  

7. Scroll through the **Status** list. The management pack deployment process is complete when **Associated** or **Imported** is listed in the status column for all of the management packs. Ensure that there's no status of either **Pending Association** or **Failed** in the status list. In the **Data Warehouse Jobs** pane, the status of the **MPSyncJob** will have changed from **Running** to **Not Started**. This deployment process can take up to two hours to complete.  
8. To refresh the **MP Sync Job** dialog:  
    1. Press **OK** to close the dialog.  
    2. In the **Tasks** pane, in the **Data Warehouse Jobs** area, select **Refresh**.  
    3. In the **Data Warehouse Jobs** pane, select **MPSyncJobs**.  
    4. In the **Tasks** pane, under **Synchronization**, select **Details**.  
9. After the management packs have been deployed (as determined in step 7), ensure that the following five data warehouse jobs are displayed in the **Data Warehouse Jobs** pane:  

    - Extract\_\<Service Manager management group name\>  
    - Extract\_\<data warehouse management group name\>  
    - Load.Common  
    - Transform.Common  
    - MPSyncJob  

10. If these five data warehouse jobs aren't displayed, perform the following procedure:  
    1. In the **Data Warehouse Jobs** pane, select **MPSyncJob**.  
    2. In the **Tasks** pane, under **Synchronization**, select **Resume**.  
    3. Assess if management pack deployment has completed by returning to step 4 above.

## Next steps

[Run an upgrade](upgrade-environment.md)
