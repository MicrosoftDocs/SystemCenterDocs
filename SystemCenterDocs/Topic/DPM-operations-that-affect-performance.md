---
title: DPM operations that affect performance
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bf9253a4-a8a4-495a-92f2-2861ba12e86e
---
# DPM operations that affect performance
A number of [!INCLUDE[dpm2012long](../Token/dpm2012long_md.md)] data transfer operations affect performance, including:

-   **[Creating replicas](#BKMK_Replica)**—This occurs once for each protection group member.

-   **[Change tracking](#BKMK_Track)**—This is a continuous process on each protected computer.

-   **[Synchronizing data](#BKMK_Data)**—This occurs on a regular schedule.

-   **[Running consistency checks](#BKMK_Check)**—This occurs when a replica becomes inconsistent.

-   **[Running express full backups](#BKMK_Express)**—This occurs on a regular schedule.

-   **[Backing up to tape](#BKMK_Tape)**—This occurs on a regular schedule.

-   [Running DPM processes](#BKMK_Process)—Describes DPM processes that affect performance.

## <a name="BKMK_Replica"></a>Creating replicas
A replica is a complete copy of the protected data on a single volume, database, or storage group. The [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] protection agent on the protected computer sends the data selected for protection to the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server. A replica of each member in the protection group is created. Creating an initial replica is a resource\-intensive operation with a significant on network resources.

Typically

The initial data replication can be performed offline, or over the network. For more information, see the section about replica creation in [Plan for protection groups](assetId:///85cae9ee-0d7c-410a-b8c1-c62a9c4e2fb9). If you’re performing replication over the network note the following:

-   Replication over the network is limited by the speed of the network connection between the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server and the protected computers. That is, the amount of time that it takes to transfer a 1\-gigabyte \(GB\) volume from a protected computer to the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server will be determined by the amount of data per second that the network can transmit.

-   On an extremely fast network, such as a gigabit connection, the speed of replica creation will be determined by the disk speed of the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server or that of the protected computer, whichever is slower.

-   You can reduce the network performance overhead of replication b using bandwidth throttling and compression.

-   Try and ensure that networks will be consistently available during replication. If the network goes down during replication and remains down for longer than five minutes, the replica status will be inconsistent.

The following table shows a sampling of the time it takes to transmit data at different network speeds. Times are in hours, unless otherwise specified.

### Data transmission times

|Data size|Network speed<br /><br />1 GB per second \(assuming disk speed isn’t a bottleneck\)|Network speed<br /><br />100 MB per second|Network speed<br /><br />32 MB per second|Network speed<br /><br />8 MB per second|Network speed<br /><br />2 MB per second|Network speed<br /><br />512 KB per second|
|-------------|-------------------------------------------------------------------------------|--------------------------------------|-------------------------------------|------------------------------------|------------------------------------|--------------------------------------|
|1 GB|< 1 minute|< 1 hour|< 1|< 1|1.5|6|
|50 GB|<10 minutes|1.5 hour|5|18|71|284|
|200 GB|<36 minutes|6 hours|18|71|284|1137|
|500 GB|<1.5 hours|15|45|178|711|2844|

> [!NOTE]
> Typically, the time to complete initial replica \(IR\) creation can be calculated as follows:
> 
> IR: hours \= \(\(data size in MB\) \/ \(.8 x network speed in MB\/s\)\) \/ 3600
> 
> Note 1: Convert network speed from bits to bytes by dividing by 8.
> 
> Note 2: The network speed is multiplied by .8 because the maximum network efficiency is approximately 80%.

## <a name="BKMK_Track"></a>Change tracking
After the replica is created, the agent on the protect computer begins tracking all changes to protected data. Changes to files are passed through a filter before being written to the volume. This process is similar to the filtering of files through antivirus software, but the performance load of [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] tracking changes is less than the performance load of antivirus software.

## <a name="BKMK_Data"></a>Synchronizing data
Synchronization is the process by which [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] transfers data changes from the protected computer to the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server and then applies the changes to the replica of the protected data. Note the following:

-   For a file volume or share, the protection agent on the protected computer tracks changes to blocks, using the volume filter and the change journal that is part of the operating system to determine whether any protected files were modified. [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] also uses the volume filter and change journal to track the creation of new files and the deletion or renaming of protected files.

-   For application data, after the replica is created, changes to volume blocks belonging to application files are tracked by the volume filter.

-   How changes are transferred to the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server depends on the application and the type of synchronization. For protected Microsoft Exchange data, synchronization transfers an incremental Volume Shadow Copy Service \(VSS\) snapshot. For protected Microsoft SQL Server data, synchronization transfers a transaction log backup.

-   [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] relies on synchronization to update replicas with the protected data. Each synchronization job consumes network resources and can therefore affect network performance.

-   The impact of synchronization on network performance can be reduced by using network bandwidth usage throttling and compression.

## <a name="BKMK_Check"></a>Running consistency checks
A consistency check is the process by which [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] checks for and corrects inconsistencies between a protected data source and its replica.

The performance of the protected computer, [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server, and network will be affected while a consistency check is running, but it is expected to be optimized because only the changes and checksums are transferred.

The network impact from a consistency check is significantly lower than initial replica creation after a successful replica creation. If the initial replica creation is interrupted or unsuccessful, the first consistency check can have an impact similar to replica creation.

We recommend that consistency checks be performed during off\-peak hours.

[!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] automatically performs a consistency check in the following instances:

-   When you modify a protection group by changing the exclusion list.

-   When a daily consistency check is scheduled and the replica is inconsistent.

## <a name="BKMK_Express"></a>Running express full backups
An express full backup is a type of synchronization in which the protection agent transfers a snapshot of all blocks that have changed since the previous express full backup \(or since the initial replica creation, for the first express full backup\) and updates the replica to include the changed blocks. The impact of an express full backup operation on performance and time is expected to be less than the impact of a full backup because [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] transfers only the blocks changed since the last express full backup.

## <a name="BKMK_Tape"></a>Backing up to tape
When [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] backs up data from the replica to tape, there is no network traffic and therefore no performance impact on the protected computer.

When [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] backs up data from the protected computer directly to tape, there will be an impact on the disk resources and performance on the protected computer. The impact on performance is less when backing up file data than when backing up application data.

## <a name="BKMK_Process"></a>Running DPM processes
On the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server, three processes can impact performance:

-   **[!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] protection agent \(MsDpmProtectionAgent.exe\)**. [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] jobs affect both memory and CPU usage by the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] protection agent. It is normal for CPU usage by MsDpmProtectionAgent.exe to increase during consistency checks.

-   **[!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] service \(MsDpm.exe\)**. The [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] service affects both memory and CPU usage.

-   **[!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] Administrator Console \(an instance of Mmc.exe\)**. [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] Administrator Console can be a significant factor in high memory usage. You can close it when it is not in use.

> [!NOTE]
> Memory usage for the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] instance of the SQL Server service \(Microsoft$DPM$Acct.exe\) is expected to be comparatively high. This does not indicate a problem. The service normally uses a large amount of memory for caching, but it releases memory when available memory is low.

