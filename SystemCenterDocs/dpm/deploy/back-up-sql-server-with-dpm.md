---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  markgalioto
ms.prod:  system-center-threshold
keywords:  
ms.date: 10/12/2016
title:  Back up SQL Server with DPM
ms.technology:  data-protection-manager
ms.assetid:  3718b565-9640-4c3f-9d44-aa969041e0e6
ms.author: markgal
---

# Back up SQL Server with DPM

>Applies To: System Center 2016 - Data Protection Manager

DPM provides backup and recovery for SQL Server databases. In addition to backing up SQL Server databases you can run a system backup or full bare-metal  backup of the SQL Server computer. Here's what DPM can protect:

-   A standalone SQL Server instance

-   A SQL Server Failover Cluster instance (FCI)

-   A SQL Server AlwaysOn availability group with theses preferences:

    -   Secondary only

    -   Primary

    -   Any Replica

## Why back up SQL Server with DPM?

-   DPM was designed to protect the advanced configurations of SQL Server.

-   DPM can be set to protect SQL Server as frequently as every 15 minutes.

-   DPM reduces potential conflicts between backup tools and SQL Server protection schedules.

-   DPM can protect SQL Server at the instance level or the database level. When protection at the instance level is turned on, DPM detects new databases on that instance and automatically adds them to its protection group.

-   DPM is an affordable option. It's a good fit for a small SQL Server footprint and can scale for organizations that have a larger SQL Server footprint.

-   DPM has a Self-Service Recovery Tool (SSRT) that extends database administrators' options for self-service recovery of SQL databases.

-   If you're upgrading to SQL Server 2014  DPM will continue to back up already protected databases after the SQL Server upgrade. You should avoid backup jobs during the SQL Server upgrade.

## Prerequisites and limitations

-   If you have a database with files on a remote file share, protection will fail with Error ID 104. DPM does not support protection for SQL Server data on a remote file share.

-   DPM cannot protect databases that are stored on remote SMB shares.

-   Ensure that the availability group replicas are configured as read-only.

-   You must explicitly add the system account NTAuthority\System to the Sysadmin group on SQL Server.

-   When you perform an alternate location recovery for a partially contained database, you must ensure that the target SQL instance has the Contained Databases feature enabled.

-   Protection for SQL Server AlwaysOn:

    -   DPM detects Availability Groups when running inquiry at protection group creation.

    -   DPM detects a failover and continues protection of the database.

    -   DPM supports multi-site cluster configurations for an instance of SQL Server.

    When you protect databases that use the AlwaysOn feature, DPM has the following limitations:

    -   DPM will honor the backup policy for availability groups that is set in SQL Server based on the backup preferences, as follows:

        -   Prefer secondary - Backups should occur on a secondary replica except when the primary replica is the only replica online. If there are multiple secondary replicas available then the node with the highest backup priority will be selected for backup. In the case that only primary replica is available then backup should occur on the primary replica.

        -   Secondary only - Backup shouldn't be performed on the primary replica. If the primary replica is the only one online, the backup shouldn't occur.

        -   Primary - Backups should always occur on the primary replica.

        -   Any Replica - Backups can happen on any of the availability replicas in the availability group. The node to be backed up from will be based on the backup priorities for each of the nodes.

    -   Note the following:

        -   Backups can happen from any readable replica i.e. primary, synchronous secondary, asynchronous secondary.

        -   If any replica is excluded from backup, for example Exclude Replica is enabled or is marked as not readable, then that replica will not be selected for backup under any of the options.

        -   If multiple replicas are available and readable then the node with the highest backup priority will be selected for backup.

        -   If the backup fails on the selected node then the backup operation fails.

        -   Recovery to the original location is not supported.

-   SQL Server 2014 backup issues:

    -   SQL server 2014 added a new feature to create a database for on-premises SQL Server in Windows Azure Blob storage. DPM cannot be used to protect this configuration.

    -   There are some known issues with "Prefer secondary" backup preference for the SQL AlwaysOn option, DPM always takes a backup from secondary; if no secondary can be found then the backup fails.

## Before you start


1.  **Deploy DPM** - Verify that DPM is installed and deployed correctly. If you haven't see:

    -   System requirements for DPM

    -   [What can DPM back up?](../dpm-protection-matrix.md)

    -   [What's supported and what isn't for DPM?](../dpm-support-issues.md)

    -   [Get DPM installed](../install-dpm.md)

2.  **Set up storage** - You can store backed up data on disk, on tape, and in the cloud with Azure. Read more in [Prepare data storage](../plan-long-and-short-term-data-storage.md).

3.  **Set up the DPM protection agent** - You'll need to install the DPM protection agent on every machine you want to back up. Read [Deploy the DPM protection agent](Deploy-the-DPM-protection-agent.md).


## Configure backup

1.  To create a protection group, click **Protection** > **Actions** > **Create Protection Group** to open the **Create New Protection Group** wizard in the DPM console.

2.  In **Select Protection Group Type**, select **Servers**.

3.  In **Select Group Members**, select the SQL Server instances on the server you want to protect.  Learn more in [Deploy protection groups](Deploy-protection-groups.md). Note that:

    -   You have the option of selecting protection at the instance level or protection of individual databases.

    -   When you are protecting at the instance level, any database that is added to that instance of SQL Server will automatically be added to DPM protection.

    -   If you are using SQL Server AlwaysOn availability groups, you can create a protection group that contains the availability groups.   DPM detects the availability groups and will displays them under **Cluster Group**. Select the whole group to protect it so that any databases that you add to the group are protected automatically, or select individual databases.
        For each instance of SQL Server, you can also run a system state backup or full bare metal backup. This in useful if you want to be able to recover your whole server and not just data.

4.  In **Select data protection method**,  specify how you want to handle short and long-term backup. Short-term back up is always to disk first, with the option of backing up from the disk to the Azure cloud with Azure backup (for short or long-term). As an alternative to long-term backup to the cloud you can also configure long-term back up to a standalone tape device or tape library connected to the DPM server.

5.  In **Select short-term goals**, specify how you want to back up to short-term storage on disk. In **Retention range**, you specify how long you want to keep the data on disk. In **Synchronization frequency**,  you specify how often you want to run an incremental backup to disk. If you don't want to set a back up interval, you can select **Just before a recovery point** so that DPM will run an express full backup just before each recovery point is scheduled.

6.  If you want to store data on tape for long-term storage, in **Specify long-term goals**, indicate how long you want to keep tape data (1-99 years). In Frequency of backup specify how often backups to tape should run. The frequency is based on the retention range you've specified:

    -   When the retention range is 1-99 years, you can select backups to occur daily, weekly, bi-weekly, monthly, quarterly, half-yearly, or yearly.

    -   When the retention range is 1-11 months, you can select backups to occur daily, weekly, bi-weekly, or monthly.

    -   When the retention range is 1-4 weeks, you can select backups to occur daily or weekly.

    On a stand-alone tape drive, for a single protection group, DPM uses the same tape for daily backups until there is insufficient space on the tape. You can also colocate data from different protection groups on tape.

    On the **Select Tape and Library Details**, page specify the tape/library to use, and whether data should be compressed and encrypted on tape.

7.  In the **Review disk allocation** page review the storage pool disk space allocated for the protection group.

    **Total Data size** is the size of the data you want to back up, and **Disk space to be provisioned on DPM** is the space that DPM recommends for the protection group. DPM chooses the ideal backup volume, based on the settings. However, you can edit the backup volume choices in the **Disk allocation details**. For the workloads, select the preferred storage in the dropdown menu. Your edits change the values for **Total Storage** and **Free Storage** in the **Available Disk Storage** pane. Underprovisioned space is the amount of storage DPM suggests you add to the volume, to continue with backups smoothly in the future.

8.  In **Choose replica creation method**, select how you want to handle the initial full data replication.  If you select to replicate over the network we recommended you choose an off-peak time. For large amounts of data or less than optimal network conditions, consider replicating the data offline using removable media.

9. In **Choose consistency check options**, select how you want to automate consistency checks. You can enable a check to run only when replica data becomes inconsistent, or according to a schedule. If you don't want to configure automatic consistency checking, you can run a manual check at any time by right-clicking the protection group in the **Protection** area of the DPM console, and selecting **Perform Consistency Check**.

10. If you've selected to back up to the cloud with Azure Backup, on the **Specify online protection data** page make sure the workloads you want to back up to Azure are selected.

11. In **Specify online backup schedule**, specify how often incremental backups to Azure should occur. You can schedule backups to run every day/week/month/year and the time/date at which they should run. Backups can occur up to twice a day. Each time a back up runs a data recovery point is created in Azure from the copy of the backed up data stored on the DPM disk.

12. In **Specify online retention policy**, you can specify how the recovery points created from the daily/weekly/monthly/yearly backups are retained in Azure.

13. In **Choose online replication**, specify how the initial full replication of data will occur. You can replicate over the network, or do an offline backup (offline seeding). Offline backup uses the Azure Import feature. For more information, see [Offline-backup workflow in Azure Backup](https://azure.microsoft.com/documentation/articles/backup-azure-backup-import-export/).

14. On the  **Summary** page, review your settings. After you click **Create Group** initial replication of the data occurs. When it finishes the protection group status will show as **OK** on the **Status** page. Backup then takes place in line with the protection group settings.

## Monitoring
After the protection group's been created the initial replication occurs and DPM starts backing up and synchronizing SQL Server data. DPM monitors the initial synchronization and subsequent backups.  You can monitor the SQL Server data in a couple of ways:

-   Using default DPM monitoring can set up notifications for proactive monitoring. by publishing alerts and configuring notifications. You can send notifications by e-mail for critical, warning, or informational alerts, and for the status of instantiated recoveries.

-   If you use Operations Manager you can centrally publish alerts.

### Set up monitoring notifications

1.  In the DPM Administrator Console, click **Monitoring** > **Action** > **Options**.

2.  Click **SMTP Server**, type the server name, port, and email address from which notifications will be sent. The address must be valid.

3.  In **Authenticated SMTP server** , type a user name and password. The user name and password must be the domain account name of the person whose "From" address is described in the previous step; otherwise, notification delivery fails.

4.  To test the SMTP server settings, click **Send Test E-mail**, type the e-mail address where you want DPM to send the test message, and then click **OK**. Click **Options** > **Notifications** and select the types of alerts about which recipients want to be notified. In **Recipients** type the e-mail address for each recipient to whom you want DPM to send copies of the notifications.

### Set up alerts with Operations Manager

1.  In the DPM Administrator Console, click **Monitoring** > **Action** > **Options** > **Alert Publishing** > **Publish Active Alerts**

2.  After you enable **Alert Publishing** all existing DPM alerts that might require a user action are published to the **DPM Alerts** event log. The Operations Manager agent that is installed on the DPM server then publishes these alerts to the Operations Manager and continues to update the console as new alerts are generated.

## Allow SQL Server admins to restore data
DPM provides a self-service recovery feature to allow SQL Server administrators access to data protected by DPM, so that they can restore a SQL Server database from backup to a network folder.
 You set up the  DPM Self-Service Recovery Configuration Tool to create and manage roles that specify which users can perform self-service recovery. Then users use the DPM Self-Service Recovery Wizard to recover SQL Server databases.

Configure self-service SQL Server recovery as follows:

1.  In the DPM console > **Protection**  click **Configure self service recovery**.

2.  In the DPM Self-Service Recovery Configuration Tool for SQL Server click **Create Role**.

3.  On the **Security Groups** page, you'll create one or more groups that contain the users for whom you want to enable self-service reocvery.  Specify  security groups in the format domain\security group,  or an individual user in the format domain\user name. You can add multiple groups and users to a DPM role.

4.  On the **Recovery Items** page you specify protected SQL Server instances and databases for which you want to allow self-service recovery. Specify instances in the format <computer name\instance name>. To specify a database  press the TAB key, and then type a database name. Alternatively, to enable role users to recover all databases on the instance, press the TAB key, and then press the spacebar to clear the text in the **Database Name** column.

    Note that when you enable users of a DPM role to recover all SQL Server databases on an instance of SQL Server, those users can also recover any SQL Server databases that are subsequently added to the instance. When you enable access by using DPM roles, ensure that all members of the role have been granted appropriate permission to view and access all databases.

5.  On the **Recovery Target Locations** page,  to restrict recovery locations for role users click **Allow users to recover the databases to another instance of SQL Server** and specify one or more recovery target locations and file paths that are allowed. If you want to allow any path on an instance then don't specify a value in **Recovered File Path**.   If you enable the setting users can  recover database files to any location for which they have write permission. However, users cannot overwrite the original database files, and the DPM Self-Service Recovery Tool (SSRT) for SQL Server blocks them if they attempt to do so.

6.  In addition on the computer from which self-service recovery will run make sure that at least .NET framework 3.5 is installed, and that the DPM Self-Service Recovery Tool is installed. The tool is available in the DPM product installation location, in the **DpmSqlEURInstaller** folder.

## Restore  SQL Server data
You can recover SharePoint data as follows:

-   Recover a database to the original location

-   Recover the database with a new name to its original location or to a different instance of SQL Server

-   Recover the database to a different instance of SQL Server

-   Copy the database to a network folder

-   Copy the database to tape

Note that you can't recover a system database to a different instance of SQL Server.

Recover a database from the DPM console as follows:

1.  In the DPM Administrator Console click **Recovery** on the navigation bar.  Using the browse functionality, select the database you want to recover.

2.  On the calendar, click any date in bold to obtain the recovery points available for that date. The **Recovery time** menu lists the time for each available recovery point.     On the **Recovery time** menu, select the recovery point you want to use.

3.  In the **Actions** pane, click **Recover** to start the Recovery Wizard.

4.  On the **Review recovery selection** page, click **Next**.  Note that:

    -   Select where you want to recover the database. If you select **Recover to any SQL instance** enter the recovery path. You can specify a new name for the recovered database. Note that this option isn't available with the setting **Latest recovery point**.

    -   You can't recover a newer version SQL Server database to an older version SQL Server instance.

    -   If you select **Copy to a network folder** and the recovery point that you selected wasn't created from an express full backup, you'll be presented with new recovery point choices.

    -   If you select **Copy to tape** and the recovery point that you selected wasn't created from an express full backup, you'll be presented with new recovery point choices. For the tape option you'll select the tape library you want to use for recovery.

5.  If you selected a recovery point other than  **Latest,** on the Specify Database State page, select **Leave database operational**.

6.  Specify recovery options for network bandwidth usage throttling, SAN-based recovery, and e-mail notifications, and then click **Next**.

7.  On the **Summary** page, review the recovery settings, and then click **Recover**.

If you want to restore data to a non-functioning SharePoint farm you'll need to create a new farm that uses the same SQL Server instance and same front-end web server  as the original farm. Then you'll run this command on the front-end web server that DPM uses to recover farm data: `ConfigureSharePoint-EnableSharePointProtection`.   Open the Recovery Wizard and in Protected Data expand the server that contains the farm you want to recovery and click **All Protected Farm Data**. Select the recovery point date and time, and recover. Note that you can't recover an entire farm to an alternate location. After recovery is finished, on  the main front-end Web server for the server farm, run the SharePoint  Configuration Wizard and disconnect the front-end Web server from the farm.

Users with self-service recovery permissions should recover as follows:

1.  The user should open the DPM Self-Service Recovery Tool, click **Connect to DPM server**, and specify the DPM server name.

2.  After a connection is established the user should click **New Recovery Job** to start the Recovery Wizard.

3.  On the **Specify Database Details** page of the wizard, specify the SQL Server instance and database name to recovery. If you're using availability groups specify the group name in the format: **AGNAME.ClusternameFQDN\AGNAME**.

4.  On the **Specify Recovery Point** page select the data and time of recovery point.

5.  On the **Select Recovery Type** page select whether to recovery to any instance on the same SQL Server or a different one. Specify whether to recover to a network folder.  Note that only recovery points that will created from full express backup can be recovered to a network folder.

6.  If you're recovering to a database, on the **Specify Database State**  page specify whether the database should remain operational after recovery, and specify whether you want to copy SQL transaction logs.

7.  On the **Specify Recovery Options** page specify whether you want to retain security settings from the source server, or apply settings from the destination server. You can also specify that an email notification should be sent when recovery finishes.
