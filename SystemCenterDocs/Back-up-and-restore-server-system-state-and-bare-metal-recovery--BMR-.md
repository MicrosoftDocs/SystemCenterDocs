---
title: Back up and restore server system state and bare metal recovery (BMR)
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d55b7545-0bba-4169-bcab-4e185afe3f93
---
# Back up and restore server system state and bare metal recovery (BMR)
DPM can back up system state and provider bare metal recovery \(BMR\) protection. This enables you System protection aims to protect you against two scenarios – one where your computer starts, but you have lost system files and registry; and the other where the computer does not start and you have to recover everything. [!INCLUDE[dpm2012long](Token/dpm2012long_md.md)] enables you to protect your computer against both these scenarios.

-   BMR protection—Backs up operating system files and all data except user data on critical volumes. By definition a BMR back up includes a system state backup.

-   System state—Backs up operating system files.

Here’s a summary of what you can recover if you’ve backed up with these methods

|Data type|Data|Recover from system state backup only|Recover from bare metal backup \(which includes a system state backup\)|
|-------------|--------|-----------------------------------------|---------------------------------------------------------------------------|
|File data<br /><br />Protect file data with regular DPM file data backup<br /><br />Protect file system with BMR backup|Lost or damaged operating system|INVALID USE OF SYMBOLS|INVALID USE OF SYMBOLS|
||Lost server \(Data volumes intact\)|x|INVALID USE OF SYMBOLS|
||Lost server \(Data volumes lost\)|x|INVALID USE OF SYMBOLS<br /><br />BMR followed by regular recovery of backed up file data|
|SharePoint<br /><br />Protect farm data using regular SharePoint backup<br /><br />Protect Web front\-end server and IIS role with BMR backup\)<br /><br />Protect servers hosting content database with BMR or system state backup|Lost or damaged operating system|INVALID USE OF SYMBOLS|INVALID USE OF SYMBOLS|
||Disaster recovery|x|INVALID USE OF SYMBOLS|
|Hyper\-V virtual machines<br /><br />Protect virtual machines with regular DPM Hyper\-V backup<br /><br />Protect Hyper\-V host server with BMR backup \(at least once a day\)|Lost or damaged operating system|INVALID USE OF SYMBOLS|INVALID USE OF SYMBOLS|
||Lost Hyper\-V host server \(virtual machines intact\)|x|INVALID USE OF SYMBOLS|
||Lost Hyper\-V host server \(virtual machines also lost\)|x|INVALID USE OF SYMBOLS<br /><br />BMR followed by regular recovery of backed up virtual machine data|
|SQL Server<br /><br />Protect database with regular DPM backup<br /><br />Protect SQL Server system with BMR backup|Lost or damaged operating system|INVALID USE OF SYMBOLS|INVALID USE OF SYMBOLS|
||Lost server \(database and transaction log files intact\)|x|INVALID USE OF SYMBOLS|
||Lost server \(database and transaction log files also lost\)|x|INVALID USE OF SYMBOLS<br /><br />BMR followed by regular recovery of backed up SQL Server database|
|Exchange<br /><br />Protect data with regular DPM backup<br /><br />Protect Exchange system with BMR backup|Lost or damaged operating system|INVALID USE OF SYMBOLS|INVALID USE OF SYMBOLS|
||Lost server \(database and transaction log files intact\)|x|INVALID USE OF SYMBOLS|
||Lost server \(database and transaction log files also lost\)|x|INVALID USE OF SYMBOLS<br /><br />BMR followed by regular recovery of backed up Exchange database|

## Prerequisites and limitations

-   BMR isn’t supported for computers running Windows Server 2003 or for computers running client operating systems.

-   You can’t protect BMR and system state for the same computer in different protection groups.

-   A [!INCLUDE[dpm2012short](Token/dpm2012short_md.md)] server can’t protect itself for BMR.

-   Short\-term protection to tape \(D2T\) isn’t supported for BMR. Long\-term storage to tape \(D2D2T\) is supported.

-   Windows Server Backup must be installed on the protected computer for BMR.

-   Windows Recovery Environment \(WinRE\) for BMR.

-   For BMR protection \(unlike system state protection\) DPM doesn’t have any space requirements on the protected computer. WSB directly transfers the backups to the DPM server. Note that the job for this doesn’t appear in the DPM Jobs view.

-   DPM reserves 30 GB of space on the replica volume for BMR. You can change this on the **Disk Allocation**page in the Modify Protection Group Wizard or using the Get\-DatasourceDiskAllocation and Set\-DatasourceDiskAllocation PowerShell cmdlets. On the recovery point volume, BMR protection requires about 6 GB for retention of five days.

    Note that you can’t reduce the replica volume size to less than 15 GB.

    DPM doesn’t calculate the size of BMR data source, but assumes 30 GB for all servers. Admins should change the value as per the size of BMR backups expected on their environments. The size of a BMR backup can be roughly calculated sum of used space on all critical volumes: Critical volumes \= Boot Volume \+ System Volume \+ Volume hosting system state data such as AD.

## Process
**System state backup**

-   When a system state back up runs DPM communicates with WSB request a backup of the server’s system state. By default DPM and WSB will use the drive with the most available free space, and information about this drive is saved in the PSDataSourceConfig.XML file. This is the drive WSB will use to do backups to.

    You can customize the drive that DPM uses for the system state backup. To do this on the protected server, go to C:\\Program Files\\Microsoft Data Protection Manager\\DPM\\Datasources. Open the PSDataSourceConfig.XML file for editing. Change the<**FilesToProtect**> value for the drive letter. Close and save the file. If there’s a protection group protecting the system state of the computer run a consistency check. In case an alert is generated click Modify protection group link in the alert, and then step through the wizard. Then run another consistency check.

    Note that if the protection server is in a cluster it’s possible that a cluster drive will be selected as the drive with the most free space. It’s important to be aware of this because if that drive ownership has been switched to another node and a system state backup runs, the drive won’t be available and the backup will fail. In this situation, you’ll need to modify the PSDataSourceConfig.XML to point it to a local drive.

-   WSB will then create a folder called WindowsImageBackup on the root of the. As it creates the backup, all of the data will be placed in this folder. When the backup completes the file will then be transferred over to the DPM server. Note that:

    -   This folder and its contents do not get cleaned up after the backup or transfer is done. The best way to think of this is that the space is being reserved for the next time a backup is done.

    -   The folder gets created every time a backup is done. The time\/date stamp will reflect the time of your last system state backup.

**BMR backup**

1.  For BMR \(which inherently captures a system state backup\) the backup job is performed directly to a share on the DPM server and not to a folder on the protected server.

2.  DPM server calls WSB and shares out the replica volume for that BMR backup. In this case it doesn’t tell WSB to use the drive with the most free space, but instead to use the share created for the job.

3.  When the backup finishes the file is transferred to the DPM server. Logs are stored in C:\\Windows\\Logs\\WindowsServerBackup.


