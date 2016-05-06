---
title: Data backup and protection overview
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92e62e1e-2076-4bfe-9d6e-045fe0f6f972
---
# Data backup and protection overview

## Backup overview
On each computer or server you want to protect by backing up data to DPM you install the DPM protection agent. In the DPM Administrator console you add each data source you want to protect to a protection group, and configure backup, storage, retention and restore settings for each group. Data you backup is stored by DPM as follows:

-   <Install Drive>\\Program Files\\Microsoft System Center 2012\\DPM\\DPM\\Volumes\\Replica— The Replica folder contains mounted data replica volumes.

-   <Install Drive>\\Program Files\\Microsoft System Center 2012\\DPM\\DPM\\Volumes\\ShadowCopy—Contains backup copies of the DPM database.

-   <Install Drive>\\Program Files\\Microsoft System Center 2012\\DPM\\DPM\\Volumes\\DiffArea—Contains mounted shadow copy volumes that store the recovery points for a data source.

DPM replicates data to storage. DPM can use disk, Microsoft Azure, or tape for short\-term storage, and tape for long\-term storage.

Read more about the clients, servers and workloads that DPM can back up in the [DPM protection support matrix](assetId:///52bed83a-f484-4925-af77-377073737fc4).

## Synchronization overview
DPM backs up and synchronizes data to disk. During this process DPM creates and maintains a replica, or copy, of the data that’s on protected servers. DPM creates recovery points \(snapshots\) of this replicated data. The replicas are stored in the DPM storage pool which consists of a set of disks on the DPM server, or on a custom volume.

The replica is synchronized at regular intervals according to the settings that you configure. During synchronization data changes are transferred from the protected source to the DPM server and then applying those data changes on the replica in the pool. DPM does this with:

-   Incremental synchronization—DPM checks what’s changed on the data source and updates the delta changes on the replica.

-   Incremental synchronization with consistency check—DPM checks what’s changed on the data source and updates the delta changes on the replica with an additional block\-level check of the replica to ensure data consistency.

The synchronization method that DPM depends on the type of data being protected — file or application data

Data that exists on a file server and which needs to be protected as a flat file qualifies as file data, such as Microsoft Office files, text files, batch files, and so forth. Data that exists on an application server and which requires DPM to be aware of the application qualifies as application data, such as Exchange storage groups, SQL Server databases, and SharePoint farms.

### Synchronizing file data
For file\-based resources \(volumes, shares, folders\) the DPM protection agent uses a volume filter and the change journal to figure out which files have changed, and then performs a checksum procedure for these files to synchronize only the changed blocks. The changes are transferred to the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] server and applied to the replica to synchronize it, as shown.

![](/Image/6220f128-bd14-4fce-a61c-e9ed66d66973.gif)

Note that:

-   If a replica becomes inconsistent [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] generates an alert. To resolve it you initiate a synchronization with a consistency check on the replica. [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] performs a block\-by\-block verification and repairs the replica to bring it back into consistency with the data source.

-   You can schedule a daily consistency check for protection groups or initiate a consistency check manually.

-   At regular intervals you can configure, [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] creates a *recovery point* for a protection group member. A recovery point is a version of the data from which data can be recovered. For files, a recovery point consists of a shadow copy of the replica, which is created by using the Volume Shadow Copy Service \(VSS\) functionality of the operating system on the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] server.

### Synchronizing workload data
For application data, after the replica is created by [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)], changes to volume blocks that belong to application files are tracked by the volume filter. How changes are transferred to the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] server depends on the application and the type of synchronization:

-   Synchronizations labelled **synchronization** in the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] Administrator Console are basically an incremental backup. When combined with the replica it creates an accurate reflection of the application data..

-   Synchronizations labeled **express full backup** in [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] Administrator Console indicate that a full Volume Shadow Copy Service \(VSS\) snapshot is created but only changed blocks are transferred to the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] server.

    Each express full backup creates a recovery point for application data. If the application supports incremental backups, each synchronization also creates a recovery point.

-   Workloads use the following types of synchronization:

    -   Exchange—Synchronization transfers an incremental VSS snapshot using the Exchange VSS writer. Recovery points are created for each synchronization and express full backup.

    -   SQL Server—Databases that are log\-shipped, in read\-only mode, or that use the simple recovery model do not support incremental backup. Recovery points are created for each express full backup only. For all other SQL Server databases, synchronization transfers a transaction log backup, and recovery points are created for each incremental synchronization and express full backup. The transaction log is a serial record of all the transactions that have been performed against the database since the transaction log was last backed up.

    -   SharePoint—Doesn’t support incremental backup. Recovery points are created for each express full backup only.

### Comparing incremental and full express backup

-   Incremental synchronizations require less time than performing an express full backup. However, the time required to recover data increases as the number of synchronizations increases. This is because [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] must restore the last full backup and then restore and apply all the incremental synchronizations up to the point in time selected for recovery.

-   To enable faster recovery time, [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] regularly performs an express full backup, a type of synchronization that updates the replica to include the changed blocks.

-   During the express full backup, [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] takes a snapshot of the replica before updating the replica with the changed blocks. To enable more frequent recovery point objectives, as well as to reduce the data loss window, [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] also performs incremental synchronizations in the time between two express full backups.

-   As with the protection of file data, if a replica becomes inconsistent with its data source, [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] generates an alert that specifies which server and which data source are affected. To resolve the problem, the administrator repairs the replica by initiating a synchronization with consistency check on the replica. During a consistency check, [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] performs a block\-by\-block verification and repairs the replica to bring it back into consistency with the data sources.

    You can schedule a daily consistency check for protection groups or initiate a consistency check manually.


