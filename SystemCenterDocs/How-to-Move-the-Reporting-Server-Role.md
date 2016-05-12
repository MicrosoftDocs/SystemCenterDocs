---
title: How to Move the Reporting Server Role
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3155a9c2-85df-4a0b-8ac0-0c55c180290e
---
# How to Move the Reporting Server Role
You can move the System Center 2012 – Operations Manager Reporting server component to a new server, or reinstall the component on the original server.

During this move, Operations Manager stops storing data in the OperationsManagerDW database until you complete the Operations Manager reporting server reinstall.

Use the procedures in this topic to move the reporting server to a new server and verify the success of the move. You must back up any custom reports that were authored outside of Operations Manager 2007. For more information about this, see [Moving the Report Server Databases to Another Computer](http://go.microsoft.com/fwlink/p/?linkID=151513) in the SQL Server 2008 Books Online \(http:\/\/go.microsoft.com\/fwlink\/?LinkId\=151513\).

> [!NOTE]
> Ensure that you follow all steps precisely, as not doing so might result in data corruption.

### To move the Operations Manager reporting server

1.  Use Microsoft SQL Server Management Studio to create a full backup of the data warehouse database. The default name is OperationsManagerDW.

    For more information, see [Create a Full Database Backup \(SQL Server\)](http://go.microsoft.com/fwlink/p/?linkID=206259).

2.  On the current Operations Manager reporting server computer, uninstall the Operations Manager reporting server component as follows:

    1.  Click **Start**, click **Control Panel**, and then click **Add or Remove Programs** if you are using Windows Server 2003, or click **Programs and Features** if you are using Windows Server 2008.

    2.  In the **Add or Remove Programs** or **Programs and Features** dialog box, select **System Center 2012 \- Operations Manager**, and then click **Uninstall\/Change**.

    3.  In the **Operations Manager Setup** wizard, click **Remove a feature**.

    4.  In the **Select features to remove** page, select **Reporting server**, and then click **Uninstall**. Click **Close** when the wizard finishes.

3.  On the new SQL server, copy the backup file to a local drive or map a local drive to the folder that contains the backup file.

4.  Optionally, on the original server that hosts the operational database, delete the data warehouse database.

5.  On the new server, use Microsoft SQL Server Management Studio to restore the data warehouse database that you previously backed up.

    For more information, see [Restore a Database Backup \(SQL Server Management Studio\)](http://go.microsoft.com/fwlink/p/?linkID=245795).

6.  If you are reinstalling the Operations Manager reporting server component on the original server, you must remove any data that is left from the original installation by doing the following:

    1.  Copy the ResetSRS.exe tool from the SupportTools folder on the product CD to a local folder.

    2.  Open a command prompt window using the **Run as Administrator** option and run the tool as follows:

        ```
        ResetSRS.exe <SQL Server instance name>
        ```

    3.  Here, SQL Server instance name is the SQL Server instance that SQL Reporting Services is installed on, such as 'Instance1'. If SQL Server is using the default instance, enter MSSQLSERVER.

    4.  Open the Reporting Configuration Manager by clicking **Start**, pointing to **Programs**, pointing to **Microsoft SQL Server 2005** or **Microsoft SQL Server 2008**, pointing to **Configuration Tools**, and then clicking **Reporting Services Configuration**.

    5.  For SQL Reporting Services 2005, in the **Configure Report Server** page, check the status of the **Web Service Identity** item. If the status is not **Configured** \(green\), click that item, and then click **Apply**.

        Check the status of the rest of the items on that page. Configure any items that are designated with a red ‘X’, indicating an unhealthy configuration status.

7.  On the new Operations Manager reporting server computer, install the Operations Manager Reporting server component as follows:

    1.  On the **Configuration**, **SQL Server instance for reporting services** page, make sure the **SQL Server instance** refers to the restored database.

    2.  On the **Configuration**, **Configure Operation Manager accounts** page, be sure the **Data Reader** account is the same account previously used for the Report server.

    For more information, see [How to Install the Operations Manager Reporting Server](assetId:///15404d1e-ad4b-4734-997c-c4992aba31ad).

Verify that you can successfully run a report from the Operations console.

Ensure that the health state of all **Management servers** is **Healthy**.


