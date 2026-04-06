---
title: Implement Disaster Recovery
description: Describes the steps needed to recover from potential software and equipment failures in your Service Manager environment.
ms.service: system-center
ms.date: 04/09/2025
author: Jeronika-MS
ms.author: v-gajeronika
ms.update-cycle: 1095-days
ms.subservice: service-manager
ms.topic: how-to
ms.custom: UpdateFrequency3, engagement-fy24
---

# Implement Service Manager disaster recovery



This article describes the steps needed to recover from potential software and equipment failures in your System Center - Service Manager environment. It includes information about how to recover Service Manager databases, management servers, and unsealed management packs.  

## Restore a database

To restore a database \(which includes the encryption keys\) for Service Manager, you rebuild a new computer using the same computer names and instance names as the original. Your disaster recovery strategy for the Service Manager databases should be based on general procedures for SQL&nbsp;Server disaster recovery. For more information, see [Plan for Disaster Recovery](/previous-versions/sql/sql-server-2008-r2/ms178094(v=sql.105)). Remember that if you restore a database, you must give the new computer the same name as the original computer and use the same instance name as the original instance.  

In addition, you must use the script that you created in the [Back Up Unsealed Management Packs in Service Manager](./prepare-disaster-recovery.md) article in this guide. You use this script to restore permissions for the recreated database.  

> [!WARNING]  
> Long\-term historical data is stored in the Service Manager data warehouse and the current snapshot of the system is stored in the Service Manager database. Recreating the Service Manager data warehouse databases should only be used as a measure of last resort. When possible, you should try to restore the Service Manager data warehouse databases from backups and avoid recreating those databases. If reinstalled, the newly created Service Manager data warehouse databases will be able to synchronize the current snapshot of the system from the Service Manager database-however, historical data will be lost.

## Recover a management server

This section describes how to recover a Service Manager management server or a data warehouse management server. If you installed additional Service Manager management servers, you've the option of promoting an additional Service Manager management server. Regardless of whether you encounter software or hardware failures of the Service Manager management server, your recovery process is based on restoring a computer that has the same computer name.  

For either management server, your first step must be to restore the encryption key *before* you start the management server setup.  

### Restore the Service Manager encryption key

You can use the following procedure to restore the encryption keys before you run Setup.exe to restore a part of Service Manager.  

To restore the encryption key, follow these steps:

1. Sign in to the computer that will host the Service Manager part that you're attempting to recover by using an account that is a member of the Administrators group. For example, sign in to the computer that will host the Service Manager or data warehouse management servers.  
2. In Windows Explorer, open the Tools\\SecureStorageBackup folder on the installation media.  
3. Right-click **SecureStorageBackup.exe** and select **Run as administrator** to start the Encryption Key Backup or Restore Wizard.  
    > [!NOTE]  
    > In this release, the wizard contains references to **Operations Manager**. This issue will be resolved in a future release.  

4. On the **Introduction** page, select **Next**.  
5. On the **Backup or Restore?** page, select **Restore the Encryption Key**, and select **Next**.  
6. On the **Provide a Location** page, enter the path and file name for the encryption key. For example, if you want to specify the file name SMBackupkey.bin for the encryption key on the server MyServer in the Backup shared folder, enter **\\\\MyServer\\Backup\\SMBackupkey.bin**, and select **Next**.  
7. On the **Provide a Password** page, enter the password that you used to back up the encryption key in the **Password** box. In the **Confirm Password** box, reenter the same password, and select **Next**.  
8. After you receive the message **Secure Storage Key Restore Complete**, select **Finish**.

### Restore the server

> [!NOTE]  
> You must restore the encryption key before starting this procedure.  

To restore a Service Manager management server, follow these steps:

1. Sign in to the computer that will host the new Service Manager management server using an account that has administrator rights.  
2. On the Service Manager installation media, double\-click the **Setup.exe** file.  
3. On the **Service Manager Setup Wizard** page, select **Service Manager management server**.  
4. On the **Product registration** page, enter the information in the text boxes. If applicable, select **I have read, understood, and agree with the terms of the license agreement**, and select **Next**.  
5. On the **Installation location** page, verify that sufficient free disk space is available, and select **Next**. If necessary, select **Browse** to change the location in which you want to install the Service Manager management server.  
6. On the **System check results** page, ensure that the prerequisite check passed or at least passed with warnings, and select **Next**.  
7. On the **Configure the Service Manager database** page, do the following:  
    1. In **Database server**, enter the name of the computer that is hosting the Service Manager database, and then press the TAB key.  
    2. Select **Use an existing database**.  
    3. Select the **Database** list, select the database name for the Service Manager database \(the default name is **ServiceManager**\), and select **Next**.  
8. On the **Configure the Service Manager management group**, wait until the **Management group name** and **Management group administrators** fields have been populated. Then select **Next**.  
9. On the **Configure the account for Service Manager services** page, select **Domain account**; specify the user name, password, and domain for the account; and select **Test Credentials**. Ensure that you receive the following message: **The credentials were accepted**, and select **Next**.  
10. On the **Help improve System Center** page, indicate your preference for participation in both the Customer Experience Improvement Program and Error Reporting. For more information, select **Tell me more about the program**, and select **Next**.  
11. On the **Installation summary** page, select **Install**.  
12. On the **Setup completed successfully** page, select **Close**.

## Recover a data warehouse management server

You can use the following procedure to reinstall a data warehouse management server for Service Manager.  

> [!NOTE]  
> You must restore the encryption key before starting this procedure.

To recover a data warehouse management server, follow these steps:

1. Sign in to the computer that will host the new data warehouse management server using an account that has administrator rights.  
2. On the Service Manager installation media, double\-click the **Setup.exe** file.  
3. On the **Service Manager Setup Wizard** page, select **Service Manager data warehouse management server**.  
4. On the **Product registration** page, enter the information in the boxes. If applicable, select **I have read, understood, and agree with the terms of the license agreement**, and select **Next**.  
5. On the **Installation location** page, verify that sufficient free disk space is available, and select **Next**. If necessary, select **Browse** to change the location in which you want to install the Service Manager data warehouse management server.  
6. On the **System check results** page, ensure that the prerequisite check passed or at least passed with warnings, and select **Next**.  
7. On the **Configure the data warehouse database** page, do the following:  
    1. In the **Select a database to change its default properties** area, select **Staging and Configuration**.  
    2. In **Database server**, enter the name of the computer that is hosting data warehouse databases, and then press the TAB key.  
    3. Select **Use an existing database**.  
    4. Select the **Database** list, select the database name for the Staging and Configuration database \(the default name is **DWStagingAndConfig**\), and select **Next**.  
8. On the **Configure the data warehouse management group** page, wait until the **Management group name** and **Management group administrators** fields have been populated, and select **Next**.  
9. On the **Configure the reporting server for the data warehouse** page, in the **Report server** text box, enter the computer name of the computer that hosts SQL Server Reporting Services \(SSRS\), and select **Next**.  
    > [!NOTE]  
    > You must use the original URL for the Reporting Server.  

10. On the **Configure the account for Service Manager services** page, select **Domain account**; specify the user name, password, and domain for the account; and select **Test Credentials**. Ensure that you receive the following message: **The credentials were accepted**, and select **Next**.  
11. On the **Configure the reporting account** page, specify the user name, password, and domain for the account, and select **Test Credentials**. After you receive a **The credentials were accepted** message, select **Next**.  
12. On the **Help improve System Center** page, indicate your preference for participation in both the Customer Experience Improvement Program and Error Reporting. For more information, select **Tell me more about the program**, and select **Next**.  
13. On the **Use Microsoft Update to help keep your computer secure and up\-to\-date** page, indicate your preference for using Microsoft Update to check for Service Manager updates, and select **Next**.  
14. On the **Installation summary** page, select **Install**.  
15. On the **Setup completed successfully** page, select **Close**.

### Promote a Service Manager management server

When you first ran Setup for Service Manager, you installed the initial Service Manager management server and you defined the management group for your installation. The initial management server handles all the workflows in your Service Manager environment. You can use additional Service Manager management servers to load\-balance Service Manager console connections. Also, you can promote one of the additional Service Manager management servers to take over the role of a failed initial Service Manager management server. For more information, see [Deploy Additional Service Manager Management Servers](deploy-additional-ms.md).

You can use the following procedures to promote a secondary Service Manager management server.  

#### Prepare the secondary management server

To prepare the secondary management server, follow these steps:

1. On the secondary management server, close the Service Manager console.  
2. On the Windows desktop, select **Start**, and select **Run**.  
3. In the **Run** dialog, in the **Open** text field, enter **services.msc**, and select **OK**.  
4. In the **Services** window, in the **Services \(Local\)** pane, locate the following three services, and for each one select **Stop**:  
    - System Center Data Access Service  
    - Microsoft Monitoring Agent  
    - System Center Management Configuration  
5. Leave the **Services** window open.  
6. Open Windows Explorer. Locate the folder \\Program Files\\Microsoft System Center \<version\>\\Service Manager.  
7. In this folder, delete the Health Service State folder and all of its contents.  

#### Define the computer name for the Service Manager database

To define the computer name for the Service Manager database, follow these steps:

1. On the Service Manager database, on the Windows desktop, select **Start**, point to **Programs**, point to **Microsoft SQL Server**, and select **SQL Server Management Studio**.  
2. In the **Connect to Database Engine** dialog, do the following:  
    1. In **Server name**, enter the name of the server that hosts the Service Manager database.  
    2. In **Authentication**, select **Windows Authentication**.  
    3. Select **Connect**.  
3. In the **Object Explorer** pane, expand **Databases**, and select **ServiceManager**.  
4. On the toolbar, select **New Query**.  
5. In the **SQLQuery1.sql** pane \(the center pane\), type the following, where \<FQDN of your server\> is the fully qualified domain name \(FQDN\) of the management server that you're promoting:  

    ```  
    EXEC p_PromoteActiveWorkflowServer '<FQDN of your server>'  
    ```  

6. On the toolbar, select **Execute**.  
7. At the bottom of the **SQLQuery1.sql** pane \(the center pane\), confirm that the "Query executed successfully" message appears.  
8. Exit Microsoft SQL&nbsp;Server Management Studio.  

#### Restart the services on the secondary management server

To restart the services on the secondary management server, follow these steps:

1. On the secondary management server, on the Windows desktop, select **Start**, and select **Run**.  
2. In the **Run** dialog, in **Open**, enter **services.msc**, and select **OK**.  
3. In the **Services** window, in the **Services \(Local\)** pane, locate the following three services, and for each one select **Start**.  
    - System Center Data Access Service  
    - Microsoft Monitoring Agent  
    - System Center Management Configuration  

Your secondary management server is now the primary management server for the management group.

## Import Service Manager unsealed management packs

After you've restored your Service Manager management server, the next step is to import unsealed management packs.  

### Import management packs

You can use this procedure to import the unsealed management packs that you saved earlier as part of your disaster recovery procedures for Service Manager.  

To import management packs, follow these steps:

1. In the Service Manager console, select **Administration**.  
2. In the **Administration** pane, expand **Administration**, and select **Management Packs**.  
3. In the **Tasks** pane, under **Management Packs**, select **Import**.  
4. In the **Select Management Packs to Import** window, under **Favorite Links**, specify the location where you backed up your unsealed management packs, select the files, and select **Open**.  
5. In the **Import Management Pack** window, select **Import**.
