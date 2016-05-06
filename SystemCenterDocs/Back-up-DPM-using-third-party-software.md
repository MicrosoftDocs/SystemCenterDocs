---
title: Back up DPM using third-party software
ms.custom: na
ms.prod: system-center-2012-r2
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d2299d54-0ef5-4e40-8b69-8db5dfc1caf5
---
# Back up DPM using third-party software
You can back up DPM using third\-party software. The backup process depends on whether the backup software supports DPM and the Volume Shadow Copy Service \(VSS\):Archive and restore operations are more complex than they are when using software that supports DPM. The software that supports VSS organizes the archived replicas so that they appear to have been backed up directly from the DPM server. Organizing the backup in this way can make the process of restoring data less intuitive.When you use backup software that does not support VSS, you cannot back up directly from the replicas. Instead, you must use the DPMBackup tool to create backup shadow copies of the replicas and database backups of the DPM database, and then use the backup software to archive the backup shadow copies and database backups to tape.

-   **[Backup with a DPM\-enabled application](#BKMK_DPM)**—This option is specifically designed to work with DPM and supports the DPM VSS Writer service \(DPM Writer\). Archived data is organized so that restore operations are simplified, and you can back up directly from the replicas.

-   **[Back up with a VSS\-enabled application](#BKMK_VSS)**—This option uses VSS\-enabled file system shadow copies but doesn’t operate with the DPM Writer service. The restore process is more complicated and you can’t back up directly from the replicas.

-   [Back up with an application without DPM or VSS support](#BKMK_NoVSS)—With this option you’ll need create backup shadow copies of the replicas and database backups, and then use the backup software to archive the backup shadow copies and database backups to tape.

## <a name="BKMK_DPM"></a>Back up with a DPM\-enabled application

1.  To backup databases, in the backup program, browse to \\Program Files\\Microsoft System Center 2012\\DPM\\DPM\\DPMDB, and select the DPMDB folder. Select the backup media and start the backup.

2.  To back up replicas, in the backup program expand the DPM server and select the computer whose replicas you want to archive \(or the individual protected volumes. Select the backup media and start the backup.

## <a name="BKMK_VSS"></a>Back up with a VSS\-enabled application
Before you start check that the software doesn’t modify data on the replica volumes. For example, if you are using Windows Backup to archive data, use only the “copy” backup type. Then back up as follows:

1.  To backup databases, in the backup program, browse to \\Program Files\\Microsoft System Center 2012\\DPM\\DPM\\DPMDB, and select the DPMDB folder. Select the backup media and start the backup. Note that some VSS\-enabled backup software does not have a SQL VSS Requester for backing up SQL Server databases through the VSS infrastructure and the MSDE VSS Writer. In that situation, use the procedure for backing up databases with non\-VSS\-enabled backup software.

2.  To back up replicas, in the backup program browse to \\Microsoft System Center 2012\\DPM\\DPM\\Volumes\\Replica\\ on the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] server the DPM server. Select the computer whose replicas you want to archive \(or the individual protected volumes\). Select a backup type that doesn’t modify the replica data. Select the backup media and start the backup.

## <a name="BKMK_NoVSS"></a>Back up with an application without DPM or VSS support
If your backup software doesn’t support DPM or VSS you’ll need to use use the D**PMBackup** command\-line tool to create backup shadow copies of the replicas and database backups of the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] database. Then use the backup software to archive the backup shadow copies and database backups to tape. DPMBackup does the following:

-   Creates and mounts backup shadow copies of each replica volume on the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] server.

-   Creates database backups of the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] database.

-   [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] creates a mount point of the backup shadow copies of the replicas on the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] server in the folder \\Program Files\\Microsoft System Center 2012\\DPM\\DPM\\Volumes\\ShadowCopy\\. The backup shadow copies of the replicas are organized by computer.

Note that:

-   The DPMBackup.exe program is stored on the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] server in the folder \\Program Files\\Microsoft System Center 2012\\DPM\\DPM\\bin. DPMBackup requires Administrator rights on the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] server.

-   You can configure either your tape backup program or Windows Scheduler to run DPMBackup before the tape backup program runs.

-   The time DPMBackup needs to create the backup shadow copies and database backups depends on factors such as disk and database activity. As a guideline, you can expect the tool to take approximately two minutes per replica volume.

-   The backup shadow copies created by DPMBackup are read\-only copies of the replica volumes. You can archive them as you would a file system. Because the backup shadow copies of the replicas are mounted, you must configure your tape backup software to traverse mount points.

You’ll back up the DPM database as follows:

1.  To back up databases, run DPMBackup.exe –db. In the backup program browse to \\Program Files\\Microsoft DPM\\DPM\\Volumes\\ShadowCopy\\Database Backups. \(DPM database backup: DPMDB.bak; Report database backup: ReportServer.bak\), Select the backup media and start the backup.

2.  To back up replicas, run DPMBackup.exe –replica. In the backup program program, browse to \\Program Files\\Microsoft System Center 2012\\DPM\\DPM\\Volumes\\ShadowCopy\\. The backup shadow copies of the replicas are organized by computer. Select the shadow copies you want to back up and the backup type. Select the backup media and start the backup.


