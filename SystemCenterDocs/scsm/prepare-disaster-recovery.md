---
title: Prepare for disaster recovery
description: This article describes the steps that you must take for Service Manager disaster recovery before problems occur.
manager: carmonm
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e481f3b8-4074-4b51-9faa-93e35f4ffe68
---

# Prepare for Service Manager disaster recovery

>Applies To: System Center 2016 - Service Manager

This article describes the steps that you must take for Service Manager disaster recovery before problems occur. The steps that you take to recover from a disaster are based on completion of the steps that are outlined here. In general, preparing your Service Manager environment for disaster recovery involves the following:  

1.  Deploying Service Manager with management servers and databases on separate computers.  
2.  Backing up the encryption keys on the Service Manager and data warehouse management servers.  
3.  Backing up the SQL databases.  
4.  Backing up your unsealed management packs.  

## Deployment strategy for disaster recovery

As a best practice, deploy your management servers and associated databases for Service Manager on separate computers. Isolating the management servers and databases provides for a successful disaster recovery operation in the event of potential software and equipment failures.  

 You must have a functioning database to restore a failed management server. Recovery of a management server is impossible if the management server and the associated database are on the same physical computer and that computer fails. For more information, see [Installing Service Manager on Four Computers](install-four-computers.md).

## Back up Service Manager management servers

When you deploy Service Manager, an encryption key is created and stored in the registry on the management servers. A matching encryption key is created in the associated databases. The encryption keys for the Service Manager and data warehouse management servers are stored in the Service Manager database. The matching encryption key for the data warehouse management server is stored in the DWStagingAndConfig database. By backing up the SQL&nbsp;Server databases, you back up the encryption key.  

 In addition, the computer name of the management server and Self-Service Portal is stored in the associated databases. Regardless of whether you encounter a software or hardware failure of a management server or Self-Service Portal, your recovery process is based on restoring a computer that has the same computer name as the computer that failed.  

 The steps for recovering from a management server failure are as follows:  

1.  Restore the encryption keys before you run Setup, and install the new management servers.  
2.  Install the new management server on a computer that has the same name as the original computer.  
3.  When you install the management server, select **Use an existing database**, and then specify the name of the computer that hosts the associated database.  

 For more information about these steps, see [Implement Service Manager disaster recovery](implement-disaster-recovery.md).  

## Back up the Service Manager encryption key

Your disaster recovery strategy for Service Manager depends on backing up the encryption keys as soon as you complete the Service Manager installation. After you back up the encryption keys and store them in a safe location, you can recover from software or hardware failures on the Service Manager and data warehouse management servers.  

You use the Encryption Key Backup or Restore Wizard to back up encryption keys on the management servers and Self-Service Portal. This wizard is located on the Service Manager installation media in the Tools\\SecureStorageBackup folder.  

### To back up the encryption key  

1.  Log on to the computer that hosts the Service Manager management server of data warehouse management server by using an account that is a member of the Administrators group.  
2.  In Windows Explorer, open the Tools\\SecureStorageBackup folder on the installation media.  
3.  Right\-click **SecureStorageBackup.exe** then click **Run as administrator** to start the Encryption Key Backup or Restore Wizard.  
4.  On the **Introduction** page, click **Next**.  
5.  On the **Backup or Restore?** page, select **Backup the Encryption Key**, and then click **Next**.  
6.  On the **Provide a Location** page, type the path and file name for the encryption key. For example, if you want to specify the file name SMBackupkey.bin for the encryption key on the MyServer server in the Backup shared folder, type **\\\\MyServer\\Backup\\SMBackupkey.bin**, and then click **Next**.  
7.  On the **Provide a Password** page, in the **Password** box type a password that contains at least eight characters. In the **Confirm Password** box, retype the same password, and then click **Next**.  
    > [!IMPORTANT]  
    >  Recovery of the password is not possible if the password is lost or forgotten.  

8.  After you see the message "Secure Storage Backup Complete," click **Finish**.

## Back up System Center 2016 - Service Manager databases

There are up to eight databases in a System Center 2016 - Service Manager environment:  

-   ServiceManager  
-   DWDataMart  
-   DWRepository  
-   DWStagingAndConfig  
-   ReportServer  
-   Analyst  
-   OMDWDataMart  
-   CMDWDataMart  

The first four databases in this list need to connect and exchange data with the Service Manager and data warehouse management servers. Data is encrypted during these exchanges. On the management servers, the encryption keys are backed up and restored as necessary, as explained in this article. For the servers that host databases, the encryption keys are stored in the databases themselves.  

If a computer that hosts a database fails, all you need for recovery is the ability to restore the databases, which include the encryption keys, to a computer with the same name as the original computer. Your disaster recovery strategy for the Service Manager databases should be based on procedures for general SQL&nbsp;Server disaster recovery. For more information, see [Planning for Disaster Recovery](http://go.microsoft.com/fwlink/p/?LinkID=131016).  

As part of your disaster recovery preparation, you run a script to capture the Security log to preserve user role information for each database. After you deploy Service Manager and, if necessary, run the Data Warehouse Registration Wizard, you use the SQL&nbsp;Server Script Wizard to create a script that captures SQL&nbsp;Server logon permissions and object\-level permissions. Then, if you need to restore a new server for the Service Manager databases, you can use this script to recreate the necessary logon permissions and object\-level permissions.  

### Enable common language runtime on SQL&nbsp;Server  

During installation of the Service Manager database, Service Manager Setup enables common language runtime \(CLR\) on the computer that is running SQL&nbsp;Server. If you restore a Service Manager database to another computer running SQL&nbsp;Server, you must enable CLR manually. For more information, see [Enabling CLR Integration](http://go.microsoft.com/fwlink/p/?LinkId=217932).  

### Start the SQL Server Script wizard

You can use the following procedure as part of your disaster recovery preparation steps for Service Manager to generate a script to capture SQL&nbsp;Server logon permissions and object\-level permissions. You perform this procedure on the computer that hosts SQL&nbsp;Server Reporting Services \(SSRS\) and on the computers that host the following Service Manager and data warehouse databases:  

-   DWDataMart  
-   DWRepository  
-   DWStagingAndConfig  
-   ServiceManager  
-   ReportServer  

#### To start the SQL&nbsp;Server Script wizard  

1.  Using an account with Administrator privileges, log on to the computer that hosts the Service Manager or data warehouse database.  
2.  On the Windows desktop, click **Start**, point to **Programs**, point to **Microsoft&nbsp;SQL&nbsp;Server&nbsp;2008&nbsp;R2**, and then click **SQL&nbsp;Server Management Studio**.  
3.  In the **Connect to Server** dialog box, do the following:  
    1.  In the **Server Type** list, select **Database Engine**.  
    2.  In the **Server Name** list, select the server and the instance for your Service Manager database. For example, select **computer\\INSTANCE1**.  
    3.  In the **Authentication** list, select **Windows Authentication**, and then click **Connect**.  
4.  In the **Object Explorer** pane, expand **Databases**.  
5.  Right\-click the database name, point to **Tasks**, and then click **Generate Scripts**. For this example, right\-click **ServiceManager**, point to **Tasks**, and then click **Generate Scripts**.  
6.  In the Generate and Publish Scripts Wizard, do the following:  
    1.  On the **Introduction** page, click **Next**.  
    2.  On the **Choose Objects** page, select **Select specific database objects**, and then click **Select All**.  
    3.  In the database objects list, expand **Tables**.  
    4.  Clear the check box for the following tables:  
        -   **dbo.STG\_Collation**  
        -   **dbo.STG\_Locale**  
        -   **dbo.STG\_MTD\_ConverisonLog**  
    5.  Scroll up to the top of the list, and then collapse **Tables**.  
    6.  Expand **Stored Procedures**.  
    7.  Clear the check box for the following stored procedures:  
        -   **dbo.STG\_DTS\_ConvertToUnicode**  
        -   **dbo.STG\_DTS\_CreateClonedTable**  
        -   **dbo.STG\_DTS\_InsertSQL**  
        -   **dbo.STG\_DTS\_ValidateConversion**  
    8.  Click **Next**.  
    9. On the **Set Scripting Options** page, select **Save scripts**, select **Save to file**, select **Single file**, specify a file location in **File name**, and then click **Next**.  
    10. On the **Summary** page, click **Next**.  
    11. When the script is complete, on the **Save or Publish Scripts** page, click **Finish**.  
7.  If you need to restore a database, use this script to set permissions.

## Back up unsealed management packs

Part of the disaster recovery plan for your Service Manager management server involves backing up your unsealed management packs. The following procedure describes how to back up your unsealed management packs.  

### Back up unsealed management packs

You can use the Windows&nbsp;PowerShell command\-line interface to identify and copy your unsealed management packs to a folder on your hard disk drive. After you copy them, save these management packs so that-as part of your disaster recovery plan for Service Manager-you can later import these management packs.  

#### To back up unsealed management packs  

1.  On the computer that hosts the Service Manager management server, create a folder on the hard disk drive where you will store the backup copy of the management packs. For example, create the folder C:\\mpbackup.  
2.  On the Windows desktop, click **Start**, point to **Programs**, point to **Windows&nbsp;PowerShell&nbsp;1.0**, right\-click **Windows&nbsp;PowerShell**, and then click **Run as administrator**.  
3.  In the Service Manager console, click **Administration**.  
4.  In the **Tasks** pane, click **Start PowerShell Session**  
5.  At the Windows&nbsp;PowerShell command prompt, type the following command:  

    ```  
    Get-SCSMManagementPack | where {$_.Sealed -eq $false}|Export-SCSMManagementPack -Path c:\mpbackup  
    ```  

6.  Save the unsealed management packs on a separate physical computer.
