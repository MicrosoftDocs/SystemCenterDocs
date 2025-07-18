---
description: You can use DPM to back up your system state and provide bare metal recovery (BMR) protection.
ms.topic: how-to
ms.service: system-center
keywords:
ms.date: 03/27/2025
title: Back up system state and bare metal
ms.subservice: data-protection-manager
ms.assetid: 7035095c-6d30-40aa-ae73-4159e305d7ea
author: jyothisuri
ms.author: jsuri
ms.custom: engagement-fy23, UpdateFrequency2, engagement-fy24
---

# Back up system state and bare metal

System Center Data Protection Manager (DPM) can back up system state and provide bare metal recovery (BMR) protection.

- **System state backup**:  Backs up operating system files, enabling you to recover when a machine starts but you've lost system files and registry. A system state backup includes:

    - Domain member: Boot files, COM+ class registration database, registry

    - Domain controller: Active Directory (NTDS), boot files, COM+ class registration database, registry, system volume (sysvol folder)

    - Machine running cluster services: Additionally backs up cluster server metadata

    - Machine running certificate services: Additionally backs up certificate data

- **Bare metal backup**: Backs up operating system files and all data except user data not located on critical volumes. By definition, a BMR backup includes a system state backup. It provides protection when a machine won't start and you have to recover everything.

This table summarizes what you can back up and recover. You can see detailed information about app versions that can be protected with system state and BMR in [What can DPM back up?](dpm-protection-matrix.md)

|Backup|Issue|Recover from DPM backup|Recover from system state backup|BMR|
|----------|---------|---------------------------|------------------------------------|-------|
|**File data**<br /><br />Regular data backup<br /><br />BMR/system state backup|Lost file data|Y|N|N|
|**File data**<br /><br />DPM backup of file data<br /><br />BMR/system state backup|Lost/damaged operating system|N|Y|Y|
|**File data**<br /><br />DPM backup of file data<br /><br />BMR/system state backup|Lost server (data volumes intact)|N|N|Y|
|**File data**<br /><br />DPM backup of file data<br /><br />BMR/system state backup|Lost server (data volumes lost)|Y|No|Yes (BMR followed by regular recovery of backed up file data)|
|**SharePoint data**:<br /><br />DPM backup of farm data<br /><br />BMR/system state backup|Lost site, lists, list items. documents|Y|N|N|
|**SharePoint data**:<br /><br />DPM backup of farm data<br /><br />BMR/system state backup|Lost or damaged operating system|N|Y|Y|
|**SharePoint data**:<br /><br />DPM backup of farm data<br /><br />BMR/system state backup|Disaster recovery|N|N|N|
|Hyper-V<br /><br />DPM backup of Hyper-V host or guest<br /><br />BMR/system state backup of host|Lost VM|Y|N|N|
|Hyper-V<br /><br />DPM backup of Hyper-V host or guest<br /><br />BMR/system state backup of host|Lost or damaged operating system|N|Y|Y|
|Hyper-V<br /><br />DPM backup of Hyper-V host or guest<br /><br />BMR/system state backup of host|Lost Hyper-V host (VMs intact)|N|N|Y|
|Hyper-V<br /><br />DPM backup of Hyper-V host or guest<br /><br />BMR/system state backup of host|Lost Hyper-V host (VMs lost)|N|N|Y<br /><br />BMR recovery followed by regular DPM recovery|
|SQL Server/Exchange<br /><br />DPM app backup<br /><br />BMR/system state backup|Lost app data|Y|N|N|
|SQL Server/Exchange<br /><br />DPM app backup<br /><br />BMR/system state backup|Lost or damaged operating system|N|Y|Y|
|SQL Server/Exchange<br /><br />DPM app backup<br /><br />BMR/system state backup|Lost server (database/transaction logs intact)|N|N|Y|
|SQL Server/Exchange<br /><br />DPM app backup<br /><br />BMR/system state backup|Lost server (database/transaction logs lost)|N|N|Y<br /><br />BMR recovery followed by regular DPM recovery|

## System state backup workflow

1. When a system state backup runs, DPM communicates with WSB to request a backup of the server's system state. By default DPM and WSB will use the drive with the most available free space, and information about this drive is saved in the PSDataSourceConfig.XML file. WSB will use this drive for backups.

2. You can customize the drive that DPM uses for the system state backup. To do this on the protected server, go to *drive*:\Program Files\Microsoft Data Protection Manager\DPM\Datasources. Open the PSDataSourceConfig.XML file for editing. Change the \<FilesToProtect\> value for the drive letter. Save and close the file. If a protection group protects the computer's system state, run a consistency check. If the consistency check generates an alert, select **Modify protection group** link in the alert, and then step through the wizard. After finishing, run another consistency check.

3. If the protection server is in a cluster, it's possible that a cluster drive will be selected as the drive with the most free space. It's important to be aware of this because if that drive ownership has been switched to another node and a system state backup runs, the drive won't be available and the backup will fail. In this situation, you'll need to modify the PSDataSourceConfig.XML to point it to a local drive.

4. Windows Server Backup (WSB) creates a folder called WindowsImageBackup on the root of the volume. As it creates the backup, all data is placed in this folder. When the backup completes, the file will then be transferred over to the DPM server.

    > [!NOTE]
    > - This folder and its contents don't get cleaned up after the backup or transfer is done. The best way to think of this is that the space is being reserved for the next time a backup is done.
    > - The folder gets created every time a backup is done. The time/date stamp will reflect the time of your last system state backup.

## BMR backup

1. For BMR (including a system state backup), the backup job is performed directly to a share on the DPM server and not to a folder on the protected server.

2. DPM server calls WSB and shares out the replica volume for that BMR backup. In this case, it doesn't tell WSB to use the drive with the most free space, but instead to use the share created for the job.

3. When the backup finishes, the file is transferred to the DPM server. Logs are stored in *C:\Windows\Logs\WindowsServerBackup*.

## Prerequisites and limitations

- BMR isn't supported for computers running client operating systems.

- You can't protect BMR and system state for the same computer in different protection groups.

- A DPM server can't protect itself for BMR.

- Short-term protection to tape (D2T) isn't supported for BMR. Long-term storage to tape (D2D2T) is supported.

- Windows Server Backup must be installed on the protected computer for BMR.

- For BMR protection (unlike system state protection), DPM doesn't have any space requirements on the protected computer. WSB directly transfers the backups to the DPM server. The job for this doesn't appear in the DPM Jobs view.


::: moniker range=">=sc-dpm-2019"


- DPM reserves 20 GB of space for the replica volume for BMR backup.

- If you use Modern Backup Storage and want to increase the BMR default replica size > 20 GB, use the registry key to increase it before protection: `HKLM\Software\Microsoft\Microsoft Data Protection Manager\Configuration ReplicaSizeInGBForSystemProtectionWithBMR (DWORD)`.

::: moniker-end

::: moniker range="sc-dpm-2025"

- If you use Modern Backup Storage, SystemState and BMR backups consume more storage (than legacy storage) due to ReFS cloning. Each SystemState or BMR backup is a full recovery point. To mitigate this storage consumption, you may want to:
  - schedule fewer System State or BMR recovery points,
  - use a smaller retention period for the recovery points,
  - increase the available storage for System State or BMR backups. 

    > [!NOTE]
    > You can't reduce the replica volume size to less than 15 GB. DPM doesn't calculate the size of BMR data source but reserves 20 GB for each server. Admins should change the registry value `ReplicaSizeInGBForSystemProtectionWithBMR` as per the size of BMR backups expected on their environments. The size of a BMR backup can be roughly calculated as the sum of used space on all critical volumes: Critical volumes = Boot Volume + System Volume + Volume hosting system state data such as AD. 

::: moniker-end

::: moniker range=">=sc-dpm-2019 <=sc-dpm-2022"

- If you use Modern Backup Storage, SystemState and BMR backups consume more storage (than legacy storage) due to ReFS cloning. Each SystemState or BMR backup is a full recovery point. To mitigate this storage consumption, you may want to:
  - schedule fewer System State or BMR recovery points,
  - use a smaller retention period for the recovery points,
  - increase the available storage for System State or BMR backups. 

    > [!NOTE]
    > You can't reduce the replica volume size to less than 15 GB. DPM doesn't calculate the size of BMR data source but reserves 20 GB for each server. Admins should change the registry value `ReplicaSizeInGBForSystemProtectionWithBMR` as per the size of BMR backups expected on their environments. The size of a BMR backup can be roughly calculated as the sum of used space on all critical volumes: Critical volumes = Boot Volume + System Volume + Volume hosting system state data such as AD. 

    > [!NOTE]
    > You can't reduce the replica volume size to less than 15 GB. DPM doesn't calculate the size of BMR data source but assumes 30 GB for all servers. Admins should change the value as per the size of BMR backups expected on their environments. The size of a BMR backup can be roughly calculated as the sum of used space on all critical volumes: Critical volumes = Boot Volume + System Volume + Volume hosting system state data such as AD. Process System state backup

::: moniker-end 

::: moniker range="sc-dpm-2016"

- If you use Modern Backup Storage and want to increase the BMR default replica size > 30 GB, use the registry key: `HKLM\Software\Microsoft\Microsoft Data Protection Manager\Configuration ReplicaSizeInGBForSystemProtectionWithBMR (DWORD)`.

- If you use Modern Backup Storage, SystemState and BMR backups consume more storage (than legacy storage) due to ReFS cloning. Each SystemState or BMR backup is a full recovery point. To mitigate this storage consumption, you may want to:
  - schedule fewer System State or BMR recovery points,
  - use a smaller retention period for the recovery points,
  - increase the available storage for System State or BMR backups. 

> [!NOTE]
> The following limitations don't apply to Modern Backup Storage (MBS). The following limitations apply only when using legacy storage after upgrading DPM 2012 R2 to DPM 2016.


- DPM reserves 30 GB of space on the replica volume for BMR. You can change this on the Disk Allocation page in the Modify Protection Group Wizard or using the Get-DatasourceDiskAllocation and Set-DatasourceDiskAllocation PowerShell cmdlets. On the recovery point volume, BMR protection requires about 6 GB for retention of five days.

     > [!NOTE]
     > You can't reduce the replica volume size to less than 15 GB. DPM doesn't calculate the size of BMR data source but assumes 30 GB for all servers. Admins should change the value as per the size of BMR backups expected on their environments. The size of a BMR backup can be roughly calculated as the sum of used space on all critical volumes: Critical volumes = Boot Volume + System Volume + Volume hosting system state data such as AD. Process System state backup

- If you move from system state protection to BMR protection, BMR protection will require less space on the **recovery point volume.** However, the extra space on the volume isn't reclaimed. You can shrink the volume size manually from the **Modify Disk Allocation** page of the **Modify Protection Group Wizard** or using the Get-DatasourceDiskAllocation and Set-DatasourceDiskAllocation cmdlets.

    If you move from system state protection to BMR protection, BMR protection will require more space on the **replica volume**. The volume will be extended automatically. If you want to change the default space allocations, you can use Modify-DiskAllocation.

- If you move from BMR protection to system state protection, you'll need more space on the recovery point volume. DPM might try to automatically grow the volume. If there's insufficient space in the storage pool, an error will be issued.

    If you move from BMR protection to system state protection, you'll need space on the protected computer because system state protection first writes the replica to the local computer and then transfers it to the DPM server

::: moniker-end

::: moniker range=">=sc-dpm-2019"

- If you move from system state protection to BMR protection, BMR protection requires more space. The replica volume extends automatically. If you want to change the default space allocations, you can use **ReplicaSizeInGBForSystemProtectionWithBMR** registry entry.

- If you move from BMR protection to system state protection, you need space on the protected computer because system state protection first writes the replica to the local computer and then transfers it to the DPM server.

::: moniker-end

## Before you start

1. **Deploy DPM**: Verify DPM is deployed correctly. If you haven't, see:

    - System requirements for DPM

    - [What can DPM back up?](dpm-protection-matrix.md)

    - [What's supported and what isn't for DPM?](dpm-support-issues.md)

    - [Get DPM installed](install-dpm.md)

2. **Set up storage** - You can store backed-up data on disk, on tape, and in the cloud with Azure. Read more in [Prepare data storage](plan-long-and-short-term-data-storage.md).

3. **Set up the DPM protection agent** - You'll need to install the DPM protection agent on the machine you want to back up. Read [Deploy the DPM protection agent](deploy-dpm-protection-agent.md)

## Back up system state and bare metal

Set up a protection group as described in [Deploy protection groups](create-dpm-protection-groups.md). 

> [!NOTE]
> You can't protect BMR and system state for the same machine in different groups, and when you select BMR, system state is automatically enabled.

1. Select **Protection** > **Actions** > **Create Protection Group** to open the **Create New Protection Group** wizard in the DPM console.

2. In **Select protection group** type, select **Servers**.

3. In **Select Group Members**, expand the machine and select **BMR** or **system state**

    Remember that you can't protect BMR and system state for the same machine in different groups, and when you select BMR, system state is automatically enabled. Learn more in [Deploy protection groups](create-dpm-protection-groups.md).

4. In **Select data protection method**, specify how you want to handle short- and long-term backups. Short-term backup is always to disk first, with the option of backing up from the disk to the Azure cloud with Azure backup (for short- or long-term). As an alternative to long-term backup to the cloud, you can also configure long-term backup to a standalone tape device or tape library connected to the DPM server.

::: moniker range="sc-dpm-2016"

5. In **Select short-term goals**, specify how you want to back up to short-term storage on disk. In Retention range, specify how long you want to keep the data on disk. In Synchronization frequency, specify how often you want to run an incremental backup to disk. If you don't want to set a backup interval, you can check just before a recovery point so that DPM will run an express full backup just before each recovery point is scheduled.

::: moniker-end

::: moniker range=">=sc-dpm-2019"

5. In **Select short-term goals**, specify how you want to back up to short-term storage on disk. In Retention range, specify how long you want to keep the data on disk. In **Express Full Backup**, specify when you want to backup to disk.  All System State and BMR backups are considered express full backups for scheduling purposes.

::: moniker-end

6. If you want to store data on tape for long-term storage in **Specify long-term goals**, indicate how long you want to keep tape data (1-99 years). In Frequency of backup, specify how often backups to tape should run. The frequency is based on the retention range you've specified:

    - When the retention range is 1-99 years, you can select backups to occur daily, weekly, biweekly, monthly, quarterly, half-yearly, or yearly.

    - When the retention range is 1-11 months, you can select backups to occur daily, weekly, bi-weekly, or monthly.

    - When the retention range is 1-4 weeks, you can select backups to occur daily or weekly.

    On a standalone tape drive, for a single protection group, DPM uses the same tape for daily backups until there's insufficient space on the tape. You can also colocate data from different protection groups on tape.

    On the **Select Tape and Library Details** page, specify the tape/library to use, and whether data should be compressed and encrypted on tape.

7. In the **Review disk allocation** page, review the storage pool disk space allocated for the protection group.

    **Total Data size** is the size of the data you want to back up, and **Disk space to be provisioned on DPM** is the space that DPM recommends for the protection group. DPM chooses the ideal backup volume based on the settings. However, you can edit the backup volume choices in the **Disk allocation details**. For the workloads, select the preferred storage in the dropdown menu. Your edits change the values for **Total Storage** and **Free Storage** in the **Available Disk Storage** pane. Underprovisioned space is the amount of storage DPM suggests you add to the volume to continue with backups smoothly in the future.

8. In **Choose replica creation method**, select how you want to handle the initial full data replication. If you select to replicate over the network, we recommend you choose an off-peak time. For large amounts of data or less than optimal network conditions, consider replicating the data offline using removable media.

9. In **Choose consistency check options**, select how you want to automate consistency checks. You can enable a check to run only when replica data becomes inconsistent or according to a schedule. If you don't want to configure automatic consistency checking, you can run a manual check at any time by right-clicking the protection group in the **Protection** area of the DPM console and selecting **Perform Consistency Check**.

10. If you've selected to back up to the cloud with Azure Backup, on the **Specify online protection data** page, ensure you select the workloads that you want to back up to Azure.

::: moniker range="sc-dpm-2016"

11. In **Specify online backup schedule**, specify how often incremental backups to Azure should occur. You can schedule backups to run every day/week/month/year and the time/date at which they should run. Backups can occur up to twice a day. Each time a backup runs, a data recovery point is created in Azure from the copy of the backed-up data stored on the DPM disk.

::: moniker-end

::: moniker range=">=sc-dpm-2019"

11. In **Specify online backup schedule**, specify how often incremental backups to Azure should occur. You can schedule backups to run every day/week/month/year and the time/date at which they should run. Backups can occur up to twice a day. Each time a backup runs, a data recovery point is created in Azure from the copy of the backed-up data stored on the DPM disk.

     >[!NOTE]
     >Online backups have a dependency on new local disk based backup prior to running.  Ensure the Online protection schedule is compatible with the Express backup time and frequency.

::: moniker-end

12. In **Specify online retention policy**, specify how the recovery points created from the daily/weekly/monthly/yearly backups are retained in Azure.

13. In **Choose online replication**, specify how the initial full replication of data will occur. You can replicate over the network or do an offline backup (offline seeding). Offline backup uses the Azure Import feature. [Read more](/azure/backup/backup-azure-backup-import-export).

14. On the **Summary** page, review your settings. After you select **Create Group**, initial replication of the data occurs. When it finishes, the protection group status will show as **OK** on the **Status** page. Backup then takes place in line with the protection group settings.

## Recover system state or BMR

You can recover BMR or system state to a network location. If you've backed up BMR, use the Windows Recovery Environment (WinRE) to start up your system and connect it to the network. Then use Windows Server Backup to recover from the network location. If you've backed up system state, just use Windows Server Backup to recover from the network location.

Select the required tab for the steps to restore BMR or system state:

# [Restore BMR](#tab/RestoreBMR)

**Run recovery on the DPM server:**

1. In the Recovery pane, find the machine you want to recover > Bare Metal Recovery.

2. Available recovery points are indicated in bold on the calendar. Select the date and time for the recovery point you want to use.

3. In **Select Recovery Type**, select **Copy to a network folder.**

4. In **Specify Destination**, select where you want to copy the data to. Remember that the selected destination will need enough room. We recommend a new folder.

5. In **Specify Recovery Options**, select the security settings to apply and select whether you want to use SAN-based hardware snapshots for quicker recovery (only an option if you have a SAN with this functionality enabled and the ability to create and split a clone to make it writable. In addition, the protected machine and DPM server must be connected to the same network).

6. Set up notification options and select **Recover** on the **Summary** page.

**Set up the share location:**

1. In the restore location, navigate to the folder that contains the backup.

2. Share the folder above WindowsImageBackup so that the root of the shared folder is the WindowsImageBackup folder. If it isn't, restore won't find the backup. To connect using WinRE, you'll need a share that you can access in WinRE with the correct IP address and credentials.

**Restore the system:**

1. Start the machine for which you want to restore the image to using the Windows DVD to match the system you're restoring.

2. On the first screen, verify language/locale settings. On the **Install** screen, select **Repair your computer**.

3. On the **System Recovery Options** page, select **Restore your computer using a system image that you created earlier**

4. On the **Select a system image backup** page, select **Select a system image** > **Advanced** > **Search for a system image on the network**. Select **Yes** if a warning appears. Navigate to the share path, input the credentials, and select the recovery point.
     This scans for specific backups available in that recovery point. Select the recovery point.

5. In **Choose how to restore the backup**, select **Format and repartition disks**. In the next screen, verify settings and select **Finish** to begin the restore. Restart as required.

# [Restore system state](#tab/RestoreSystemState)

**Run recovery on the DPM server:**

1. In the Recovery pane, find the machine you want to recover > Bare Metal Recovery.

2. Available recovery points are indicated in bold on the calendar. Select the date and time for the recovery point you want to use.

3. In **Select Recovery Type**, select **Copy to a network folder.**

4. In **Specify Destination**, select where you want to copy the data to. Remember that the selected destination will need enough room. We recommend a new folder.

5. In **Specify Recovery Options**, select the security settings to apply and select whether you want to use SAN-based hardware snapshots for quicker recovery (only an option if you have a SAN with this functionality enabled and the ability to create and split a clone to make it writable. In addition, the protected machine and DPM server must be connected to the same network).

6. Set up notification options and select **Recover** on the **Summary** page.

**Run Windows Server Backup:**

1. Select **Actions** > **Recover** > **This Server** > **Next.**

2. Select **Another Server** > **Specify Location Type** page > **Remote shared folder**. Provide the path to the folder that contains the recovery point.

3. In **Select Recovery Type**, select **System state**. In **Select Location for System State Recovery**, select **Original Location**

4. In **Confirmation**, select **Recover**. You'll need to restart the server after the restore.

5. You can also run a system state restore from the command line. To do this, start Windows Server Backup on the machine you want to recover. From a command line, enter: **wbadmin get versions -backuptarget <servername\sharename>** to get the version identifier.

    Use the version identifier to start system state restore. At the command line, enter: **wbadmin start systemstaterecovery -version:\<versionidentified\> -backuptarget:<servername\sharename>**, and confirm that you want to start the recovery. You can see the process in the command window. A restore log is created. You'll need to restart the server after the restore.
---
