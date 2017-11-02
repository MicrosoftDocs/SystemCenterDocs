---
title: Create a production environment for upgrade
description: To prepare for upgrade, create a production environment and prepare it for production data.
manager: carmonm
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 05/30/2017
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
---

# Set up a Service Manager 2016 production environment to prepare it for upgrade

>Applies To: System Center 2016 - Service Manager

Use the following procedures to prepare for Service Manager upgrade by creating a production environment and preparing it for production data.

## Install an additional management server in the production Service Manager management group

The following procedure shows how to install an additional management server. You must deploy the initial Service Manager management server and Service Manager Database before deploying an additional management server.  

> [!TIP]  
>  You must be a member of the Service Manager Administrators user role in order to install an additional Service Manager management server.  

When you install a secondary management server, data retention settings are reset. Before you install a secondary management server, make a note of data retention settings. After you have installed the additional management server, adjust the data retention settings to their original values.  

### Run Setup

1.  By using an account that has administrator rights and that is also a member of the Service Manager Management group administrators, log on to the computer that will host the additional Service Manager Management server.  
2.  On the System Center 2016 - Service Manager installation media, double\-click Setup.exe.  
3.  On the **Microsoft System Center 2016 Service Manager** page, click **Install a Service Manager Management server**.  
4.  On the **Product registration** page, type information in the boxes. In the **Product key** boxes, type the product key you received with Service Manager, or alternatively, select **Install as an evaluation edition \(180 day trial\)?**. Read the Microsoft Software License Terms, and, if applicable, click **I have read, understood, and agree with the terms of the license agreement**, and then click **Next**.  
5.  On the **Installation location** page, verify that sufficient free disk space is available, and then click **Next**. If necessary, click **Browse** to change the location where the additional Service Manager Management server will be installed.  
6.  On the **System check results** page, make sure that the prerequisite check passed or at least passed with warnings, and then click **Next**.  
    - If the prerequisite checker determines that the Microsoft Report Viewer Redistributable has not been installed, click **Install Microsoft Report Viewer Redistributable**. After the **Microsoft Report Viewer Redistributable 2008 \(KB971119\) Setup** wizard completes, click **Check perquisites again**.  
7.  On the **Configure the Service Manager Database** page, in the **Database server** box, type the name of the computer that hosts the Service Manager database that you used for your initial Service Manager Management server, and then press TAB. When the name of the instance displays in the **SQL Server instance** box, click **Use an existing database**. For example, type **Computer 2** in the **Database server** box.  
8.  Click the **Database** list, select the database name for the Service Manager database \(the default name is ServiceManager\), and then click **Next**.  
9. On the **Configure the Service Manager Management group** page, verify that the management group name and management group administrators boxes have been populated. Click **Next**.  
10. On the **Configure the Account for Service Manager Services** page, click **Domain account**, specify the user name, password, and domain for the account, and then click **Test Credentials**. After you receive a **The credentials were accepted** message, click **Next**. For example, enter the account information for the domain user SM\_Acct, and then click **Next**.  

    > [!NOTE]  
    >  The user name and password you provide here must be the same ones used for the Service Manager account on the data warehouse management server.  

11. On the **Diagnostic and usage data** page, indicate your preference for sharing your Service Manager diagnostic and usage data with Microsoft. As an option, click **Privacy statement for System Center Service Manager**, and then click **Next**.
12. On the **Use Microsoft Update to help keep your computer secure and up\-to\-date** page, indicate your preference for using Microsoft Update to check for Service Manager updates, and then click **Next**.  
13. On the **Installation summary** page, click **Install**.  
14. On the **Setup completed successfully** page, we recommend that you leave **Open the Encryption Backup or Restore Wizard** selected, and then click **Close**.

## Copy customized workflow assembly files

Use the following procedure to copy the workflow assembly files from the Service Manager Installation folder on the primary management server to the secondary management server that you created in the previous procedure.  

### To copy the workflow assembly files  

1.  On the computer that is running the Service Manager Primary Server role, browse to the Service Manager Installation folder for example, C:\\Program Files\\Microsoft System Center\\Service Manager copy the workflow files (workflow.dll).  
2.  On the computer that is running the Service Manager Secondary server; browse to the Service Manager Installation folder; for example, C:\\Program Files\\Microsoft System Center\\Service Manager. Paste the copied workflow files into this folder. You should overwrite any existing files.  

    > [!NOTE]  
    >  You must place the workflow assembly files in the Service Manager installation folder. This is very important step if you want to test the custom workflows that depend on workflow assembly files. Failure to copy these files would lead to failed custom workflows in the lab environment.


## Disable Service Manager connectors in the production environment


Use the following procedure to disable the Service Manager connectors in the production environment.  

1.  In the Service Manager console, click **Administration**.  
2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.  
3.  In the **Connectors** pane, select the connector that you want to disable.  
4.  In the **Tasks** pane, under the connector name, click **Disable**.  
5.  In the **Disable Connector** dialog box, click **OK**.

## Disable email notifications in the production environment

Use the following procedure to disable incoming and outbound E\-mail notifications in the production environment.  

### Disable outbound email notifications  

1.  In the Service Manager console, click **Administration**.  
2.  In the **Administration** pane, expand **Notifications**, and then click **Channels**.  
3.  In the **Channels** pane, click **E\-Mail Notification Channel**.  
4.  In the **Tasks** pane, under **E\-Mail Notification Channel**, click **Properties** to open the **Configure E\-Mail Notification Channel** dialog box.  
5.  Clear the **Enable e\-mail notifications** check box.  

### Disable incoming email notifications  

1.  In the Service Manager console, select **Administration**.  
2.  In the **Administration** pane, expand **Administration**, and then click **Settings**.  
3.  In the **Settings** pane, double\-click **Incident Settings**.  
4.  In the Incident **Settings** dialog box, click **Incoming E\-mail**.  
5.  Clear **Turn on incoming e\-mails processing**, and then click **OK**.

## Stop Service Manager services on the secondary management server

Use the following procedure to stop the Service Manager services.  

### To stop the Service Manager services  

1.  In the **Run** dialog box, in the **Open** text field, type **services.msc**, and then click **OK**.  
2.  In the **Services** window, in the **Services \(Local\)** pane, locate the following three services and for each one, click **Stop**:  
    1.  System Center Data Access Service  
    2.  System Center Management  
    3.  System Center Management Configuration  
3.  Open Windows Explorer.  
4.  Locate the folder \\Program Files\\Microsoft System Center\\Service Manager.  
5.  Delete the **Health Service State** folder and all of its contents.

## Back up the production Service Manager database for future recovery

Use the following procedure to back up the production Service Manager database in Microsoft SQL Server 2016.

### To back up the Service Manager database

1. After connecting to the appropriate instance of the Microsoft SQL Server Database Engine, in Object Explorer, click the server name to expand the server tree.
2. Expand **Databases**, and depending on the database, either select a user database or expand **System Databases** and select a system database.
3. Right-click the database, point to **Tasks**, and then click **Back Up**. The Back Up Database dialog box appears.
4. In the **Database** list box, verify the database name. You can optionally select a different database from the list.
5. You can perform a database backup for any recovery model (FULL, BULK_LOGGED, or SIMPLE).
6. In the **Backup type** list box, select **Full**.

    > [!NOTE]
    > After creating a full database backup, you can create a differential database backup. For more information, see [How to: Create a Differential Database Backup (SQL Server Management Studio)](https://go.microsoft.com/fwlink/p/?LinkId=134470).

7. Optionally, you can select **Copy Only Backup** to create a copy-only backup. A copy-only backup is a SQL Server backup that is independent of the sequence of conventional SQL Server backups. For more information, see [Copy-Only Backups](https://go.microsoft.com/fwlink/p/?LinkId=236002).

    > [!NOTE]
    > When the **Differential** option is selected, you cannot create a copy-only backup.

8. For **Backup component**, click **Database**.
9. Either accept the default backup set name suggested in the **Name** text box, or enter a different name for the backup set.
10. Optionally, in the **Description** text box, enter a description of the backup set.
11. Specify when the backup set will expire and can be overwritten without explicitly skipping verification of the expiration data.

    > [!NOTE]
    > For more information about backup expiration dates, see [BACKUP (Transact-SQL)](https://go.microsoft.com/fwlink/p/?LinkId=134324).

12. Choose the type of backup destination by clicking **Disk** or **Tape**. To select the paths of up to 64 disk or tape drives containing a single media set, click **Add**. The selected paths are displayed in the **Backup to** list box.
13. To view or select the advanced options, click **Options** in the **Select a page** pane.
14. Select an Overwrite Media option, by clicking either **Back up to the existing media set** or **Back up to a new media set, and erase all existing backup sets**.
15. In the Reliability section, select either **Verify backup when finished** or **Perform checksum before writing to media**, and then optionally select **Continue on checksum error**. For more information, see [Detecting and Coping with Media Errors During Backup and Restore](https://go.microsoft.com/fwlink/p/?LinkId=236004)

## Enable Service Manager connectors in the production environment

Use the following procedure to enable the Service Manager connectors in the production environment.  

### Enable a connector  

1.  In the Service Manager console, click **Administration**.  
2.  In the **Administration** pane, expand **Administration**, and then click **Connectors**.  
3.  In the **Connectors** pane, select the connector that you want to enable.  
4.  In the **Tasks** pane, under the connector name, click **Enable**.


## Enable email notifications in the production environment

Use the following procedure to enable incoming and outbound email notifications in the production environment.  

### Enable outbound email notifications  

1.  In the Service Manager console, click **Administration**.  
2.  In the **Administration** pane, expand **Notifications**, and then click **Channels**.  
3.  In the **Channels** pane, click **E\-Mail Notification Channel**.  
4.  In the **Tasks** pane, under **E\-Mail Notification Channel**, click **Properties** to open the **Configure E\-Mail Notification Channel** dialog box.  
5.  Select **Enable e\-mail notifications**.  

### Enable incoming email notifications  

1.  In the Service Manager console, select **Administration**.  
2.  In the **Administration** pane, expand **Administration**, and then click **Settings**.  
3.  In the **Settings** pane, double\-click **Incident Settings**.  
4.  In the Incident **Settings** dialog box, click **Incoming E\-mail**.  
5.  Select **Turn on incoming e\-mails processing**, and then click **OK**.

## Next steps

- [Prepare the lab environment](lab-env.md)
