---
description: Use DPM to protect SharePoint farms, external SQL Server databases, and folders.
ms.topic: how-to
ms.service: system-center
keywords:
ms.date: 05/27/2025
title: Back up SharePoint with DPM
ms.subservice: data-protection-manager
ms.assetid: 3769bebe-3e5a-4b51-9c01-d07e94fc8c43
author: jyothisuri
ms.author: jsuri
ms.custom: UpdateFrequency2, engagement-fy23, engagement-fy24
---

# Back up SharePoint with DPM

You can deploy System Center Data Protection Manager (DPM) to protect SharePoint farms, external SQL Server databases, and folders that include farm customizations. This article describes the steps required to back up and recover SharePoint data. The following sections provide detailed information about configuring and restoring backup data for SharePoint:

- [Configure SharePoint protection in DPM](#configure-backup)

- [Restore SharePoint with DPM](#restore-sharepoint-data)

For information about troubleshooting, see [Troubleshoot SharePoint and DPM](https://techcommunity.microsoft.com/t5/system-center-blog/backing-up-sharepoint-with-data-protection-manager-and/ba-p/350563).

## Prerequisites and limitations

- For a list of supported SharePoint versions and the DPM versions required to back them up, see [What can DPM back up?](dpm-protection-matrix.md).

- By default when you protect SharePoint, all content databases \(and the SharePoint\_Config and SharePoint\_AdminContent\* databases\) will be protected. If you want to add customizations, such as search indexes, templates or application service databases, or the user profile service, you'll need to configure these for protection separately. Ensure that you enable protection for all folders that include these types of features or customization files:

- SharePoint databases using AlwaysOn can be protected from DPM 2012 R2 with Update 5 onwards.

- You can't protect SharePoint databases as a SQL Server data source. You can recover individual databases from a farm backup.

- Remember that for DPM runs as Local System and to back up SQL Server databases, it needs sysadmin privileges on that account for the SQL Server. On the SQL Server you want to back up, set NT AUTHORITY\\SYSTEM to sysadmin.

- For every 10 million items in the farm, there must be at least 2 GB of space on the volume where the DPM folder is located. This space is required for catalog generation. To enable you to use DPM to perform a specific recovery of items \(site collections, sites, lists, document libraries, folders, individual documents, and list items\), catalog generation creates a list of URLs contained within each content database. You can view the list of URLs in the recoverable items pane in the Recovery task area of the DPM Administrator Console.

- In the SharePoint farm, if you've SQL Server databases that are configured with SQL Server aliases, install the SQL Server client components on the front\-end Web server that DPM will protect.

- Protecting application store items isn't supported with SharePoint 2013.

- DPM doesn't support protecting remote FILESTREAM. The FILESTREAM should be part of the database.

## Before you start

Before you start backing up data, do the following:

1. **Deploy DPM** - Verify that DPM is installed and deployed correctly. If you haven't, see:

    - System requirements for DPM

    - [What can DPM back up?](dpm-protection-matrix.md)

    - [What's supported and what isn't for DPM?](dpm-support-issues.md)

    - [Get DPM installed](install-dpm.md)

2. **Set up storage** - You can store backed-up data on disk, on tape, and in the cloud with Azure. Read more in [Prepare data storage](plan-long-and-short-term-data-storage.md).

3. **Set up the DPM protection agent** - You'll need to install the DPM protection agent on every server in the SharePoint farm, including SQL Servers. The only exception is that you only install it on a single Web Front End \(WFE\) server. For example, if you've a single farm with two WFE servers, an index server and a two\-node SQL Server cluster, you would install the agent on the index server, both nodes in the SQL Server cluster, and one of the WFE servers. As WFE servers don't host content, DPM only needs the agent on one of them to serve as the entry point for protection. Read [Deploy the DPM protection agent](deploy-dpm-protection-agent.md).

    If the SharePoint SQL Server database is remote, you'll need to configure the DPM agent on it. If it's clustered, then install the agent on all cluster nodes.

## Configure backup

To back up SharePoint farm, configure protection for SharePoint by using ConfigureSharePoint.exe, and then create a protection group in DPM, follow these steps:

1. **Run ConfigureSharePoint.exe** - This tool configures the SharePoint VSS Writer service \(WSS\) and provides the protection agent with credentials for the SharePoint farm.
    After you've deployed the protection agent, the ConfigureSharePoint.exe file can be found in the \<DPM Installation Path\>\\bin folder on the front\-end Web server.  If you've multiple WFE servers, you only need to install it on one of them. Run as follows:

    - On the WFE server at a command prompt, navigate to \<DPM installation location\>\\bin\\ and run **ConfigureSharePoint \[\-EnableSharePointProtection\] \[\-EnableSPSearchProtection\] \[\-ResolveAllSQLAliases\] \[\-SetTempPath \<path\>\]**, where:

        - **EnableSharePointProtection** enables protection of the SharePoint farm, enables the VSS writer, and registers the identity of the DCOM application WssCmdletsWrapper to run as a user whose credentials are entered with this option. This account should be a farm admin and also local admin on the front\-end Web Server.

        - **EnableSPSearchProtection** enables the protection of WSS 3.0 SP Search by using the registry key SharePointSearchEnumerationEnabled under HKLM\\Software\\Microsoft\\ Microsoft Data Protection Manager\\Agent\\2.0\\ on the front\-end Web Server, and registers the identity of the DCOM application WssCmdletsWrapper to run as a user whose credentials are entered with this option. This account should be a farm admin and also local admin on the front\-end Web Server.

        - **ResolveAllSQLAliases** displays all the aliases reported by the SharePoint VSS writer and resolves them to the corresponding SQL Server. It also displays their resolved instance names. If the servers are mirrored, it will also display the mirrored server. It reports all the aliases that aren't being resolved to a SQL Server.

        - **SetTempPath** sets the environment variable TEMP and TMP to the specified path. Item-level recovery fails if a large site collection, site, list, or item is being recovered and there's insufficient space in the farm admin Temporary folder. This option allows you to change the folder path of the temporary files to a volume that has sufficient space to store the site collection or site being recovered.

    - Enter the farm administrator credentials. This account should be a member of the local Administrator group on the WFE server. If the farm administrator isn't a local admin, grant the following permissions on the WFE server:

        - Grant the WSS\_Admin\_WPG group full control to the DPM folder \(%Program Files%\\Microsoft Data Protection Manager\\DPM\).

        - Grant the WSS\_Admin\_WPG group read access to the DPM Registry key \(HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\Microsoft Data Protection Manager\).

        After running ConfigureSharePoint.exe,  you'll need to rerun it if there's a change in the SharePoint farm administrator credentials.

2. To create a protection group, select **Protection** > **Actions** > **Create Protection Group** to open the **Create New Protection Group** wizard in the DPM console.

3. In **Select Protection Group Type**, select **Servers**.

4. In **Select Group Members**, expand the server that holds the WFE role. If there's more than one WFE server, select the one on which you installed ConfigureSharePoint.exe. Learn more in [Deploy protection groups](create-dpm-protection-groups.md).

    When you expand the SharePoint server, DPM queries VSS to see what data DPM can protect. If the SharePoint database is remote, DPM connects to it. If the SharePoint data sources don't appear, check if the VSS writer is running on the SharePoint server and any remote SQL Server, and ensure that the DPM agent is installed on both the SharePoint server and the remote SQL Server. In addition, ensure that the SharePoint databases aren't being protected elsewhere as SQL Server databases.

5. In **Select data protection method**, specify how you want to handle short- and long\-term backup. Short\-term backup is always to disk first, with the option of backing up from the disk to the Azure cloud with Azure backup \(for short or long\-term\). As an alternative to long\-term backup to the cloud, you can also configure long\-term backup to a standalone tape device or tape library connected to the DPM server.

6. In **Select short-term goals** > **Retention range**, specify how long you want to keep the data on the disk. Under **Application recovery points**, select the Express Full Backup schedule. DPM will run an Express Full Backup just before each recovery point is scheduled. For SharePoint databases that are in full recovery mode, the logs will automatically be truncated after each successful Express Full Backup.

7. If you want to store data on tape for long-term storage, in **Specify long-term goals** indicate how long you want to keep the tape data (1-99 years). In Frequency of backup, specify how often backups to tape should run. The frequency is based on the retention range you've specified:

    - When the retention range is 1-99 years, you can select backups to occur daily, weekly, bi-weekly, monthly, quarterly, half-yearly, or yearly.

    - When the retention range is 1-11 months, you can select backups to occur daily, weekly, bi-weekly, or monthly.

    - When the retention range is 1-4 weeks, you can select backups to occur daily or weekly.

    On a standalone tape drive, for a single protection group, DPM uses the same tape for daily backups until there's insufficient space on the tape. You can also colocate data from different protection groups on tape.

    On the **Select Tape and Library Details** page, specify the tape/library to use and whether data should be compressed and encrypted on tape.

8. In the **Review disk allocation** page, review the storage pool disk space allocated for the protection group.

    **Total Data size** is the size of the data you want to back up, and **Disk space to be provisioned on DPM** is the space that DPM recommends for the protection group. DPM chooses the ideal backup volume based on the settings. However, you can edit the backup volume choices in the **Disk allocation details**. For the workloads, select the preferred storage in the dropdown menu. Your edits change the values for **Total Storage** and **Free Storage** in the **Available Disk Storage** pane. Underprovisioned space is the amount of storage DPM suggests you add to the volume to continue with backups smoothly in the future.

9. In **Choose replica creation method**, select how you want to handle the initial full data replication. If you select to replicate over the network, we recommend you choose an off-peak time. For large amounts of data or less than optimal network conditions, consider replicating the data offline using removable media.

10. In **Choose consistency check options**, select how you want to automate consistency checks. You can enable a check to run only when replica data becomes inconsistent or according to a schedule. If you don't want to configure automatic consistency checking, you can run a manual check at any time by right-clicking the protection group in the **Protection** area of the DPM console and selecting **Perform Consistency Check**.

11. If you've selected to back up to the cloud with Azure Backup, on the **Specify online protection data** page, ensure to select the workloads that you want to back up to Azure.

12. In **Specify online backup schedule**, specify how often incremental backups to Azure should occur. You can schedule backups to run every day/week/month/year and the time/date at which they should run. Backups can occur up to twice a day. Each time a backup runs, a data recovery point is created in Azure from the copy of the backed-up data stored on the DPM disk.

13. In **Specify online retention policy**, you can specify how the recovery points created from the daily/weekly/monthly/yearly backups are retained in Azure.

14. In **Choose online replication**, specify how the initial full replication of data will occur. You can replicate over the network or do an offline backup (offline seeding). Offline backup uses the Azure Import feature. [Read more](/azure/backup/backup-azure-backup-import-export).

15. On the  **Summary** page, review your settings. After you select **Create Group**, initial replication of the data occurs. When it finishes the protection, group status will show as **OK** on the **Status** page. Backup then takes place in line with the protection group settings.

## Monitoring

After the protection group has been created, the initial replication occurs and DPM starts backing up and synchronizing the Exchange data. DPM monitors the initial synchronization and subsequent backups.  You can monitor the SharePoint data in a couple of ways:

- Using default DPM monitoring can set up notifications for proactive monitoring by publishing alerts and configuring notifications. You can send notifications by email for critical, warning, or informational alerts, and for the status of instantiated recoveries.

- If you use Operations Manager, you can centrally publish alerts.

### Set up monitoring notifications

To set up monitoring the notifications, follow these steps:

1. In the DPM Administrator Console, select **Monitoring** > **Action** > **Options**.

2. Select **SMTP Server**, type the server name, port, and email address from which notifications will be sent. The address must be valid.

3. In **Authenticated SMTP server**, type a username and password. The username and password must be the domain account name of the person whose "From" address is described in the previous step; otherwise, notification delivery fails.

4. To test the SMTP server settings, select **Send Test E-mail**, type the e-mail address where you want DPM to send the test message, and then select **OK**. Select **Options** > **Notifications** and select the types of alerts about which recipients want to be notified. In **Recipients**, type the email address for each recipient to whom you want DPM to send copies of the notifications.

### Publish Operations Manager alerts

To publish Operations Manager alerts, follow these steps:

1. In the DPM Administrator Console, select **Monitoring** > **Action** > **Options** > **Alert Publishing** > **Publish Active Alerts**

2. After you enable **Alert Publishing**, all the existing DPM alerts that might require a user action are published to the **DPM Alerts** event log. The Operations Manager agent that is installed on the DPM server then publishes these alerts to the Operations Manager and continues to update the console as new alerts are generated.

## Restore SharePoint data

You can recover SharePoint data as follows:

- Recover to the original location.

- Recover to an alternate location. Remember, you can't perform a full farm recovery to a new location.

- Copy the data to a network folder.

- Copy the data to tape.

Remember, to recover a farm:

- If you protected a SharePoint server as a SQL Server database, you can recover SharePoint data by selecting the SQL Server database in the Recovery Wizard.

- Note the following to recover a farm:

    - The front-end Web servers should be configured the same as they were when the recovery point was created.

    - The farm structure must be created on the front-end Web server; the farm data will be recovered to the existing structure.

    - The instances of SQL Server are configured with the same names as when the recovery point was created.

    - The instances of SQL Server are configured with the same drive configuration as when the recovery point was created.

    - The recovery farm must have all service packs, language packs, and patches installed on the primary farm.

    - Don't directly try to recover the Central Administration content database or the configuration database because this could cause data corruption in the SharePoint farm.

    - The recovery point time for SharePoint data displayed on the **Browse** tab may differ from the time displayed on the **Search** tab. The **Browse** tab displays the backup time for the farm, while the **Search** tab lists the correct recovery point time for sites, documents, and folders.

There are a couple of possible scenarios for farm recovery:

- A farm configuration exists as it did at the time of taking the backup. In this case, you'll be restoring to a functioning farm.

- The configuration database is corrupt and the servers in the farm are down.

Select the required tab for steps to restore data to a functioning or non-functioning farm:

# [Restore data to a functioning farm](#tab/FunctioningFarm)

To restore data to a functioning farm, follow these steps:

1. In the DPM Administrator Console, select **Recovery** on the navigation bar.

2. In the **Protected data** pane, expand the server that contains the farm you want to recover and then select **All Protected SharePoint Data**. The farm displays in the **Recoverable** item pane as server name\farm name.

3. On the calendar, select any date in bold to obtain the recovery points available for that date. The **Recovery time** menu lists the time for each available recovery point.

4. On the **Recovery time** menu, select the recovery point you want to use.

5. In the **Actions** pane, select **Recover**.

    The Recovery Wizard starts.

6. On the **Review recovery selection** page, select **Next**.

7. Select where you want to recover the database.

> [!NOTE]
>  - You can't recover an entire farm to an alternate location.
>  - If you select **Copy to a network folder** and the recovery point that you selected wasn't created from an express full backup, you'll be presented with new recovery point choices.
>  - If you select **Copy to tape** and the recovery point that you selected wasn't created from an express full backup, you'll be presented with new recovery point choices. For the tape option, you'll select the tape library you want to use for recovery.

8. Specify recovery options for network bandwidth usage throttling, SAN-based recovery, and email notifications, and then select **Next**.

9. On the **Summary** page, review the recovery settings and then select **Recover**.

# [Restore data to a non-functioning farm](#tab/NonfunctioningFarm)

To restore data to a non-functioning farm, follow these steps:

1. Create a new farm that uses the same instance of SQL Server and the same front-end Web server as the original protected farm.

2. On the front-end Web server that DPM uses to recover farm data, run the following command at the command prompt:`ConfigureSharePoint-EnableSharePointProtection`

3. In the DPM Administrator Console, select **Recovery** on the navigation bar.

4. In the **Protected data** pane, expand the server that contains the farm you want to recover, and then select **All Protected SharePoint Data**. The farm displays in the **Recoverable** item pane as server name\farm name.

5. On the calendar, select any date in bold to obtain the recovery points available for that date. The **Recovery time** menu lists the time for each available recovery point.

6. On the **Recovery time** menu, select the recovery point you want to use.

7. In the **Actions** pane, select **Recover**.

    The Recovery Wizard starts.

8. On the **Review recovery selection** page, select **Next**.

9. Select where you want to recover the database.

    > [!NOTE]
    > - You can't recover an entire farm to an alternate location.
    > - If you select **Copy to a network folder** and the recovery point that you selected wasn't created from an express full backup, you'll be presented with new recovery point choices.
    > - If you select **Copy to tape** and the recovery point that you selected wasn't created from an express full backup, you'll be presented with new recovery point choices. For the tape option, you'll select the tape library you want to use for recovery.

10. Specify recovery options for network bandwidth usage throttling, SAN-based recovery, and e-mail notifications, and then select **Next**.

11. On the **Summary** page, review the recovery settings, and then select **Recover**.

12. On the main front-end Web server for the server farm, run the SharePoint Products and Technologies Configuration Wizard and disconnect the front-end Web server from the farm.

---

## Switch the Front-End Web Server

The following procedure uses the example of a server farm with two front-end Web servers, Server1 and Server2. DPM uses Server1 to protect the farm. You need to change the front-end Web server that DPM uses to Server2 so that you can remove Server1 from the farm.

> [!NOTE]
> If the front-end Web server that DPM uses to protect the farm is unavailable, use the following procedure to change the front-end Web server by starting at step 4.

#### Change the front-end Web server that DPM uses to protect the farm

To change the front-end Web server that DPM uses to protect the farm, follow these steps:

1. Stop the SharePoint VSS Writer service on Server1 by running the following command at command prompt:

   **stsadm -o unregisterwsswriter**

2. On Server1, open the Registry Editor and navigate to the following key:

   **HKLM\System\CCS\Services\VSS\VssAccessControl**

3. Check all the values listed in the VssAccessControl subkey. If any entry has a value data of 0 and another VSS writer is running under the associated account credentials, change the value data to 1.

4. Install a protection agent on Server2.

   > [!WARNING]
   > You can only switch Web front-end servers if both the servers are on the same domain.

5. On Server2, at the command prompt, change the directory to _DPM installation location_\bin\ and run ConfigureSharepoint. For more information about ConfigureSharePoint, see [Configure backup](#configure-backup).

6. There's a known issue when the server farm is the only member of the protection group and the protection group is configured to use tape-based protection. If your server farm is the only member of the protection group using tape-based protection, to change the front-end Web server that DPM uses to protect the farm, you must temporarily add another member to the protection group by performing the following steps:

   - In the DPM Administrator Console, select **Protection** on the navigation bar.

   - Select the protection group that the server farm belongs to and then select **Modify protection group**.

   - In the Modify Group Wizard, add a volume on any server to the protection group. You can remove this volume from the protection after the procedure is completed.

   - If the protection group is configured for short-term disk-based protection and long-term tape-based protection, select the manual replica creation option. This prevents creating a replica for the volume that you're temporarily adding to the protection group.

   - Complete the wizard.

7. Remove Server1 from the protection group, selecting to retain the replicas on disk and tape.

8. Select the protection group that the server farm belongs to and then select **Modify protection group**.

9. In the Modify Group Wizard, on the **Select Group Members** page, expand Server2 and select the server farm and then complete the wizard.

   A consistency check will start.

10. If you performed step 6, you can now remove the volume from the protection group.

::: moniker range="= sc-dpm-2019"

## Remove a database from a SharePoint farm

When a database is removed from a SharePoint farm, DPM will skip the backup of that database, continue to back up other databases in the SharePoint farm, and alert the backup administrator.

### DPM Alert - Farm Configuration Changed

This is a warning alert that is generated in Data Protection Manager (DPM) when automatic protection of a SharePoint database fails. For more information about the cause of this alert, see the alert **Details** pane.

To resolve the DPM alert, follow these steps:

1. Verify with the SharePoint administrator if the database has been removed from the farm. If the database has been removed from the farm, then it must be removed from active protection in DPM.
2. To remove the database from active protection:
   1. In the **MABS Administrator Console**, select **Protection** on the navigation bar.
   2. In the **Display** pane, right-click the protection group for the SharePoint farm, and then select **Stop Protection of member**.
   3. In the **Stop Protection** dialog, select **Retain Protected Data**.
   4. Select **Stop Protection**.

You can add the SharePoint farm back for protection by using the **Modify Protection Group** wizard. During reprotection, select the SharePoint front-end server and select **Refresh** to update the SharePoint database cache, and then select the SharePoint farm and proceed.

::: moniker-end
