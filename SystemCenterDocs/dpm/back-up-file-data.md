---
description:  You can back up file data on server and client computers with DPM.
manager:  carmonm
ms.topic:  article
author:  markgalioto
ms.author: markgal
ms.prod:  system-center-threshold
keywords:  
ms.date: 11/01/2017
title:  Back up file data with DPM
ms.technology:  data-protection-manager
ms.assetid:  98626f09-e4b1-4cbb-9195-651d54e118d1
---

# Back up file data with DPM

>Applies To: System Center 2016 - Data Protection Manager

You can use System Center Data Protection Manager (DPM) to back up file data on server and client computers.

## Before you start

1.  **Deploy DPM** - Verify that DPM is installed and deployed correctly. We recommend that you review the following articles:

    -   [System requirements](prepare-environment-for-dpm.md)

    -   [What can DPM back up?](dpm-protection-matrix.md)

    -   [What's supported and what isn't for DPM?](dpm-support-issues.md)

    -   [Get DPM installed](install-dpm.md)

2.  **Set up storage** - You can store backed up data on disk, on tape, and in the cloud with Azure. Read more in [Prepare data storage](plan-long-and-short-term-data-storage.md).

3.  **Set up the DPM protection agent** - You'll need to install the DPM protection agent on every machine you want to back up. Read [Deploy the DPM protection agent](deploy-dpm-protection-agent.md).

## Back up file data
After you have your DPM infrastructure set up you can enable protection machines that have file data you want to back up.

1.  To create a protection group, click **Protection** > **Actions** > **Create Protection Group** to open the **Create New Protection Group** wizard in the DPM console.

2.  In **Select Protection Group Type** select **Servers**.

3.  In **Select Group Members** you'll add the machines for which you want to back up file data to the protection group. On those machines you select the locations, shares, and folders you want to protect.  [Deploy protection groups](create-dpm-protection-groups.md). You can select different types of folders (such as Desktop) or different file types. You can also exclude specific locations from protection.

4.  In **Select data protection method**  specify how you want to handle short and long-term backup. Short-term back up is always to disk first, with the option of backing up from the disk to the Azure cloud with Azure backup (for short or long-term). As an alternative to long-term backup to the cloud you can also configure long-term back up to a standalone tape device or tape library connected to the DPM server.

5.  In **Select short-term goals** specify how you want to back up to short-term storage on disk.  In **Retention range** you specify how long you want to keep the data on disk. In **Synchronization frequency** you specify how often you want to run an incremental backup to disk. If you don't want to set a back up interval you can check Just before  a recovery point so that DPM will run an express full backup just before each recovery point is scheduled.

6.  If you want to store data on tape for long-term storage in **Specify long-term goals** indicate how long you want to keep tape data (1-99 years). In Frequency of backup specify how often backups to tape should run. The frequency is based on the retention range you've specified:

    -   When the retention range is 1-99 years, you can select backups to occur daily, weekly, bi-weekly, monthly, quarterly, half-yearly, or yearly.

    -   When the retention range is 1-11 months, you can select backups to occur daily, weekly, bi-weekly, or monthly.

    -   When the retention range is 1-4 weeks, you can select backups to occur daily or weekly.

    On a stand-alone tape drive, for a single protection group, DPM uses the same tape for daily backups until there is insufficient space on the tape. You can also co-locate data from different protection groups on tape.

    On the **Select Tape and Library Details** page specify the tape/library to use, and whether data should be compressed and encrypted on tape.

7.  In the **Review disk allocation** page review the storage pool disk space allocated for the protection group.

    **Total Data size** is the size of the data you want to back up, and **Disk space to be provisioned on DPM** is the space that DPM recommends for the protection group. DPM chooses the ideal backup volume, based on the settings. However, you can edit the backup volume choices in the **Disk allocation details**. For the workloads, select the preferred storage in the dropdown menu. Your edits change the values for **Total Storage** and **Free Storage** in the **Available Disk Storage** pane. Underprovisioned space is the amount of storage DPM suggests you add to the volume, to continue with backups smoothly in the future.

8.  In **Choose replica creation method** select how you want to handle the initial full data replication.  If you select to replicate over the network we recommended you choose an off-peak time. For large amounts of data or less than optimal network conditions, consider replicating the data offline using removable media.

9. In **Choose consistency check options**, select how you want to automate consistency checks. You can enable a check to run only when replica data becomes inconsistent, or according to a schedule. If you don't want to configure automatic consistency checking, you can run a manual check at any time by right-clicking the protection group in the **Protection** area of the DPM console, and selecting **Perform Consistency Check**.

10. If you've selected to back up to the cloud with Azure Backup, on the **Specify online protection data** page make sure the workloads you want to back up to Azure are selected.

11. In **Specify online backup schedule** specify how often incremental backups to Azure should occur. You can schedule backups to run every day/week/month/year and the time/date at which they should run. Backups can occur up to twice a day. Each time a back up runs a data recovery point is created in Azure from the copy of the backed up data stored on the DPM disk.

12. In **Specify online retention policy** you can specify how the recovery points created from the daily/weekly/monthly/yearly backups are retained in Azure.

13. In **Choose online replication** specify how the initial full replication of data will occur. You can replicate over the network, or do an offline backup (offline seeding). Offline backup uses the Azure Import feature. [Read more](https://azure.microsoft.com/en-in/documentation/articles/backup-azure-backup-import-export/).

14. On the  **Summary** page review your settings. After you click **Create Group** initial replication of the data occurs. When it finishes the protection group status will show as **OK** on the **Status** page. Backup then takes place in line with the protection group settings.

## Recover backed up file data
You recover data using the Recovery Wizard. When you double-click a protected volume on the **Protected data** pane in the wizard, DPM displays the data that belongs to that volume in the results pane. You can filter protected server names alphabetically by clicking **Filter**. After selecting a data source to recover in the tree view, you can select a specific recovery point by clicking the bold dates in the calendar. When you click **Recover** in the **Actions** pane, DPM starts the recovery job.

## Recover data
Recover data from the DPM console as follows:

1.  In DPM console  click **Recovery** on the navigation bar. and browse for the data you want to recover. In the results pane, select the data.

2.  Available recovery points are indicated in bold on the calendar in the recovery points section. Select the bold date for the recovery point you want to recover.

3.  In the **Recoverable item** pane, click to select the recoverable item you want to recover.

4.  In the **Actions** pane, click **Recover** to open the Recovery Wizard.

5.  You can recover data as follows:

    1.  **Recover to the original location**. Note that this doesn't work if the client computer is connected over VPN. In this case use an alternate location and then copy data from that location.

    2.  **Recover to an alternate location**.

    3.  **Copy to tape**. This option copies the volume that contains the selected data to a tape in a DPM library. You can also choose to compress or encrypt the data on tape.

6.  Specify your recovery options:

    1.  **Existing version recovery behavior**. Select **Create copy**, **Skip**, or **Overwrite**. This option is enabled only when you're recovering to the original location.

    2.  **Restore security**. Select **Apply settings of the destination computer** or **Apply the security settings of the recovery point version**.

    3.  **Network bandwidth usage throttling**. Click **Modify** to enable network bandwidth usage throttling.

    4.  **Enable SAN based recovery using hardware snapshots**. Select this option to use SAN-based hardware snapshots for quicker recovery.

        This option is valid only when you have a SAN where hardware snapshot functionality is enabled, the SAN has the capability to create a clone and to split a clone to make it writable, and the protected computer and the DPM server are connected to the same SAN.

    5.  **Notification**. Click **Send an e-mail when the recovery completes**, and specify the recipients who will receive the notification. Separate the e-mail addresses with commas.

7.  Click **Next** after you have made your selections for the preceding options.

8.  Review your recovery settings, and click **Recover**. Note that any synchronization job for the selected recovery item will be canceled while the recovery is in progress.

When using Modern Backup Storage (MBS), File Server end user recovery (EUR) is not supported. File Server EUR has a dependency on the Volume Shadow Copy Service (VSS), which Modern Backup Storage does not use. If end-user recovery is enabled, then recover data as follows:

1.  Navigate to the protected data file. Right-click the file name > **Properties**.

2.  In **Properties** > **Previous Versions** select the version that you want to recover.
