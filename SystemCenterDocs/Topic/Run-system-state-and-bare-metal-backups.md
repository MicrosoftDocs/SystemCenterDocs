---
title: Run system state and bare metal backups
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b33f0de2-0194-42b1-89c2-4338cbaef532
---
# Run system state and bare metal backups
DPM provides two types of system backup —system state and bare metal backup.

-   System state backup protects your operating system files. If a protected computer can start but can’t access system files or the registry you can recover using a system state backup. System state backs up the following:

    -

-   Bare metal backup protects your operating system files and data \(except for data on critical volumes\). If a protected computer can’t start you can recover using a bare metal backup. Note that a bare metal backup includes a system state backup.

-   Both types of system back up use Windows Server Backup to back up data to a .bkf file. For recovery, DPM retrieves the backups and you use the retrieved backup data to recover the computer using Windows Server Backup.

-   Check the [DPM protection support matrix](assetId:///52bed83a-f484-4925-af77-377073737fc4) to verify which clients can be protected with system backup. Note that a DPM can’t protect itself using bare metal backup.

-   Because system data doesn’t change frequently, consider placing sources you want to protect with system state and bare metal backup into separate protection groups.

-   For system protection of servers running Windows Server 2008, install the update described in KB [949779](http://go.microsoft.com/fwlink/?LinkId=122512).

## What does system state backup include?

|Protected computer|What system state backs up|
|----------------------|------------------------------|
|Domain member|-   The boot files<br />-   The COM\+ class registration database<br />-   The registry|
|Domain controller|-   Active Directory \(NTDS\)<br />-   The boot files<br />-   The COM\+ class registration database<br />-   The registry<br />-   The system volume \(SYSVOL\)|
|Domain member or domain controller running Certificate Services|Additionally protects certificate services.|
|Domain member or domain controller running Cluster server|Additionally protects cluster server metadata|

## Running a system backups

1.  When a system state backup kicks off DPM requests a backup of the protected server system state from Windows Backup server.

2.  When the DPM protection agent was installed on the protected server it was installed on the drive with the most available free space. This is the drive that Windows Server Backup will uses for the backups it creates.

3.  Windows Server Backup creates a folder \(WindowsImageBackup\) in the root of that drive. As the backup is created the data is placed there.

    Note that this folder gets created every time a backup is done. The time and data stamp indicate the time of the last system backup. This folder and its contents don’t get cleaned up after first backup is done. It operates as space reserved the next time a backup is done.

    You can customize the drive that DPM uses for the system state backup. To do this on the protected server, go to C:\\Program Files\\Microsoft Data Protection Manager\\DPM\\Datasources. Open the PSDataSourceConfig.XML file for editing. Change the **<FilesToProtect>** value for the drive letter. Close and save the file. If there’s a protection group protecting the system state of the computer run a consistency check. In case an alert is generated click **Modify protection group** link in the alert, and then step through the wizard. Then run another consistency check.

4.  When you run a bare metal backup \(which includes capturing the system state\) the backup job is done directly to a share on the DPM server and not to a folder on the protected server.  To do this DPM server shares out the replica volume for the bare metal backup and communicates to Windows Server Backup that it should use the share created for the job rather than the drive with the most free space.

5.  When the backup finishes the file is transferred to the DPM server.

6.  Logs are stored in C:\\Windows\\Logs\\WindowsServerBackup.

## Run a system state or bare metal backup

1.  Create a new protection group or modify an existing one to configure system state or bare metal backup for a resource you want to protection.

2.  In the Select Group Members page of the protection group wizard, expand the Available Members section and under System Protection select **Bare Metal Recovery** \(which includes **System State**\) or **System State** only.

3.  Configure or verify the rest of the wizard settings.

4.  When the wizard finishes the initial backup runs. When this completes you’ll be able to view the recovery point. To do this, click the Recover ribbon and drill down to Recoverable Data > System Protection > All DPM Protected Data.

## NTBackup
If you’re protecting a server running an operating system earlier than Windows Server 2008 DPM will use NTBackup and not Windows Server Backup note the following:

-   When a system state backup runs the backup file is created in backup file of system state is created at %systemdrive%\\DPM\_SYSTEM\_STATE.

-   The logs for system state backup are stored at C:\\Document and Settings\\Default User\\Application Data\\Microsoft\\NTBackup. Log files will be named NTBackup0.log, NTBackup1.log, and so forth. You can view these logs to help resolve any issues that occur with the system state backup. You can change the default location of the backup file in the same way described above for Windows Server Backup.

