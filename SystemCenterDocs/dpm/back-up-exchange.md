---
description: This article explains how to back up Exchange mailbox databases with DPM.
ms.topic: how-to
author: Jeronika-MS
ms.author: v-gajeronika
ms.reviewer: v-gajeronika
ms.service: system-center
ms.date: 01/13/2026
title: Back up Exchange with DPM
ms.subservice: data-protection-manager
ms.assetid: 79fb8831-1d70-4d1d-bed1-f28fa9186730
ms.custom: engagement-fy23, engagement-fy24
ms.update-cycle: 1095-days
---

# Back up Exchange with DPM

::: moniker range="sc-dpm-2016"

System Center Data Protection Manager (DPM) provides backup and recovery for Exchange 2013 and Exchange 2016. To ensure your entire Exchange deployment is protected, configure protection for volumes, system state, or full bare metal recovery. This article provides the steps for configuring DPM so that you can protect your Exchange deployment. If you've a large Exchange deployment, use a database availability group (DAG) to scale protection for Exchange mailbox databases. In addition to backing up mail databases to fully protect your Exchange deployment, you should back up Exchange Server roles, such as the Client Access Server or the transport service on mailbox servers.

## Prerequisites and limitations

Before you deploy DPM to protect Exchange 2013 and Exchange 2016, verify the deployment prerequisites:

- Review the [DPM release notes](dpm-release-notes.md)

- Review the article, [What's supported and what isn't for DPM?](dpm-support-issues.md), for any Exchange issues.

- Ensure that the same versions of Eseutil.exe and Ese.dll are installed on both the Exchange and the DPM server. For example, if you're using the 64-bit version of DPM, you must have the 64-bit version of eseutil.exe and ese.dll. If you update these files on the Exchange server, you must update the files on the DPM server too. The `.ese` and `.eseutil` files are usually in the location, `C:\Program Files\Microsoft\Exchange Server\V15\Bin`.

    To maintain up-to-date copies:

    1. At the command prompt, navigate to the `<DPM installation folder>\Bin` directory.

    2. Enter the fsutil command as follows to create a hard link for eseutil.exe: `fsutil hardlink create <link> <target>`

        For example, in a typical installation, enter: `fsutil hardlink create "c:\program files\microsoft\dpm\bin\eseutil.exe" "c:\program files\microsoft\Exchange\bin\eseutil.exe"`

        > [!NOTE]
        > The *Eseutil* isn't forward or backward compatible. If you protect two different versions of Exchange Server database using a single DPM server, the integrity check will work only with the compatible version of *Eseutil* and it will fail for all other Exchange Server version. <br>To avoid this, we recommend you to use a separate DPM server for protecting each version of the Exchange Server with respective *Eseutil* version installed on the DPM server. If that isn't feasible, you need to turn on the integrity check for only one version of Exchange Server databases with the respective version of *Eseutil*.

- Install the latest [Visual C++ Redistributable for Visual Studio 2012 Update](https://www.microsoft.com/download/details.aspx?id=30679).

- To protect an Exchange 2013 and Exchange 2016 Database Availability Group (DAG) node, install the DPM protection agent on the node.

     > [!NOTE]
     > While you can protect different DAG nodes from different DPM servers, only one node can be protected by one DPM server only.

- DPM 2012 (and later) has a storage pool size limit of 120 terabytes (TB). There's an 80-TB limit for DPM replica volumes, and 40-TB limit for recovery point volumes. When protecting a large Exchange deployment, it's important to know the user mailbox size limit and the number of users or mailboxes. The number of users or mailboxes determines the maximum size of a mailbox. Provided the mailboxes stay within limits, the number of mailboxes determines the number of Exchange databases a single DPM can protect. Use the number of users assigned to a database and their mailbox limits to calculate the maximum size possible for each Exchange database. For example, if the maximum size of a user's mailbox is 8 GB, a single DPM server can protect up to 10,000 mailboxes. If the maximum size of a user's mailbox is greater than 8 GB or if more than 10,000 user mailboxes require protection, configure the Exchange server with a DAG. Use additional DPM servers to provide full protection. An Exchange node can only be protected by a single DPM server. Therefore, the number of Exchange nodes should be equal to or greater than the number of DPM servers required to protect all Exchange databases.

- DPM functions with any database role. You can configure DPM to protect a server that hosts a collection of active or passive mailbox databases.

- Configure one full backup per day and a synchronization frequency to suit your requirements for Exchange log truncations. When protecting more than one copy of an Exchange mailbox database (for example, when protecting members of a DAG), configure one node for full backups and the rest for copy backups. Copy backups don't truncate log files.

- Protect at least two copies of each mailbox database. You can use inexpensive Serial Advanced Technology Attachment (SATA) drives or several JBOD disks for storage.

- Set the minimum frequency to greater than 15 minutes for mailbox synchronization. Start by setting up your current backup policy and then gradually increase the number of recovery points. Performing one or two express full backups per day, in addition to a synchronization frequency of two hours, is a sound approach. For an optimal synchronization frequency, consider the volume of your data, the performance impact, and the volume required to store the replicas.

- Exchange 2013 and Exchange 2016 can support up to eight parallel backups. To accommodate parallel Exchange database backups for an Exchange server, create multiple protection groups (up to eight) and add Exchange databases to each protection group.

- As you maintain your Exchange data, note the following:

    - **Add mailbox databases to the server**. If you create or add new mailbox databases to a protected storage group on an Exchange server, these databases are automatically added to the DPMreplication and protection. You can add mailbox databases in incremental backups only after a full backup has finished.

    - **Change mailbox database file paths**. If you move a protected database or log files to a volume that contains data that is protected by DPM, the protection continues. If you move a protected database or log files to a volume that isn't protected by DPM, an alert appears and the protection jobs fail. To resolve the alert, in the alert details, select the **Modify protection job** link and then run a consistency check.

    - **Dismount mailbox databases**. If you dismount a protected mailbox database, the protection job for that particular database fails. The replica is marked inconsistent when DPM runs the next express full backup.

    - **Rename mailbox databases**. If you need to change the name of the mailbox database, stop the protection, and protect the database again. Until you protect the database again, the backups continue to work, but mailbox enumeration fails.

## Why back up Exchange with DPM?

When deciding whether to back up Exchange data with Exchange 2013 and Exchange 2016 native data protection or DPM, consider the following:

Native data protection provides:

- Disaster recovery

- Recovery of accidentally deleted items

- Long-term data storage

- Point-in-time database snapshots

Native protection might not be enough if application errors, corruptions, or security and malware incidents occur. In these situations, DPM provides a number of advantages:

- Fewer DAGs are required - Native protection requires additional mailbox servers to host copies of the active data. There's no reliance on DAGs for backup with DPM protection.

- Simpler restore - DPM provides simple and centralized data recovery from point-in-time backups.

- Longer retention range - DPM provides longer retention times for backed-up data. Native protection is limited to 14 days.

- Consistent backup of Microsoft workloads - DPM provides a centralized and simple backup and recovery process across your Microsoft workloads, including Exchange, file servers, SQL Server, Hyper-V, and SharePoint.

## Before you start

1. **Deploy DPM** - Verify that DPM is installed and deployed correctly. If you haven't, see:

    - System requirements for DPM

    - [What can DPM back up?](dpm-protection-matrix.md)

    - [What's supported and what isn't for DPM?](dpm-support-issues.md)

    - [Get DPM installed](install-dpm.md)

2. Set up storage - You can store backed-up data on disk, on tape, and in the cloud with Azure.  Read more in [Prepare data storage](plan-long-and-short-term-data-storage.md).

3. **Set up the DPM protection agent** - The agent must be installed on the Exchange server.  Read [Deploy the DPM protection agent](deploy-dpm-protection-agent.md).

## Configure backup

1. Select **Protection** > **Actions** > **Create Protection Group** to open the **Create New Protection Group** wizard in the DPM console.

2. In **Select Protection Group Type**, select **Servers**.

3. In **Select Group Members**, select all the DAGs that store data you want to protect. For each Exchange server, you can also select to do a system state backup or full bare metal backup (which includes the system state). This is useful if you want the ability to recover your entire server and not just the data. [Deploy protection groups](create-dpm-protection-groups.md).

4. In **Select data protection method**, specify how you want to handle short- and long-term backup. Short-term backup is always to disk first, with the option of backing up from the disk to the Azure cloud with Azure backup (for short- or long-term). As an alternative to long-term backup to the cloud, you can also configure long-term backup to a standalone tape device or tape library connected to the DPM server.

5. In **Specify Exchange Protection Options**, select **Run Eseutil** to check data integrity to check the integrity of the Exchange Server databases. This moves the backup consistency checking from the Exchange Server to the DPM server, which means the I/O impact of running Eseutil.exe on the Exchange Server during the backup itself is eliminated. To protect a DAG, ensure that you select Run for log files only (Recommended for DAG servers). If you didn't previously copy the .eseutil file, an error will occur.

6. In **Specify Exchange DAG Protection**, select the databases you want to copy for either a full backup or copy backup from the **Database copies selected for Full Backup** or **Database copies selected for Copy Backup** list boxes. For protecting multiple copies of the same database, you can select only one copy for full backup and then select the remaining copies for copy backup.

7. In **Select short-term goals**, specify how you want to back up to short-term storage on disk.   In **Retention range**, specify how long you want to keep the data on disk. In **Synchronization frequency**, specify how often you want to run an incremental backup to disk. If you don't want to set a backup interval, you can check **Just before a recovery point** so that DPM will run an express full backup just before each recovery point is scheduled.

8. If you want to store data on tape for long-term storage, in **Specify long-term goals**, indicate how long you want to keep tape data (1-99 years). In **Frequency of backup**, specify how often backups to tape should run. The frequency is based on the retention range you've specified:

    - When the retention range is 1-99 years, you can select backups to occur daily, weekly, bi-weekly, monthly, quarterly, half-yearly, or yearly.

    - When the retention range is 1-11 months, you can select backups to occur daily, weekly, bi-weekly, or monthly.

    - When the retention range is 1-4 weeks, you can select backups to occur daily or weekly.

    On a standalone tape drive, for a single protection group, DPM uses the same tape for daily backups until there's insufficient space on the tape. You can also colocate data from different protection groups on tape.

    On the **Select Tape and Library Details** page, specify the tape/library to use, and whether data should be compressed and encrypted on tape.

9. In the **Review disk allocation** page, review the storage pool disk space allocated for the protection group.

    **Total Data size** is the size of the data you want to back up, and **Disk space to be provisioned on DPM** is the space that DPM recommends for the protection group. DPM chooses the ideal backup volume based on the settings. However, you can edit the backup volume choices in the **Disk allocation details**. For the workloads, select the preferred storage in the dropdown menu. Your edits change the values for **Total Storage** and **Free Storage** in the **Available Disk Storage** pane. Underprovisioned space is the amount of storage DPM suggests you add to the volume to continue with backups smoothly in the future.

10. In **Choose replica creation method**, select how you want to handle the initial full data replication. If you select to replicate over the network, we recommend you choose an off-peak time. For large amounts of data or less than optimal network conditions, consider replicating the data offline using removable media.

11. In **Choose consistency check options**, select how you want to automate consistency checks. You can enable a check to run only when replica data becomes inconsistent or according to a schedule. If you don't want to configure automatic consistency checking, you can run a manual check at any time by right-clicking the protection group in the **Protection** area of the DPM console and selecting **Perform Consistency Check**.

12. If you've selected to back up to the cloud with Azure Backup, on the **Specify online protection data** page, ensure to select the workloads that you want to back up to Azure.

13. In **Specify online backup schedule**, specify how often incremental backups to Azure should occur. You can schedule backups to run every day/week/month/year and the time/date at which they should run. Backups can occur up to twice a day. Each time a backup runs, a data recovery point is created in Azure from the copy of the backed-up data stored on the DPM disk.

14. In **Specify online retention policy**, you can specify how the recovery points created from the daily/weekly/monthly/yearly backups are retained in Azure.

15. In **Choose online replication**, specify how the initial full replication of data will occur. You can replicate over the network or do an offline backup (offline seeding). Offline backup uses the Azure Import feature. [Read more](/azure/backup/backup-azure-backup-import-export).

16. On the  **Summary** page, review your settings. After you select **Create Group**, the initial replication of the data occurs. When it finishes, the protection group status will show as **OK** on the **Status** page. Backup then takes place in line with the protection group settings.

## Monitoring

After the protection group has been created, the initial replication occurs, and DPM starts backing up and synchronizing the Exchange data. DPM monitors the initial synchronization and subsequent backups. You can monitor the Exchange data in a couple of ways:

- Using default DPM monitoring can set up notifications for proactive monitoring by publishing alerts and configuring notifications. You can send notifications by email for critical, warning, or informational alerts, and for the status of instantiated recoveries.

- If you use Operations Manager, you can centrally publish alerts.

### Set up monitoring notifications

1. In the DPM Administrator Console, select **Monitoring** > **Action** > **Options**.

2. Select **SMTP Server**, enter the server name, port, and email address from which notifications will be sent. The address must be valid.

3. In **Authenticated SMTP server**, enter a username and password. The username and password must be the domain account name of the person whose **From** address is described in the previous step; otherwise, notification delivery fails.

4. To test the SMTP server settings, select **Send Test E-mail**, enter the email address where you want DPM to send the test message and then select **OK**. Select **Options** > **Notifications** and select the types of alerts about which recipients want to be notified. In **Recipients**, enter the email address for each recipient to whom you want DPM to send copies of the notifications.

5. To test the SMTP server settings, select **Send Test Notification** > **OK**.

### Publish alerts for Operations Manager

1. In the DPM Administrator Console, select **Monitoring** > **Action** > **Options**.

2. In **Options**, select **Alert Publishing** > **Publish Active Alerts**.

3. After you enable **Alert Publishing**, all the existing DPM alerts that might require a user action are published to the **DPM Alerts** event log. The Operations Manager agent that is installed on the DPM server then publishes these alerts to the Operations Manager and continues to update the console as new alerts are generated.

## Recover Exchange data

Select the required tab for steps to recover a single mailbox, an Exchange database, or an entire Exchange server:

# [A single mailbox](#tab/RecoverSingleMailbox)

Follow these steps to recover a single mailbox:

1. On the protected Exchange server, verify whether you've an existing recovery mailbox database. If you don't, create one using the New-MailboxDatabase cmdlet. Configure the recovery database so it can be overwritten by using the Set-MailboxDatabase cmdlet. For example:

    ```powershell
    New-MailboxDatabase -Recovery -Name RDB-CONTROL -Server E2K13-MBX1
    ```

    ```powershell
    Set-MailboxDatabase -Identity 'RDB-CONTROL' -AllowFileRestore $true
    ```

2. In the DPM Administrator Console, go to the **Recovery** view and navigate to the mailbox database you want to recover (in the **All Protected Exchange Data** node).

3. The available recovery points are indicated in bold on the calendar in the recovery points section. Select a date and select a recovery point in **Recovery time** > **Recover**.

    You won't be able to select **Latest**, as it isn't available for individual mailboxes.

4. In the Recovery Wizard, review your recovery selection, and select **Next**.

5. Specify the type of recovery you would like to perform and select **Next**.

6. In the **Specify Recovery Options** page, do the following:

    1. **Mount the databases after they are recovered**. Clear the checkbox if you don't want to mount the databases.

    2. **Network bandwidth usage throttling**. Select **Modify** to enable throttling.

    3. Select **Enable SAN-based recovery using hardware snapshots** if applicable.

    4. In **Notification**, select **Send an e-mail when the recovery completes** and specify the recipients. Separate the email addresses with commas.

7. On the **Summary** page, review your recovery settings and select **Recover**. When the recovery finishes, select **Close**.

    Any synchronization job for the selected recovery item is canceled while the recovery is in progress.

8. After the recovery process has finished, the required mailbox isn't fully restored. The mailbox database to which the mailbox belongs is only restored to the Recovery mailbox database. Restore the mailbox by running this cmdlet:

    ```powershell
    New-MailboxRestoreRequest -SourceDatabase 'RDB-CONTROL' -SourceStoreMailbox 'mailbox name' -TargetMailbox <name>@contoso.com -TargetRootFolder Recovery -SkipMerging StorageProviderForSource
    ```

    You must add `\-SkipMerging StorageProviderForSource` to the command; otherwise, an error occurs. For a workaround, see Release Notes for Exchange 2013 and Exchange 2016.

    When you now open the `<mailbox name>` mailbox, all its contents until 3:15 PM are located beneath the Recovery folder.

9. After you've finished the restore, you can dismount and delete the Recovery Mailbox database by running the following Windows PowerShell cmdlet.

    ```powershell
    Remove-MailboxDatabase -Identity 'RDB-CONTROL'
    ```

# [An Exchange database](#tab/RecoverExchangeDatabase)

Follow these steps to recover an Exchange database:

- In the DPM Administrator Console, go to the **Recovery** view and navigate to the mailbox database you want to recover (in the **All Protected Exchange Data** node).

- Available recovery points are indicated in bold on the calendar in the recovery points section. Select a date and select **Latest** to get the newest backup, and select **Recover**.

- In the Recovery Wizard, review your recovery selection and select **Next**.

- Specify the type of recovery you would like to perform and select **Next**.

- In the **Specify Recovery Options** page, do the following:

    1. **Mount the databases after they are recovered**. Select this.

    2. **Network bandwidth usage throttling**. Select **Modify** to enable throttling.

    3. Select **Enable SAN-based recovery using hardware snapshots** if applicable.

    4. In **Notification**, select **Send an e-mail when the recovery completes** and specify the recipients. Separate the email addresses with commas.

- You must now return to the Exchange server in order to enable the databases to be overwritten by the restore. If you miss this step, the restore fails. To do this, open the Exchange admin center, navigate to  **Servers**> **Databases**, select the Exchange mailbox database that you want to be overwritten, and then select **Edit**.

    Select **Maintenance** > **This database can be overwritten by a restore** > **Save**.

- Back in the Recovery Wizard, on the **Summary** page, review your recovery settings and select **Recover**. When the recovery finishes, select **Close**.

    Any synchronization job for the selected recovery item is canceled while the recovery is in progress.

- Check your mailbox contents to verify the success of your restore operation. If the recovered mailbox database was part of a Database Availability Group (DAG), the passive copy shows the failed and suspended status.

- To resume normal DAG operations, select the failed database copy, and then select **Resume**. A dialog appears prompting you to reseed (or reset) the database. Select **Yes**.

# [An entire Exchange server](#tab/RecoverExchangeServer)

Follow these steps to recover an entire Exchange server:

- In the DPM Administrator Console, go to the **Recovery** view and navigate to the server you want to recover.

- Available recovery points are indicated in bold on the calendar in the recovery points section. Select a date, and select a recovery point from the list. In the list, right-click **Bare Metal Recovery** (BMR) and select **Recover**.

- In the Recovery Wizard, review your recovery selection and select **Next**.

- In the **Select Recovery Type** page, select **Copy to a network folder** to restore the server to a separate network location. Or you can select **Copy to tape** if you've one available.

- In the **Specify Destination** page, select where you want to copy the database files. These files can be used to perform the BMR.

- In the **Specify Recovery Options** page, do the following:

    1. **Mount the databases after they are recovered**. Select this.

    2. **Network bandwidth usage throttling**. Select **Modify** to enable throttling.

    3. Select **Enable SAN-based recovery using hardware snapshots** if applicable.

    4. In **Notification**, select **Send an e-mail when the recovery completes** and specify the recipients. Separate the email addresses with commas.

- You can monitor the process on the **Monitoring** tab. A 'recovery success' alert shows when recovery finishes.

    Open the folder where recovery files are located and rename it with a shorter name. This will make the recovery process easier. Create a share in the recovery folder.

- To run the bare metal recovery, insert the ISO of your operating system for boot purposes. Select the **Repair** option, and in **Advanced Options**, select **System Image Recovery**.

    In the **Re-image your computer** wizard, you can ignore any warning about a system image not found.

- In the **Select a system image backup** page, select **Select a system image**. Select **Advanced** to select recovery files from a network share. Select **Search for a system image on the network** and select **Yes** when asked if you're sure you want to connect to the network.

- Specify the network folder, select the backup, and select the date and time of the image you want to restore. Specify any additional driver and disk settings, and then select **Finish** to start the restore.

---

::: moniker-end

::: moniker range=">=sc-dpm-2019"

System Center Data Protection Manager (DPM) provides backup and recovery for Exchange 2016 and Exchange 2019. To ensure that your entire Exchange deployment is protected, configure protection for volumes, system state, or full bare metal recovery. This article provides the steps for configuring DPM so that you can protect your Exchange deployment. If you've a large Exchange deployment, use a database availability group (DAG) to scale protection for Exchange mailbox databases. In addition to backing up mail databases, to fully protect your Exchange deployment, you should back up Exchange Server roles such as the Client Access Server or the transport service on mailbox servers.

## Prerequisites and limitations

Before you deploy DPM to protect Exchange 2016 and Exchange 2019, verify the deployment prerequisites:

- Review the [DPM release notes](dpm-release-notes.md)

- Review the article, [What's supported and what isn't for DPM?](dpm-support-issues.md), for any Exchange issues.

- Ensure that the same versions of Eseutil.exe and Ese.dll are installed on both the Exchange and the DPM server. For example, if you're using the 64-bit version of DPM, you must have the 64-bit version of eseutil.exe and ese.dll. If you update these files on the Exchange server, you must update the files on the DPM server too. The `.ese` and `.eseutil` files are usually in the location, `C:\Program Files\Microsoft\Exchange Server\V15\Bin`.

    To maintain up-to-date copies:

    1. At the command prompt, navigate to the `<DPM installation folder>\Bin` directory.

    2. Enter the fsutil command as follows to create a hard link for eseutil.exe: `fsutil hardlink create <link> <target>`

        For example, in a typical installation, enter: `fsutil hardlink create "c:\program files\microsoft\dpm\bin\eseutil.exe" "c:\program files\microsoft\Exchange\bin\eseutil.exe"`

    > [!NOTE]
    > The *Eseutil* isn't forward or backward compatible. If you protect two different versions of Exchange Server database using a single DPM server, the integrity check will work only with the compatible version of *Eseutil* and it will fail for all other Exchange Server versions.<br>
    To avoid this, we recommend you to use a separate DPM server for protecting each version of Exchange Server with respective *Eseutil* version installed on the DPM server. If that isn't feasible, you need to turn on the integrity check for only one version of Exchange Server databases with the respective version of *Eseutil*.

- Install the latest [Visual C++ Redistributable for Visual Studio 2012 Update](https://www.microsoft.com/download/details.aspx?id=30679).

- To protect an Exchange 2016 and Exchange 2019 Database Availability Group (DAG) node, install the DPM protection agent on the node.

> [!NOTE]
> While you can protect different DAG nodes from different DPM servers, only one node can be protected by one DPM server only.

::: moniker-end

::: moniker range="sc-dpm-2019"

- DPM 2012 (and later) has a storage pool size limit of 120 terabytes (TB). There's an 80-TB limit for DPM replica volumes, and 40-TB limit for recovery point volumes. When protecting a large Exchange deployment, it's important to know the user mailbox size limit and the number of users or mailboxes. The number of users or mailboxes determines the maximum size of a mailbox. Provided the mailboxes stay within limits, the number of mailboxes determines the number of Exchange databases a single DPM can protect. Use the number of users assigned to a database and their mailbox limits to calculate the maximum size possible for each Exchange database. For example, if the maximum size of a user's mailbox is 8 GB, a single DPM server can protect up to 10,000 mailboxes. If the maximum size of a user mailbox is greater than 8 GB or if more than 10,000 user mailboxes require protection, configure the Exchange server with a DAG. Use additional DPM servers to provide full protection. An Exchange node can only be protected by a single DPM server. Therefore, the number of Exchange nodes should be equal to or greater than the number of DPM servers required to protect all Exchange databases.

::: moniker-end

::: moniker range=">=sc-dpm-2019"

- DPM functions with any database role. You can configure DPM to protect a server that hosts a collection of active or passive mailbox databases.

- Configure one full backup per day and a synchronization frequency to suit your requirements for Exchange log truncations. When protecting more than one copy of an Exchange mailbox database (for example, when protecting members of a DAG), configure one node for full backups and the rest for copy backups. Copy backups don't truncate log files.

- Protect at least two copies of each mailbox database. You can use inexpensive Serial Advanced Technology Attachment (SATA) drives or several JBOD disks for storage.

- Set the minimum frequency to greater than 15 minutes for mailbox synchronization. Start by setting up your current backup policy and then gradually increase the number of recovery points. Performing one or two express full backups per day in addition to a synchronization frequency of two hours is a sound approach. For an optimal synchronization frequency, consider the volume of your data, the performance impact, and the volume required to store the replicas.

- Exchange 2016 and Exchange 2019 can support up to eight parallel backups. To accommodate parallel Exchange database backups for an Exchange server, create multiple protection groups (up to eight) and add Exchange databases to each protection group.

- As you maintain your Exchange data, note the following:

    - **Add mailbox databases to the server**. If you create or add new mailbox databases to a protected storage group on an Exchange server, these databases are automatically added to the DPMreplication and protection. You can add mailbox databases in incremental backups only after a full backup has finished.

    - **Change mailbox database file paths**. If you move a protected database or log files to a volume that contains data that is protected by DPM, the protection continues. If you move a protected database or log files to a volume that isn't protected by DPM, an alert appears and the protection jobs fail. To resolve the alert, in the alert details, select the **Modify protection job** link and then run a consistency check.

    - **Dismount mailbox databases**. If you dismount a protected mailbox database, the protection job for that particular database fails. The replica is marked inconsistent when DPM runs the next express full backup.

    - **Rename mailbox databases**. If you need to change the name of the mailbox database, stop the protection and protect the database again. Until you protect the database again, the backups continue to work, but mailbox enumeration fails.

## Why back up Exchange with DPM?

When deciding whether to back up Exchange data with Exchange 2016 and Exchange 2019 native data protection or DPM, consider the following:

Native data protection provides:

- Disaster recovery

- Recovery of accidentally deleted items

- Long-term data storage

- Point-in-time database snapshots

Native protection might not be enough if application errors, corruptions, or security and malware incidents occur. In these situations, DPM provides the following advantages:

- Fewer DAGs are required - Native protection requires additional mailbox servers to host copies of the active data. There's no reliance on DAGs for backup with DPM protection.

- Simpler restore - DPM provides simple and centralized data recovery from point-in-time backups.

- Longer retention range - DPM provides longer retention times for backed-up data. Native protection is limited to 14 days.

- Consistent backup of Microsoft workloads - DPM provides a centralized and simple backup and recovery process across your Microsoft workloads, including Exchange, file servers, SQL Server, Hyper-V, and SharePoint.

## Before you start

1. **Deploy DPM** - Verify that DPM is installed and deployed correctly. If you haven't, see:

    - System requirements for DPM

    - [What can DPM back up?](dpm-protection-matrix.md)

    - [What's supported and what isn't for DPM?](dpm-support-issues.md)

    - [Get DPM installed](install-dpm.md)

2. Set up storage - You can store backed-up data on disk, on tape, and in the cloud with Azure. Read more in [Prepare data storage](plan-long-and-short-term-data-storage.md).

3. **Set up the DPM protection agent** - The agent must be installed on the Exchange server. Read [Deploy the DPM protection agent](deploy-dpm-protection-agent.md).

## Configure backup

1. Select **Protection** > **Actions** > **Create Protection Group** to open the **Create New Protection Group** wizard in the DPM console.

2. In **Select Protection Group Type**, select **Servers**.

3. In **Select Group Members**, select all the DAGs that store data you want to protect. For each Exchange server, you can also select to do a system state backup or full bare metal backup (which includes the system state). This is useful if you want the ability to recover your entire server and not just data. [Deploy protection groups](create-dpm-protection-groups.md).

4. In **Select data protection method**, specify how you want to handle short- and long-term backup. Short-term backup is always to disk first, with the option of backing up from the disk to the Azure cloud with Azure backup (for short- or long-term). As an alternative to long-term backup to the cloud, you can also configure long-term back up to a standalone tape device or tape library connected to the DPM server.

5. In **Specify Exchange Protection Options**, select **Run Eseutil** to check data integrity to check the integrity of the Exchange Server databases. This moves the backup consistency checking from the Exchange Server to the DPM server, which means the I/O impact of running Eseutil.exe on the Exchange Server during the backup itself is eliminated. To protect a DAG, ensure that you select Run for log files only (Recommended for DAG servers). If you didn't previously copy the .eseutil file, an error will occur.

6. In **Specify Exchange DAG Protection**, select the databases you want to copy for either a full backup or copy backup from the **Database copies selected for Full Backup** or **Database copies selected for Copy Backup** list boxes. For protecting multiple copies of the same database, you can select only one copy for full backup and then select the remaining copies for copy backup.

7. In **Select short-term goals**, specify how you want to back up to short-term storage on disk. In **Retention range**, specify how long you want to keep the data on disk. In **Synchronization frequency**, specify how often you want to run an incremental backup to disk. If you don't want to set a backup interval, you can check **Just before a recovery point** so that DPM will run an express full backup just before each recovery point is scheduled.

8. If you want to store data on tape for long-term storage, in **Specify long-term goals**, indicate how long you want to keep tape data (1-99 years). In Frequency of backup, specify how often backups to tape should run. The frequency is based on the retention range you've specified:

    - When the retention range is 1-99 years, you can select backups to occur daily, weekly, bi-weekly, monthly, quarterly, half-yearly, or yearly.

    - When the retention range is 1-11 months, you can select backups to occur daily, weekly, bi-weekly, or monthly.

    - When the retention range is 1-4 weeks, you can select backups to occur daily or weekly.

    On a standalone tape drive, for a single protection group, DPM uses the same tape for daily backups until there's insufficient space on the tape. You can also colocate data from different protection groups on tape.

    On the **Select Tape and Library Details** page, specify the tape/library to use and whether data should be compressed and encrypted on tape.

9. In the **Review disk allocation** page, review the storage pool disk space allocated for the protection group.

    **Total Data size** is the size of the data you want to back up, and **Disk space to be provisioned on DPM** is the space that DPM recommends for the protection group. DPM chooses the ideal backup volume based on the settings. However, you can edit the backup volume choices in the **Disk allocation details**. For the workloads, select the preferred storage in the dropdown menu. Your edits change the values for **Total Storage** and **Free Storage** in the **Available Disk Storage** pane. Underprovisioned space is the amount of storage DPM suggests you add to the volume to continue with backups smoothly in the future.

10. In **Choose replica creation method**, select how you want to handle the initial full data replication. If you select to replicate over the network, we recommend you choose an off-peak time. For large amounts of data or less than optimal network conditions, consider replicating the data offline using removable media.

11. In **Choose consistency check options**, select how you want to automate consistency checks. You can enable a check to run only when replica data becomes inconsistent or according to a schedule. If you don't want to configure automatic consistency checking, you can run a manual check at any time by right-clicking the protection group in the **Protection** area of the DPM console and selecting **Perform Consistency Check**.

12. If you've selected to back up to the cloud with Azure Backup, on the **Specify online protection data** page, ensure to select the workloads that you want to back up to Azure.

13. In **Specify online backup schedule**, specify how often incremental backups to Azure should occur. You can schedule backups to run every day/week/month/year and the time/date at which they should run. Backups can occur up to twice a day. Each time a backup runs, a data recovery point is created in Azure from the copy of the backed-up data stored on the DPM disk.

14. In **Specify online retention policy**, you can specify how the recovery points created from the daily/weekly/monthly/yearly backups are retained in Azure.

15. In **Choose online replication**, specify how the initial full replication of data will occur. You can replicate over the network or do an offline backup (offline seeding). Offline backup uses the Azure Import feature. [Read more](/azure/backup/backup-azure-backup-import-export).

16. On the **Summary** page, review your settings. After you select **Create Group**, the initial replication of the data occurs. When it finishes the protection, the group status will show as **OK** on the **Status** page. Backup then takes place in line with the protection group settings.

## Monitoring

After the protection group has been created, the initial replication occurs and DPM starts backing up and synchronizing the Exchange data. DPM monitors the initial synchronization and subsequent backups. You can monitor the Exchange data in a couple of ways:

- Using default DPM monitoring, you can set up notifications for proactive monitoring by publishing alerts and configuring notifications. You can send notifications by email for critical, warning, or informational alerts, and for the status of instantiated recoveries.

- If you use Operations Manager, you can centrally publish alerts.

#### Set up monitoring notifications

1. In the DPM Administrator Console, select **Monitoring** > **Action** > **Options**.

2. Select **SMTP Server**, enter the server name, port, and email address from which notifications will be sent. The address must be valid.

3. In **Authenticated SMTP server**, enter a username and password. The username and password must be the domain account name of the person whose **From** address is described in the previous step; otherwise, notification delivery fails.

4. To test the SMTP server settings, select **Send Test E-mail**, enter the email address where you want DPM to send the test message, and then select **OK**. Select **Options** > **Notifications** and select the types of alerts about which recipients want to be notified. In **Recipients**, enter the email address for each recipient to whom you want DPM to send copies of the notifications.

5. To test the SMTP server settings, select **Send Test Notification** > **OK**.

#### Publish alerts for Operations Manager

1. In the DPM Administrator Console, select **Monitoring** > **Action** > **Options**.

2. In Options, select **Alert Publishing** > **Publish Active Alerts**.

3. After you enable **Alert Publishing**, all the existing DPM alerts that might require a user action are published to the **DPM Alerts** event log. The Operations Manager agent that is installed on the DPM server then publishes these alerts to the Operations Manager and continues to update the console as new alerts are generated.

## Recover Exchange data

Select the required tab for steps to recover a single mailbox, an Exchange database, or an entire Exchange server:

# [Recover a single mailbox](#tab/SingleMailbox)

Follow these steps to recover a single mailbox:

1. On the protected Exchange server, verify whether you've an existing recovery mailbox database. If you don't, create one using the New-MailboxDatabase cmdlet. Configure the recovery database so it can be overwritten by using the Set-MailboxDatabase cmdlet. For example:

    ```powershell
    New-MailboxDatabase -Recovery -Name RDB-CONTROL -Server E2K13-MBX1
    ```

    ```powershell
    Set-MailboxDatabase -Identity 'RDB-CONTROL' -AllowFileRestore $true
    ```

2. In the DPM Administrator Console, go to the **Recovery** view and navigate to the mailbox database you want to recover (in the **All Protected Exchange Data** node).

3. Available recovery points are indicated in bold on the calendar in the recovery points section. Select a date and select a recovery point in **Recovery time** > **Recover**.

    You won't be able to select **Latest**, as it isn't available for individual mailboxes.

4. In the Recovery Wizard, review your recovery selection and select **Next**.

5. Specify the type of recovery you would like to perform and select **Next**.

6. In the **Specify Recovery Options** page, do the following:

    1. **Mount the databases after they are recovered**. Clear the checkbox if you don't want to mount the databases.

    2. **Network bandwidth usage throttling**. Select **Modify** to enable throttling.

    3. Select **Enable SAN-based recovery using hardware snapshots** if applicable.

    4. In **Notification**, select **Send an e-mail when the recovery completes** and specify the recipients. Separate the email addresses with commas.

7. On the **Summary** page, review your recovery settings and select **Recover**. When the recovery finishes, select **Close**.

    Any synchronization job for the selected recovery item is canceled while the recovery is in progress.

8. After the recovery process has finished, the required mailbox isn't fully restored. The mailbox database to which the mailbox belongs is only restored to the Recovery mailbox database. Restore the mailbox by running this cmdlet:

    ```powershell
    New-MailboxRestoreRequest -SourceDatabase 'RDB-CONTROL' -SourceStoreMailbox 'mailbox name' -TargetMailbox <name>@contoso.com -TargetRootFolder Recovery -SkipMerging StorageProviderForSource
    ```

    You must add `\-SkipMerging StorageProviderForSource` to the command; otherwise, an error occurs. For a workaround, see Release Notes for Exchange 2016 and Exchange 2019.

    When you now open the `<mailbox name>` mailbox, all its contents until 3:15 PM are located beneath the Recovery folder.

9. After you've finished the restore, you can dismount and delete the Recovery Mailbox database by running the following Windows PowerShell cmdlet.

    ```powershell
    Remove-MailboxDatabase -Identity 'RDB-CONTROL'
    ```

# [Recover an Exchange database](#tab/ExchangeDatabase)

Follow these steps to recover an Exchange database:

- In the DPM Administrator Console, go to the **Recovery** view and navigate to the mailbox database you want to recover (in the **All Protected Exchange Data** node).

- Available recovery points are indicated in bold on the calendar in the recovery points section. Select a date and select **Latest** to get the newest backup and select **Recover**.

- In the Recovery Wizard, review your recovery selection and select **Next**.

- Specify the type of recovery you would like to perform and select **Next**.

- In the **Specify Recovery Options** page, do the following:

    1. **Mount the databases after they are recovered**. Select this.

    2. **Network bandwidth usage throttling**. Select **Modify** to enable throttling.

    3. Select **Enable SAN-based recovery using hardware snapshots** if applicable.

    4. In **Notification**, select **Send an e-mail when the recovery completes** and specify the recipients. Separate the email addresses with commas.

- You must now return to the Exchange server in order to enable the databases to be overwritten by the restore. If you miss this step, the restore fails. To do this, open the Exchange admin center, navigate to **Servers**> **Databases**, select the Exchange mailbox database that you want to be overwritten, and then select **Edit**.

    Select **Maintenance** > **This database can be overwritten by a restore** > **Save**.

- Back in the Recovery Wizard, on the **Summary** page, review your recovery settings and select **Recover**. When the recovery finishes, select **Close**.

    Any synchronization job for the selected recovery item is canceled while the recovery is in progress.

- Check your mailbox contents to verify the success of your restore operation. If the recovered mailbox database was part of a Database Availability Group (DAG), the passive copy shows the failed and suspended status.

- To resume normal DAG operations, select the failed database copy, and then select **Resume**. A dialog appears prompting you to reseed (or reset) the database. Select **Yes**.

# [Recover an entire Exchange server](#tab/EntireExchangeServer)

Follow these steps to recover an entire Exchange server:

- In the DPM Administrator Console, go to the **Recovery** view and navigate to the server you want to recover.

- Available recovery points are indicated in bold on the calendar in the recovery points section. Select a date and select a recovery point from the list. In the list, right-click **Bare Metal Recovery** (BMR) and select **Recover**.

- In the Recovery Wizard, review your recovery selection and select **Next**.

- In the **Select Recovery Type** page, select **Copy to a network folder** to restore the server to a separate network location. Or you can select **Copy to tape** if you've one available.

- In the **Specify Destination** page, select where you want to copy the database files. These files can be used to perform the BMR.

- In the **Specify Recovery Options** page, do the following:

    1. **Mount the databases after they are recovered**. Select this.

    2. **Network bandwidth usage throttling**. Select **Modify** to enable throttling.

    3. Select **Enable SAN-based recovery using hardware snapshots** if applicable.

    4. In **Notification**, select **Send an e-mail when the recovery completes** and specify the recipients. Separate the email addresses with commas.

- You can monitor the process on the **Monitoring** tab. A 'recovery success' alert shows when the recovery finishes.

    Open the folder where  recovery files are located and rename it with a shorter name. This will make the recovery process easier. Create a share in the recovery folder.

- To run the bare metal recovery, insert the ISO of your operating system for boot purposes. Select the **Repair** option, and in **Advanced Options**, select **System Image Recovery**.

    In the **Re-image your computer** wizard, you can ignore any warning about a system image not found.

- In the **Select a system image backup** page, select **Select a system image**. Select **Advanced** to select recovery files from a network share. Select **Search for a system image on the network** and select **Yes** when asked if you're sure you want to connect to the network.

- Specify the network folder, select the backup, and select the date and time of the image you want to restore. Specify any additional driver and disk settings, and then select **Finish** to start the restore.

---

::: moniker-end
