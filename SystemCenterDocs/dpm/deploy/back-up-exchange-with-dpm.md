---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  markgalioto
ms.author: markgal
ms.prod:  system-center-threshold
keywords:  
ms.date: 10/12/2016
title:  Back up Exchange with DPM
ms.technology:  data-protection-manager
ms.assetid:  79fb8831-1d70-4d1d-bed1-f28fa9186730
---

# Back up Exchange with DPM

>Applies To: System Center 2016 - Data Protection Manager

DPM provides backup and recovery for Exchange 2013. You can back up the following:

-   Exchange mailbox databases under a database availability group (DAG)

-   In addition to backing up mail databases, to fully protect your Exchange deployment you'll need to backup other Exchange Server roles such as the Client Access Server, or the transport service on mailbox servers. You can configure protection for volumes, system state or full bare metal recovery backup to ensure that all Exchange data and configuration settings are protected.

## Prerequisites and limitations
Before you deploy DPM to protection Exchange 2013 verify the deployment prerequisites:

-   Review the [Release Notes for System Center 2016](../../get-started/release-notes.md) and [What's supported and what isn't for DPM?](../get-started/What-s-supported-and-what-isn-t-for-DPM-.md) to check for any Exchange issues.

-   Make sure the same versions of Eseutil.exe and Ese.dll are installed on both the Exchange and the DPM server. For example, if you're using the 64-bit version of DPM, you must have the 64-bit version of eseutil.exe and ese.dll.  If you update these files on the Exchange server you'll need to update them on the DPM server too. The .ese and .eseutil files are usually in C:\Program Files\Microsoft\Exchange Server\V15\Bin folder.

    To maintain up-to-date copies do the following:

    1.  At the command prompt, navigate to the `<DPM installation folder>\Bin` directory.

    2.  Type the fsutil command as follows to create a hard link for eseutil.exe: `fsutil hardlink create <link> <target>`

        For example in a typical installation type: `fsutil hardlink create "c:\program files\microsoft\dpm\bin\eseutil.exe" "c:\program files\microsoft\Exchange\bin\eseutil.exe"`

-   Install the latest [Visual C++ Redistributable for Visual Studio 2012 Update](http://go.microsoft.com/fwlink/?LinkId=266498).

-   To protect an Exchange 2013 Database Availability Group (DAG) node, install the DPM protection agent on the node. Note that you can protect different DAG nodes from different DPM servers, only one node can be protected by one DPM server only.

-   You can protect up to 80 terabytes (TB) of data with a single DPM server. Therefore, you can protect DAGs that have up to 20 nodes with a single server or up to 10,000 mailboxes with a DPM server.

-   DPM functions with any database role. You can configure DPM to protect a server that hosts a collection of active or passive mailbox databases.

-   You should configure at least one full backup per day and a synchronization frequency to suit your requirements for Exchange log truncations When you protect more than one copy of an Exchange mailbox database (for example, when you are protecting multiple members of a DAG), you should configure one node for full backups and the rest for copy backups. Copy backups do not truncate log files.

-   Protect at least two copies of each mailbox database whether Exchange is implemented with inexpensive Serial ATA (Serial Advanced Technology Attachment or SATA) or several disks/drives (JBOD) disks.

-   Set the minimum frequency to greater than 15 minutes for mailbox synchronization. Start by setting up your current backup policy, and then gradually increase the number of recovery points. Performing one or two express full backups per day, in addition to a synchronization frequency of two hours, is a sound approach. For an optimal synchronization frequency consider the volume of your data, the performance impact, and the volume required to store the replicas.

-   Exchange 2013 can support up to eight parallel backups. To accommodate parallel Exchange database backups for an Exchange server, create multiple protection groups (up to eight), and add Exchange databases to each protection group.

-   As you maintain your Exchange data note the following:

    -   **Add mailbox databases to the server**. If you create or add new mailbox databases to a protected storage group on an Exchange server, these databases are automatically added to the DPMreplication and protection. You can add mailbox databases in incremental backups only after a full backup has finished.

    -   **Change mailbox database file paths**. If you move a protected database or log files to a volume that contains data that is protected by DPM, protection continues. If you move a protected database or log files to a volume that is not protected by DPM, an alert appears, and the protection jobs fail. To resolve the alert, in the alert details, click the **Modify protection job** link, and then run a consistency check.

    -   **Dismount mailbox databases**. If you dismount a protected mailbox database, the protection job for that particular database fails. The replica is marked inconsistent when DPM runs the next express full backup.

    -   **Rename mailbox databases**. If you need to change the name of the mailbox database, stop protection, and protect the database again. Until you protect the database again, the backups continue to work but mailbox enumeration fails.

## Why back up Exchange with DPM?
When deciding whether to back up Exchange data with Exchange 2013 native data protection or DPM, consider the following:

Native data protection provides:

-   Disaster recovery

-   Recovery of accidentally deleted items

-   Long-term data storage

-   Point-in-time database snapshots

However native protection might not be enough if application errors, corruptions, or security and malware incidents occur. In these situations DPM provides a number of advantages:

-   Less DAGs are require - Native protection requires additional mailbox servers to host copies of active data. There's no reliance on DAGs for backup with DPM protection.

-   Simpler restore - DPM provides simple and centralized data recovery from point-in-time backups.

-   Longer retention range - DPM provides longer retention times for backed up data. Native protection is limited to 14 days.

-   Consistent backup of Microsoft workloads - DPM provides a centralized and simple backup and recovery process across your Microsoft workloads, including, Exchange, file servers, SQL Server, Hyper-V, and SharePoint.

## Before you start

1.  **Deploy DPM** - Verify that DPM is installed and deployed correctly. If you haven't see:

    -   System requirements for DPM

    -   [What can DPM back up?](../get-started/What-can-DPM-back-up-.md)

    -   [What's supported and what isn't for DPM?](../get-started/What-s-supported-and-what-isn-t-for-DPM-.md)

    -   [Get DPM installed](../get-started/Get-DPM-installed.md)

2.  Set up storage - You can store backed up data on disk, on tape, and in the cloud with Azure.  Read more in [Prepare data storage](../get-started/Prepare-data-storage.md).

3.  **Set up the DPM protection agent** - The agent needs to be installed on the Exchange server.  Read [Deploy the DPM protection agent](Deploy-the-DPM-protection-agent.md).

## Configure backup

1.  Click **Protection** > **Actions** > **Create Protection Group** to open the **Create New Protection Group** wizard in the DPM console.

2.  In **Select Protection Group Type** select **Servers**.

3.  In **Select Group Members** select all the DAGs that store data you want to protect. For each Exchange server you can also select to do a system state backup or full bare metal backup (which includes the system state. This in useful if you want the ability to recover your entire server and not just data.   [Deploy protection groups](Deploy-protection-groups.md).

4.  In **Select data protection method**  specify how you want to handle short and long-term backup. Short-term back up is always to disk first, with the option of backing up from the disk to the Azure cloud with Azure backup (for short or long-term). As an alternative to long-term backup to the cloud you can also configure long-term back up to a standalone tape device or tape library connected to the DPM server.

5.  In **Specify Exchange Protection Options** select **Run Eseutil** to check data integrity to check the integrity of the Exchange Server databases. This moves the backup consistency checking from the Exchange Server to the DPM server which means the I/O impact of running Eseutil.exe on the Exchange Server during the backup itself is eliminated. To protect a DAG, be sure that you select Run for log files only (Recommended for DAG servers). If you did not previously copy the .eseutil file an error will occur.

6.  In **Specify Exchange DAG Protection** select the databases you want to copy for either a full backup or copy backup from the **Database copies selected for Full Backup** or **Database copies selected for Copy Backup** list boxes. For protecting multiple copies of the same database, you can select only one copy for full backup, and then select the remaining copies for copy backup.

7.  In **Select short-term goals** specify how you want to back up to short-term storage on disk.   In **Retention range** you specify how long you want to keep the data on disk. In **Synchronization frequency** you specify how often you want to run an incremental backup to disk. If you don't want to set a back up interval you can check Just before  a recovery point so that DPM will run an express full backup just before each recovery point is scheduled.

8.  If you want to store data on tape for long-term storage in **Specify long-term goals** indicate how long you want to keep tape data (1-99 years). In Frequency of backup specify how often backups to tape should run. The frequency is based on the retention range you've specified:

    -   When the retention range is 1-99 years, you can select backups to occur daily, weekly, bi-weekly, monthly, quarterly, half-yearly, or yearly.

    -   When the retention range is 1-11 months, you can select backups to occur daily, weekly, bi-weekly, or monthly.

    -   When the retention range is 1-4 weeks, you can select backups to occur daily or weekly.

    On a stand-alone tape drive, for a single protection group, DPM uses the same tape for daily backups until there is insufficient space on the tape. You can also colocate data from different protection groups on tape.

    On the **Select Tape and Library Details** page specify the tape/library to use, and whether data should be compressed and encrypted on tape.

9.  In the **Review disk allocation** page, review the storage pool disk space allocated for the protection group.

    **Total Data size** is the size of the data you want to back up, and **Disk space to be provisioned on DPM** is the space that DPM recommends for the protection group. DPM chooses the ideal backup volume, based on the settings. However, you can edit the backup volume choices in the **Disk allocation details**. For the workloads, select the preferred storage in the dropdown menu. Your edits change the values for **Total Storage** and **Free Storage** in the **Available Disk Storage** pane. Underprovisioned space is the amount of storage DPM suggests you add to the volume, to continue with backups smoothly in the future.

10. In **Choose replica creation method** select how you want to handle the initial full data replication.  If you select to replicate over the network we recommended you choose an off-peak time. For large amounts of data or less than optimal network conditions, consider replicating the data offline using removable media.

11. In **Choose consistency check options**, select how you want to automate consistency checks. You can enable a check to run only when replica data becomes inconsistent, or according to a schedule. If you don't want to configure automatic consistency checking, you can run a manual check at any time by right-clicking the protection group in the **Protection** area of the DPM console, and selecting **Perform Consistency Check**.

12. If you've selected to back up to the cloud with Azure Backup, on the **Specify online protection data** page make sure the workloads you want to back up to Azure are selected.

13. In **Specify online backup schedule** specify how often incremental backups to Azure should occur. You can schedule backups to run every day/week/month/year and the time/date at which they should run. Backups can occur up to twice a day. Each time a back up runs a data recovery point is created in Azure from the copy of the backed up data stored on the DPM disk.

14. In **Specify online retention policy** you can specify how the recovery points created from the daily/weekly/monthly/yearly backups are retained in Azure.

15. In **Choose online replication** specify how the initial full replication of data will occur. You can replicate over the network, or do an offline backup (offline seeding). Offline backup uses the Azure Import feature. [Read more](https://azure.microsoft.com/documentation/articles/backup-azure-backup-import-export/).

16. On the  **Summary** page review your settings. After you click **Create Group** initial replication of the data occurs. When it finishes the protection group status will show as **OK** on the **Status** page. Backup then takes place in line with the protection group settings.

## Monitoring
After the protection group's been created the initial replication occurs and DPM starts backing up and synchronizing the Exchange data. DPM monitors the initial synchronization and subsequent backups. You can monitor the Exchange data in a couple of ways:

-   Using default DPM monitoring can set up notifications for proactive monitoring. by publishing alerts and configuring notifications. You can send notifications by e-mail for critical, warning, or informational alerts, and for the status of instantiated recoveries.

-   If you use Operations Manager you can centrally publish alerts.

#### Set up monitoring notifications

1.  In the DPM Administrator Console, click **Monitoring** > **Action** > **Options**.

2.  Click **SMTP Server**, type the server name, port, and email address from which notifications will be sent. The address must be valid.

3.  In **Authenticated SMTP server** , type a user name and password. The user name and password must be the domain account name of the person whose "From" address is described in the previous step; otherwise, notification delivery fails.

4.  To test the SMTP server settings, click **Send Test E-mail**, type the e-mail address where you want DPM to send the test message, and then click **OK**. Click **Options** > **Notifications** and select the types of alerts about which recipients want to be notified. In **Recipients** type the e-mail address for each recipient to whom you want DPM to send copies of the notifications.

5.  To test the SMTP server settings, click **Send Test Notification** > **OK**.

#### Publish alerts for Operations Manager

1.  In the DPM Administrator Console, click **Monitoring** > **Action** > **Options**.

2.  In Options click **Alert Publishing** > **Publish Active Alerts**.

3.  After you enable **Alert Publishing** all existing DPM alerts that might require a user action are published to the **DPM Alerts** event log. The Operations Manager agent that is installed on the DPM server then publishes these alerts to the Operations Manager and continues to update the console as new alerts are generated.

## Recover Exchange data

### <a name="BKMK_Single"></a>Recover a single mailbox

1.  On the protected Exchange server, verify whether you have an existing recovery mailbox database. If you don't, create one using the New-MailboxDatabase cmdlet. Configure the recovery database so it can be overwritten by using the Set-MailboxDatabase cmdlet. For example:

    ```
    New-MailboxDatabase -Recovery -Name RDB-CONTROL -Server E2K13-MBX1
    ```

    ```
    Set-MailboxDatabase -Identity 'RDB-CONTROL' -AllowFileRestore $true
    ```

2.  In the DPM Administrator Console, go to the **Recovery** view and navigate to the mailbox database you want to recover (in the **All Protectd Exchange Data** node).

3.  Available recovery points are indicated in bold on the calendar in the recovery points section. Click a date, select a recovery point in **Recovery time** > **Recover**.

    Note that you won't be able to select **Latest**. This isn't available for individual mailboxes.

4.  In the Recovery Wizard review your recovery selection, and click **Next**.

5.  Specify the type of recovery you would like to perform and click **Next**.

6.  In the **Specify Recovery Options** page do the following:

    1.  **Mount the databases after they are recovered**. Clear the check box if you don't want to mount the databases.

    2.  **Network bandwidth usage throttling**. Click **Modify** to enable throttling.

    3.  Click **Enable SAN-based recovery using hardware snapshots** if applicable.

    4.  In **Notification** click **Send an e-mail when the recovery completes**, and specify the recipients. Separate the e-mail addresses with commas.

7.  On the **Summary** page review your recovery settings, and click **Recover**. When the recovery finishes click **Close**.

    Any synchronization job for the selected recovery item is canceled while the recovery is in progress.

8.  After the recovery process has finished, the required mailbox is not quite fully restored. The mailbox database to which the mailbox belongs is only restored to the Recovery mailbox database. Restore the mailbox by running this cmdlet:

    ```
    New-MailboxRestoreRequest -SourceDatabase 'RDB-CONTROL' -SourceStoreMailbox 'mailbox name' -TargetMailbox <name>@contoso.com -TargetRootFolder Recovery -SkipMerging StorageProviderForSource
    ```

    You must add `\-SkipMerging StorageProviderForSource` to the command; otherwise an error occurs. For a workaround, see Release Notes for Exchange 2013.

    When you now open the `<mailbox name>` mailbox, all its contents until 3:15 PM are located beneath the Recovery folder.

9. After you finished the restore, you can dismount and delete the Recovery Mailbox database by running the following Windows PowerShell cmdlet.

    ```
    Remove-MailboxDatabase -Identity 'RDB-CONTROL'
    ```

### <a name="BKMK_DB"></a>Recover an Exchange database

-   In the DPM Administrator Console, go to the **Recovery** view and navigate to the mailbox database you want to recover (in the **All Protected Exchange Data** node).

-   Available recovery points are indicated in bold on the calendar in the recovery points section. Click a date, and select **Latest** to get the newest backup and click **Recover**.

-   In the Recovery Wizard review your recovery selection, and click **Next**.

-   Specify the type of recovery you would like to perform and click **Next**.

-   In the **Specify Recovery Options** page do the following:

    1.  **Mount the databases after they are recovered**. Select this.

    2.  **Network bandwidth usage throttling**. Click **Modify** to enable throttling.

    3.  Click **Enable SAN-based recovery using hardware snapshots** if applicable.

    4.  In **Notification** click **Send an e-mail when the recovery completes**, and specify the recipients. Separate the e-mail addresses with commas.

-   You must now return to the Exchange server in order to enable the databases to be overwritten by the restore. If you miss this step, the restore fails. To do this, open the Exchange admin center, navigate to  **Servers**> **Databases**, select the Exchange mailbox database that you want to be overwritten, and then click **Edit**.

    Click **Maintenance** > **This database can be overwritten by a restore** > **Save**.

-   Back in the Recovery Wizard on the **Summary** page review your recovery settings, and click **Recover**. When the recovery finishes click **Close**.

    Any synchronization job for the selected recovery item is canceled while the recovery is in progress.

-   Check your mailbox contents to verify the success of your restore operation. If the recovered mailbox database was part of a Database Availability Group (DAG), the passive copy shows the failed and suspended status.

-   To resume normal DAG operations, select the failed database copy, and then click **Resume**. A dialog box appears prompting you to reseed (or reset) the database. Click **Yes**.

### <a name="BKMK_Server"></a>Recover an entire Exchange server

-   In the DPM Administrator Console, go to the **Recovery** view and navigate to the server you want to recover.

-   Available recovery points are indicated in bold on the calendar in the recovery points section. Click a date, and select a recovery point from the list. In the list, right-click **Bare Metal Recovery** (BMR) and click **Recover**.

-   In the Recovery Wizard review your recovery selection, and click **Next**.

-   In the **Select Recovery Type** page, select **Copy to a network folder** to restore the server to a separate network location. Or you can select **Copy to tape** if you have one available.

-   In the **Specify Destination** page, select where you want to copy the database files. These files can be used to perform the BMR.

-   In the **Specify Recovery Options** page do the following:

    1.  **Mount the databases after they are recovered**. Select this.

    2.  **Network bandwidth usage throttling**. Click **Modify** to enable throttling.

    3.  Click **Enable SAN-based recovery using hardware snapshots** if applicable.

    4.  In **Notification** click **Send an e-mail when the recovery completes**, and specify the recipients. Separate the e-mail addresses with commas.

-   You can monitor the process on the **Monitoring** tab. A 'recovery success' alert shows when recovery finishes.

    Open the folder where are located recovery files and rename it with a shorter name. This will make the recovery process easier. Create a share in the recovery folder.

-   To run the bare metal recovery, insert the ISO of your operating system for boot purposes. Select the **Repair** option and in **Advanced Options**, select **System Image Recovery**.

    In the **Re-image your computer** wizard, you can ignore any warning about a system image not found.

-   In the **Select a system image backup** page, click **Select a system image**. Click **Advanced** to select recovery files from a network share. Select **Search for a system image on the network**and click **Yes**if asked if you're sure you want to connect to the network.

-   Specify the network folder, select the backup, and select the date and time of the image you want to restore. Specify any additional driver and disk settings, and then click **Finish**to start the restore.
