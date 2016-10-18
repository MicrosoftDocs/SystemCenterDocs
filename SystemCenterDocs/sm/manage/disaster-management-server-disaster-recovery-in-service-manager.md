---
title: Management Server Disaster Recovery in Service Manager
manager: cfreeman
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
ms.assetid: 6b874bbe-a28e-4f7b-9c54-833557fbf81c
---

# Management Server Disaster Recovery in Service Manager

>Applies To: System Center 2016 - Service Manager

This section describes how to recover a Service Manager management server or a data warehouse management server. If you installed additional Service Manager management servers, you have the option of promoting an additional Service Manager management server. Regardless of whether you encounter software or hardware failures of the Service Manager management server, your recovery process is based on restoring a computer that has the same computer name.  

 For either management server, your first step must be to restore the encryption key *before* you start the management server setup.  

## How to Restore the Service Manager Encryption Key

You can use the following procedure to restore the encryption keys before you run Setup.exe to restore a part of System Center 2016 - Service Manager.  

### To restore the encryption key  

1.  Log on to the computer that will host the Service Manager part that you are attempting to recover by using an account that is a member of the Administrators group. For example, log on to the computer that will host the Service Manager or data warehouse management servers.  

2.  In Windows Explorer, open the Tools\\SecureStorageBackup folder on the installation media.  

3.  Right\-click **SecureStorageBackup.exe** then click **Run as administrator** to start the Encryption Key Backup or Restore Wizard.  

    > [!NOTE]  
    >  In this release, the wizard contains references to "Operations Manager." This issue will be resolved in a future release.  

4.  On the **Introduction** page, click **Next**.  

5.  On the **Backup or Restore?** page, select **Restore the Encryption Key**, and then click **Next**.  

6.  On the **Provide a Location** page, type the path and file name for the encryption key. For example, if you want to specify the file name SMBackupkey.bin for the encryption key on the server MyServer in the Backup shared folder, type **\\\\MyServer\\Backup\\SMBackupkey.bin**, and then click **Next**.  

7.  On the **Provide a Password** page, type the password that you used to back up the encryption key in the **Password** box. In the **Confirm Password** box, reenter the same password, and then click **Next**.  

8.  After you receive the message, "Secure Storage Key Restore Complete," click **Finish**.

## How to Recover a Service Manager Management Server

You can use the following procedure to reinstall a management server in System Center 2016 - Service Manager.  

> [!NOTE]  
>  You must restore the encryption key before starting this procedure.  

### To recover a Service Manager management server  

1.  Log on to the computer that will host the new Service Manager management server using an account that has administrator rights.  

2.  On the Service Manager installation media, double\-click the **Setup.exe** file.  

3.  On the **Service Manager Setup Wizard** page, click **Service Manager management server**.  

4.  On the **Product registration** page, type the information in the text boxes. If applicable, click **I have read, understood, and agree with the terms of the license agreement**, and then click **Next**.  

5.  On the **Installation location** page, verify that sufficient free disk space is available, and then click **Next**. If necessary, click **Browse** to change the location in which you want to install the Service Manager management server.  

6.  On the **System check results** page, make sure that the prerequisite check passed or at least passed with warnings, and then click **Next**.  

7.  On the **Configure the Service Manager database** page, do the following:  

    1.  In **Database server**, type the name of the computer that is hosting the Service Manager database, and then press the TAB key.  

    2.  Select **Use an existing database**.  

    3.  Click the **Database** list, select the database name for the Service Manager database \(the default name is **ServiceManager**\), and then click **Next**.  

8.  On the **Configure the Service Manager management group**, wait until the **Management group name** and **Management group administrators** fields have been populated. Then, click **Next**.  

9. On the **Configure the account for Service Manager services** page, click **Domain account**; specify the user name, password, and domain for the account; and then click **Test Credentials**. Make sure that you receive the following message: "The credentials were accepted." and then click **Next**.  

10. On the **Help improve System Center** page, indicate your preference for participation in both the Customer Experience Improvement Program and Error Reporting. For more information, click **Tell me more about the program**, and then click **Next**.  

11. On the **Installation summary** page, click **Install**.  

12. On the **Setup completed successfully** page, click **Close**.


## How to Recover a Data Warehouse Management Server

You can use the following procedure to reinstall a data warehouse management server for System Center 2016 - Service Manager.  

> [!NOTE]  
>  You must restore the encryption key before starting this procedure.   

### To recover a data warehouse management server  

1.  Log on to the computer that will host the new data warehouse management server using an account that has administrator rights.  

2.  On the Service Manager installation media, double\-click the **Setup.exe** file.  

3.  On the **Service Manager Setup Wizard** page, click **Service Manager data warehouse management server**.  

4.  On the **Product registration** page, type the information in the boxes. If applicable, click **I have read, understood, and agree with the terms of the license agreement**, and then click **Next**.  

5.  On the **Installation location** page, verify that sufficient free disk space is available, and then click **Next**. If necessary, click **Browse** to change the location in which you want to install the Service Manager data warehouse management server.  

6.  On the **System check results** page, make sure that the prerequisite check passed or at least passed with warnings, and then click **Next**.  

7.  On the **Configure the data warehouse database** page, do the following:  

    1.  In the **Select a database to change its default properties** area, select **Staging and Configuration**.  

    2.  In **Database server**, type the name of the computer that is hosting data warehouse databases, and then press the TAB key.  

    3.  Select **Use an existing database**.  

    4.  Click the **Database** list, select the database name for the Staging and Configuration database \(the default name is **DWStagingAndConfig**\), and then click **Next**.  

8.  On the **Configure the data warehouse management group** page, wait until the **Management group name** and **Management group administrators** fields have been populated, and then click **Next**.  

9. On the **Configure the reporting server for the data warehouse** page, in the **Report server** text box, type the computer name of the computer that hosts SQL Server Reporting Services \(SSRS\), and then click **Next**.  

    > [!NOTE]  
    >  You must use the original URL for the Reporting Server.  

10. On the **Configure the account for Service Manager services** page, click **Domain account**; specify the user name, password, and domain for the account; and then click **Test Credentials**. Make sure that you receive the following message: "The credentials were accepted.", and then click **Next**.  

11. On the **Configure the reporting account** page, specify the user name, password, and domain for the account, and then click **Test Credentials**. After you receive a "The credentials were accepted" message, click **Next**.  

12. On the **Help improve System Center** page, indicate your preference for participation in both the Customer Experience Improvement Program and Error Reporting. For more information, click **Tell me more about the program**, and then click **Next**.  

13. On the **Use Microsoft Update to help keep your computer secure and up\-to\-date** page, indicate your preference for using Microsoft Update to check for Service Manager updates, and then click **Next**.  

14. On the **Installation summary** page, click **Install**.  

15. On the **Setup completed successfully** page, click **Close**.

## How to Promote a Service Manager Management Server

When you first ran Setup for Service Manager, you installed the initial Service Manager management server and you defined the management group for your installation. The initial management server handles all the workflows in your Service Manager environment. You can use additional Service Manager management servers to load\-balance Service Manager console connections. Also, you can promote one of the additional Service Manager management servers to take over the role of a failed initial Service Manager management server. For more information, see [Deploying Additional Service Manager Management Servers](../deploy/deploy-deploying-additional-service-manager-management-servers.md).

 You can use the following procedures to promote a secondary Service Manager management server.  

### To prepare the secondary management server  

1.  On the secondary management server, close the Service Manager console.  

2.  On the Windows desktop, click **Start**, and then click **Run**.  

3.  In the **Run** dialog box, in the **Open** text field, type **services.msc**, and then click **OK**.  

4.  In the **Services** window, in the **Services \(Local\)** pane, locate the following three services, and for each one click **Stop**:  

    -   System Center Data Access Service  

    -   Microsoft Monitoring Agent  

    -   System Center Management Configuration  

5.  Leave the **Services** window open.  

6.  Open Windows Explorer. Locate the folder \\Program Files\\Microsoft System Center 2016\\Service Manager.  

7.  In this folder, delete the Health Service State folder and all of its contents.  

### To define the computer name for the Service Manager database  

1.  On the Service Manager database, on the Windows desktop, click **Start**, point to **Programs**, point to **Microsoft SQL Server**, and then click **SQL Server Management Studio**.  

2.  In the **Connect to Database Engine** dialog box, do the following:  

    1.  In **Server name**, type the name of the server that hosts the Service Manager database.  

    2.  In **Authentication**, select **Windows Authentication**.  

    3.  Click **Connect**.  

3.  In the **Object Explorer** pane, expand **Databases**, and then click **ServiceManager**.  

4.  On the toolbar, click **New Query**.  

5.  In the **SQLQuery1.sql** pane \(the center pane\), type the following, where \<FQDN of your server\> is the fully qualified domain name \(FQDN\) of the management server that you are promoting:  

    ```  
    EXEC p_PromoteActiveWorkflowServer '<FQDN of your server>'  
    ```  

6.  On the toolbar, click **Execute**.  

7.  At the bottom of the **SQLQuery1.sql** pane \(the center pane\), confirm that the "Query executed successfully" message appears.  

8.  Exit Microsoft SQL&nbsp;Server Management Studio.  

### To restart the services on the secondary management server  

1.  On the secondary management server, on the Windows desktop, click **Start**, and then click **Run**.  

2.  In the **Run** dialog box, in **Open**, type **services.msc**, and then click **OK**.  

3.  In the **Services** window, in the **Services \(Local\)** pane, locate the following three services, and for each one click **Start**.  

    -   System Center Data Access Service  

    -   Microsoft Monitoring Agent  

    -   System Center Management Configuration  

 Your secondary management server is now the primary management server for the management group.
