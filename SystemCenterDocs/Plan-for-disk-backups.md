---
title: Plan for disk backups
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 59da5b8e-67ae-4d88-96f8-2c3aad188143
---
# Plan for disk backups
DPM provides short\-term backup to disk by saving data to the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] storage pool. The storage pool is the set of disk on which the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] server stores the replicas and recovery points for the protected data. Before you can start protecting data using disk storage, you must add at least one disk to the storage pools.

The storage pool is a set of disks DPM can use any of the following for the storage pool:

-   Direct attached storage \(DAS\)

-   Fiber Channel storage area network \(SAN\)

-   iSCSI storage device or SAN

Note the following:

-   The DPM server must have at least two disks installed: one dedicated to the startup, system, and DPM installation files; and one dedicated to the storage pool. In the context of DPM, disk is defined as any disk device manifested as a disk in the Windows Disk Management tool. DPM does not add any disk containing startup files, system files, or any component of the DPM installation to the storage pool.

-   Disks added to the storage pool should not have any partitions. To prepare disks for data protection, DPM reformats the disks and erases any data on them.

-   The storage pool supports most disk types, including Integrated Drive Electronics \(IDE\), Serial Advanced Technology Attachment \(SATA\), and SCSI, and it supports both the master boot record \(MBR\) and GUID partition table \(GPT\) partition styles. We strongly recommend that you use GPT disks for the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] storage pool.

-   If you use a SAN for the storage pool, we recommend that you create a separate zone for the disk and tape used on [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)]. Do not mix the devices in a single zone.

-   DPM does not support USB\/1394 disks in the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] storage pool.

-   You cannot use Storage Spaces for the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] disk storage pool.

-   Support for deduplicated volumes depends on the DPM operating system. For more information, see [Storage issues](assetId:///3e0cd491-3757-4727-90db-eca0c3e6f7fc#BKMK_Storage).

-   DPM running as a Hyper\-V virtual machine can store backup data to VHDs in shared folders on a Windows File Server with data deduplication enabled. For more information, see [Deduplicating DPM storage](assetId:///a681ca08-bf1c-40b6-a9b7-c6fbbc76aeb5).

-   Some original equipment manufacturers \(OEMs\) include a diagnostic partition that is installed from media that they provide. The diagnostic partition might also be named the OEM partition, or the EISA partition. EISA partitions must be removed from disks before you can add the disk to the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] storage pool.

-   You can also substitute custom volumes that you define in Disk Management for volumes in the storage pool.

Planning the storage pool involves the following:

-   [Calculate capacity requirements](#BKMK_Capacity)

-   [Plan the disk configuration](#BKMK_PlanDisk)

-   [Define custom volumes](#BKMK_Custom)

## <a name="BKMK_Capacity"></a>Calculate capacity requirements
Capacity requirements for the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] storage pool are variable and depend primarily on the size of the protected data, the daily recovery point size, expected volume data growth rate, and retention range objectives.

Daily recovery point size refers to the total size of changes made to protected data during a single day. It is roughly equivalent to the size of an incremental backup. Retention range refers to the number of days for which you want to store recovery points of protected data on disk. For files, [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] can store a maximum of 64 recovery points for each volume included in a protection group, and it can create a maximum of 8 scheduled recovery points for each protection group each day.

> [!NOTE]
> The limit of 64 recovery points for files is a result of the limitations of the Volume Shadow Copy Service \(VSS\), which is necessary for the end\-user recovery functionality of [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)]. The recovery point limit does not apply to application data.

In general, we recommend making the storage pool two times the size of the protected data for protection of files. This recommendation is based on an assumed daily recovery point size of approximately 10 percent of the protected data size and a retention range of 10 days \(two weeks, excluding weekends\).

If your daily recovery point size is larger or smaller than 10 percent of your protected data size, or if your retention range objectives are longer or shorter than 10 days, you can adjust the capacity requirements for your storage pool accordingly.

Regardless of how much capacity you decide to allow for the storage pool in your initial deployment, we recommend that you use extensible hardware so that you have the option of adding capacity should the need arise.

The sections that follow provide guidelines for determining your daily recovery point size and retention range objectives.

### Estimating Daily Recovery Point Size
Our recommendation to make the storage pool two times the size of the protected data assumes a daily recovery point size of 10 percent of the protected data size. Daily recovery point size is related to data change rate and refers to the total size of all recovery points created during a single day. To get an estimate of the daily recovery point size for your protected data, you can review an incremental backup for a recent, average day. The size of the incremental backup is usually indicative of the daily recovery point size. For example, if the incremental backup for 100 GB of data includes 10 GB of data, your daily recovery point size will probably be approximately 10 GB.

### Determining Retention Range Objectives
Our recommendation to make the storage pool two times the size of the protected data assumes a retention range objective of 10 days \(two weeks, excluding weekends\). For the typical enterprise, requests for recovery of data are concentrated within two to four weeks after data loss events. A retention range of 10 days provides for recovery of data up to two weeks after a data loss event.

The longer your retention range objective, the fewer recovery points you can create each day. For example, if your retention range objective is 64 days, you can create just one recovery point each day. If your retention range objective is eight days, you can create eight recovery points each day. With a retention range objective of 10 days, you can create approximately six recovery points each day.

## <a name="BKMK_PlanDisk"></a>Plan the disk configuration
If you are using direct\-attached storage for the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] storage pool, you can use any hardware\-based configuration of redundant array of independent disks \(RAID\), or you can use a "just a bunch of disks" \(JBOD\) configuration. Do not create a software\-based RAID configuration on disks that you will add to the storage pool.

To decide on the configuration for the disks, consider the relative importance of capacity, cost, reliability, and performance in your environment. For example, because JBOD does not consume disk space for storing parity data, a JBOD configuration makes maximum use of storage capacity. For the same reason, the reliability of JBOD configurations is poor; a single disk failure inevitably results in data loss.

For the typical [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] deployment, [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] recommends a RAID 5 configuration, which offers an effective compromise between capacity, cost, reliability, and performance.

To help you evaluate options for configuring the disks in your storage pool, the following table compares the trade\-offs between JBOD and the various levels of RAID, on a scale from 4 \(very good\) to 1 \(acceptable\).

**Comparison of Configuration Options for Storage Pool Disks**

|Disk Configuration|Capacity|Cost|Reliability|Performance and Scalability|
|----------------------|------------|--------|---------------|-------------------------------|
|JBOD|4|4|1|4|
|RAID 0|4|4|1|4|
|RAID 1|1|1|4|3|
|RAID 5|3|3|3|3|
|RAID 10|1|1|4|4|

For more information about RAID, see [Achieving Fault Tolerance by Using RAID](http://go.microsoft.com/fwlink/?LinkId=46086).

## <a name="BKMK_Custom"></a>Define custom volumes
In [!INCLUDE[dpm2012long](./Token/dpm2012long_md.md)], you can assign a *custom volume* to a protection group member, in place of the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] storage pool. A custom volume is a volume that is not in the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] storage pool and is specified to store the replica and recovery points for a protection group member.

Although the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)]\-managed storage pool is sufficient for most business needs, you might want a greater amount of control over storage for specific data sources. For example, you have critical data that you want to store using a high\-performance logical unit number \(LUN\) on a storage area network.

Any volume that is attached to the [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] server can be selected as a custom volume in the Create New Protection Group Wizard, except the volume that contains the system and program files. To use custom volumes for a protection group member, two custom volumes must be available: one volume to store the replica and one volume to store the recovery points.

[!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] cannot manage the space in custom volumes. If [!INCLUDE[dpm2012short](./Token/dpm2012short_md.md)] alerts you that a custom replica volume or recovery point volume is running out of space, you must manually change the size of the custom volume by using Disk Management.

You cannot change the selection of storage pool or custom volume for a protection group member after the group is created. If you must change the storage location for a data source's replica or recovery points, you can do so only by removing the data source from protection and then adding it to a protection group as a new protection group member.


