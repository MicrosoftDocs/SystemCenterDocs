---
title: Create a production environment for System Center - Service Manager upgrade
description: Learn about create a production environment to test System Center - Service Manager upgrade.
ms.service: system-center
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.subservice: service-manager
ms.update-cycle: 1095-days
ms.topic: upgrade-and-migration-article
ms.custom: UpdateFrequency2, engagement-fy23, engagement-fy24
---

# Prepare a production environment for upgrade

Use the following procedures to prepare for System Center - Service Manager upgrade by creating a production environment and preparing it for production data for the purpose of upgrade testing.

## Install an additional management server

The following procedure shows how to install an additional management server. You must deploy the initial Service Manager management server and Service Manager Database before deploying an additional management server.  

> [!TIP]  
> You must be a member of the Service Manager Administrators user role in order to install an additional Service Manager management server.  

When you install a secondary management server, data retention settings are reset. Before you install a secondary management server, make a note of the data retention settings. After you've installed the additional management server, adjust the data retention settings to their original values.  

### Run setup

Follow these steps to run setup:

1. By using an account that has administrator rights and that is also a member of the Service Manager Management group administrators, sign in to the computer that will host the additional Service Manager Management server.  
2. On the System Center - Service Manager installation media, double-click Setup.exe.  
3. On the **Microsoft System Center \<version\> Service Manager** page, select **Install a Service Manager Management server**.  
4. On the **Product registration** page, enter the information in the boxes. In the **Product key** boxes, enter the product key you received with Service Manager, or alternatively, select **Install as an evaluation edition (180 day trial)?**. Read the Microsoft Software License Terms, and, if applicable, select **I have read, understood, and agree with the terms of the license agreement**, and select **Next**.  
5. On the **Installation location** page, verify that sufficient free disk space is available, and select **Next**. If necessary, select **Browse** to change the location where the additional Service Manager Management server will be installed.  
6. On the **System check results** page, ensure that the prerequisite check passed or at least passed with warnings, and select **Next**.  
    - If the prerequisite checker determines that the Microsoft Report Viewer Redistributable hasn't been installed, select **Install Microsoft Report Viewer Redistributable**. After the **Microsoft Report Viewer Redistributable 2008 (KB971119) Setup** wizard completes, select **Check perquisites again**.  
7. On the **Configure the Service Manager Database** page, in the **Database server** box, enter the name of the computer that hosts the Service Manager database that you used for your initial Service Manager Management server, and then press TAB. When the name of the instance displays in the **SQL Server instance** box, select **Use an existing database**. For example, enter **Computer 2** in the **Database server** box.  
8. Select the **Database** list, select the database name for the Service Manager database (the default name is ServiceManager), and select **Next**.  
9. On the **Configure the Service Manager Management group** page, verify that the management group name and management group administrators boxes have been populated. Select **Next**.  
10. On the **Configure the Account for Service Manager Services** page, select **Domain account**, specify the user name, password, and domain for the account, and select **Test Credentials**. After you receive a **The credentials were accepted** message, select **Next**. For example, enter the account information for the domain user SM_Acct, and select **Next**.  

    > [!NOTE]  
    > The user name and password you provide here must be the same ones used for the Service Manager account on the data warehouse management server.  

11. On the **Diagnostic and usage data** page, indicate your preference for sharing your Service Manager diagnostic and usage data with Microsoft. As an option, select **Privacy statement for System Center Service Manager**, and select **Next**.
12. On the **Use Microsoft Update to help keep your computer secure and up-to-date** page, indicate your preference for using Microsoft Update to check for Service Manager updates, and select **Next**.  
13. On the **Installation summary** page, select **Install**.  
14. On the **Setup completed successfully** page, we recommend that you leave **Open the Encryption Backup or Restore Wizard** selected, and select **Close**.

## Copy customized workflow assembly files

Use the following procedure to copy the workflow assembly files from the Service Manager Installation folder on the primary management server to the secondary management server that you created in the previous procedure.  

### Copy the workflow assembly files

Follow these steps to copy the workflow assembly files:

1. On the computer that is running the Service Manager Primary Server role, browse to the Service Manager Installation folder for example, C:\Program Files\Microsoft System Center\Service Manager copy the workflow files (workflow.dll).  
2. On the computer that is running the Service Manager Secondary server; browse to the Service Manager Installation folder; for example, C:\Program Files\Microsoft System Center\Service Manager. Paste the copied workflow files into this folder. You should overwrite any existing files.  

    > [!NOTE]  
    >  You must place the workflow assembly files in the Service Manager installation folder. This is very important step if you want to test the custom workflows that depend on workflow assembly files. Failure to copy these files would lead to failed custom workflows in the lab environment.

## Disable Service Manager connectors in the production environment

Use the following procedure to disable the Service Manager connectors in the production environment:

1. In the Service Manager console, select **Administration**.  
2. In the **Administration** pane, expand **Administration**, and select **Connectors**.  
3. In the **Connectors** pane, select the connector that you want to disable.  
4. In the **Tasks** pane, under the connector name, select **Disable**.  
5. In the **Disable Connector** dialog, select **OK**.

## Disable email notifications in the production environment

Use the following procedure to disable incoming and outbound email notifications in the production environment:

# [Disable outbound email notifications](#tab/DisableOutbound)

Follow these steps to disable outbound email notifications:

1. In the Service Manager console, select **Administration**.  
2. In the **Administration** pane, expand **Notifications**, and select **Channels**.  
3. In the **Channels** pane, select **E\-Mail Notification Channel**.  
4. In the **Tasks** pane, under **E\-Mail Notification Channel**, select **Properties** to open the **Configure E\-Mail Notification Channel** dialog.  
5. Clear the **Enable e\-mail notifications** checkbox.  

# [Disable incoming email notifications](#tab/DisableIncoming)

Follow these steps to disable incoming email notifications:

1. In the Service Manager console, select **Administration**.  
2. In the **Administration** pane, expand **Administration**, and select **Settings**.  
3. In the **Settings** pane, double\-click **Incident Settings**.  
4. In the Incident **Settings** dialog, select **Incoming E\-mail**.  
5. Clear **Turn on incoming e\-mails processing**, and select **OK**.

---

## Stop Service Manager services on the secondary management server

Use the following procedure to stop the Service Manager services:

### Stop the Service Manager services  

Follow these steps to stop the Service Manager services:

1. In the **Run** dialog, in the **Open** text field, enter **services.msc**, and select **OK**.  
2. In the **Services** window, in the **Services (Local)** pane, locate the following three services and for each one, and select **Stop**:  
    1. System Center Data Access Service  
    2. System Center Management  
    3. System Center Management Configuration  
3. Open Windows Explorer.  
4. Locate the folder \\Program Files\\Microsoft System Center\\Service Manager.  
5. Delete the **Health Service State** folder and all of its contents.

## Back up the production Service Manager database for future recovery

Use the following procedure to back up the production Service Manager database in Microsoft SQL Server:

### Back up the Service Manager database

Follow these steps to back up the Service Manager database:

1. After connecting to the appropriate instance of the Microsoft SQL Server Database Engine, in Object Explorer, select the server name to expand the server tree.
2. Expand **Databases**, and depending on the database, either select a user database or expand **System Databases** and select a system database.
3. Right-click the database, point to **Tasks**, and select **Back Up**. The Back Up Database dialog appears.
4. In the **Database** list box, verify the database name. You can optionally select a different database from the list.
5. You can perform a database backup for any recovery model (FULL, BULK_LOGGED, or SIMPLE).
6. In the **Backup type** list box, select **Full**.

    > [!NOTE]
    > After creating a full database backup, you can create a differential database backup. For more information, see [How to: Create a Differential Database Backup (SQL Server Management Studio)](/sql/relational-databases/backup-restore/create-a-differential-database-backup-sql-server).

7. Optionally, you can select **Copy Only Backup** to create a copy-only backup. A copy-only backup is a SQL Server backup that is independent of the sequence of conventional SQL Server backups. For more information, see [Copy-Only Backups](/sql/relational-databases/backup-restore/copy-only-backups-sql-server).

    > [!NOTE]
    > When the **Differential** option is selected, you can't create a copy-only backup.

8. For **Backup component**, select **Database**.
9. Either accept the default backup set name suggested in the **Name** text box, or enter a different name for the backup set.
10. Optionally, in the **Description** text box, enter a description of the backup set.
11. Specify when the backup set will expire and can be overwritten without explicitly skipping verification of the expiration data.

    > [!NOTE]
    > For more information about backup expiration dates, see [BACKUP (Transact-SQL)](/sql/t-sql/statements/backup-transact-sql).

12. Choose the type of backup destination by selecting **Disk** or **Tape**. To select the paths of up to 64 disk or tape drives containing a single media set, select **Add**. The selected paths are displayed in the **Backup to** list box.
13. To view or select the advanced options, select **Options** in the **Select a page** pane.
14. Select an Overwrite Media option, by selecting either **Back up to the existing media set** or **Back up to a new media set, and erase all existing backup sets**.
15. In the Reliability section, select either **Verify backup when finished** or **Perform checksum before writing to media**, and then optionally select **Continue on checksum error**. For more information, see [Detecting and Coping with Media Errors During Backup and Restore](/sql/relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server)

## Enable Service Manager connectors in the production environment

Use the following procedure to enable the Service Manager connectors in the production environment:

### Enable a connector  

Follow these steps to enable a connector:

1. In the Service Manager console, select **Administration**.  
2. In the **Administration** pane, expand **Administration**, and select **Connectors**.  
3. In the **Connectors** pane, select the connector that you want to enable.  
4. In the **Tasks** pane, under the connector name, select **Enable**.

## Enable email notifications in the production environment

Use the following procedure to enable incoming and outbound email notifications in the production environment:

# [Enable outbound email notifications](#tab/Outbound)

Follow these steps to enable outbound email notifications:

1. In the Service Manager console, select **Administration**.  
2. In the **Administration** pane, expand **Notifications**, and select **Channels**.  
3. In the **Channels** pane, select **E\-Mail Notification Channel**.  
4. In the **Tasks** pane, under **E\-Mail Notification Channel**, select **Properties** to open the **Configure E\-Mail Notification Channel** dialog.  
5. Select **Enable e\-mail notifications**.  

# [Enable incoming email notifications](#tab/Incoming)

Follow these steps to enable incoming email notifications:

1. In the Service Manager console, select **Administration**.  
2. In the **Administration** pane, expand **Administration**, and select **Settings**.  
3. In the **Settings** pane, double\-click **Incident Settings**.  
4. In the Incident **Settings** dialog, select **Incoming E\-mail**.  
5. Select **Turn on incoming e\-mails processing**, and select **OK**.

---

## Next steps

[Prepare the lab environment](lab-env.md)
