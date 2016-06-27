---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  markgalioto
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-27
title:  Deduplicate DPM storage
ms.technology:  data-protection-manager
ms.assetid:  af49cdc3-1f63-4c10-843a-d1cd27af473a
---

# Deduplicate DPM storage
Data deduplication (dedup) finds and removed duplicated data in a volume  while ensuring data remains correct and complete.   Learn more about [deduplication planning](http://go.microsoft.com/fwlink/?LinkId=522614) .

-   Dedup reduces storage consumption and although the amount of redundancy for a set of data will depend on the workload and data type, typically backup data shows strong savings when dedup is used.

-   Data redundancy can be further reduced with dedup when backed up data of similar types and workloads is processed together.

-   Dedup is designed to be installed on primary data volumes without adding additional dedicated hardware so that it doesn’t impact the primary workload on the server. The default settings are nonintrusive because they allow data to age for five days before processing a particular file, and has a default minimum file size of 32 KB. The implementation is designed for low memory and CPU usage.

-   Dedup can be implemented on the following workloads:

    -   General file shares: Group content publication and sharing, user home folders, and Folder Redirection/Offline Files

    -   Software deployment shares: Software binaries, images, and updates

    -   VHD libraries: Virtual hard disk (VHD) file storage for provisioning to hypervisors

    -   VDI Deployments (Windows Server 2012 R2 only): Virtual Desktop Infrastructure (VDI) deployments using Hyper-V

    -   Virtualized backup: Backup solutions (such as DPM running in a Hyper-V virtual machine) that save backup data to VHD/VHDX files on a Windows File Server.

## DPM and dedup
Using dedup with DPM can result in large savings. The amount of space saved by dedup when optimizing DPM backup data varies depending on the type of data being backed up. For example, a backup of an encrypted database server may result in minimal savings since any duplicate data is hidden by the encryption process. However backup of a large Virtual Desktop Infrastructure (VDI) deployment can result in very large savings in the range of 70-90+% range, since there is typically a large amount of data duplication between the virtual desktop environments. In the configuration described in this topic we ran a variety of test workloads and saw savings ranging between 50% and 90%.

To use dedup for DPM storage DPM should be running in a Hyper-V virtual machine and store backup data to VHDs in shared folders with data dedup enabled.

## Recommended deployment
To deploy DPM as a virtual machine backing up data to a dedupl volume we recommend the following deployment topology:

-   DPM running in a virtual machine in a Hyper-V host cluster.

-   DPM storage using VHD/VHDX files stored on an SMB 3.0 share on a file server.

-   For our test example we configured the file server as a scaled-out file server (SOFS) deployed using storage volumes configured from Storage Spaces pools built using directly connected SAS drives. Note that this deployment ensures performance at scale.

Note that:

-   This deployment is supported for DPM 2012 R2, and for all workload data that can be backed up by DPM 2012 R2.

-   All the Windows File Server nodes on which DPM virtual hard disks reside and on which dedup will be enabled must be running Windows Server 2012 R2 with at least [Update Rollup November 2014](http://go.microsoft.com/fwlink/?LinkId=522571).

-   We’ll provide general recommendations and instructions for the scenario deployment. Whenever hardware-specific examples are given, the hardware deployed in the Microsoft Cloud Platform System (CPS) is used for reference.

-   This example uses remote SMB 3.0 shares to store the backup data, so primary hardware requirements center around the File Server nodes rather than the Hyper-V nodes. The following hardware configuration is used in CPS for backup and production storage. Note that the overall hardware is used for both backup and production storage, but the number of drives listed in the drive enclosures are only those used for backup.

    -   4 node Scale Out File Server cluster

    -   Per node configuration

        -   2x Intel(R) Xeon(R) CPU E5-2650 0 @ 2.00GHz, 2001 MHz, 8 cores, 16 logical processors

        -   128GB 1333MHz RDIMM memory

        -   Storage connections: 2 ports of SAS, 1 port of 10GbE iWarp/RDMA

    -   4 JBOD drive enclosures

        -   18 Disks in each JBOD – 16 x 4TB HDDs + 2 x 800GB SSDs

        -   Dual path to each drive - Multipath I/O load balancing policy set to failover only

        -   SSDs configured for write back cache (WBC) and the rest for dedicated journal drives

## Set up dedup volumes
Let’s consider how big volumes should be to support the deduplicated VHDX files containing DPM data. In CPS we’ve created volumes of 7.2TB each. The optimum volume size depends primarily on how much and how frequently the data on the volume changes, and on the data access throughput rates of the disk storage subsystem. It’s important to note that if the deduplication processing can’t keep up with the rate of daily data changes (the churn) the savings rate will drop until the processing can complete. For more detailed information see [Sizing Volumes for Data Deduplication](http://go.microsoft.com/fwlink/?LinkId=522575). The following general guidelines are recommended for the dedup volumes:

-   Use Parity Storage Spaces with enclosure-awareness for resiliency and increased disk utilization.

-   Format NTFS with 64 KB allocation units and large file record segments to work better with dedup use of sparse files.

-   In the hardware configuration above the recommended volume size is 7.2TB volumes and volumes will be configured as follows:

    -   Enclosure aware dual parity 7.2TB + 1GB Write back cache

        -   ResiliencySettingName == Parity

        -   PhysicalDiskRedundancy == 2

        -   NumberOfColumns == 7

        -   Interleave == 256KB (Dual parity performance at 64KB interleave is much lower than at the default 256KB interleave)

        -   IsEnclosureAware == $true

        -   AllocationUnitSize=64KB

        -   Large FRS

        Set up a new virtual disk in the specified storage pool as follows:

        ```
        New-VirtualDisk -Size 7.2TB -PhysicalDiskRedundancy 2 -ResiliencySettingName Parity -StoragePoolFriendlyName BackupPool -FriendlyName BackupStorage -NumberOfColumns 7 -IsEnclosureAware $true
        ```

    -   Each of these volumes must then be formatted as:

        ```
        Format-Volume -Partition <volume> -FileSystem NTFS -AllocationUnitSize 64KB –UseLargeFRS -Force
        ```

        In the CPS deployment, these are then configured as CSVs.

    -   Within these volumes DPM will store a series of VHDX files to hold the backup data. Enable deduplication on the volume after formatting it, as follows:

        ```
        Enable-DedupVolume –Volume <volume> -UsageType HyperV
        Set-DedupVolume -Volume <volume> -MinimumFileAgeDays 0 -OptimizePartialFiles:$false
        ```

        This command also modifies the following volume level dedup settings:

        -   Set **UsageType** to **HyperV**: This results in dedup processing open files, which is required because the VHDX files used for backup storage by DPM remain open with DPM running in its virtual machine.

        -   Disable PartialFileOptimization: This causes dedup to optimize all sections of an open file rather scan for changed sections with a minimum age.

        -   Set MinFileAgeDays parameter to 0: With PartialFileOptimization disabled, MinFileAgeDays changes its behavior so that dedup only considers files that haven’t changed in that many days. Since we want dedup to begin processing the backup data in all DPM VHDX files without any delay, we need to set MinFileAgeDays to 0.

For more information on setting up deduplication see [Install and Configure Data Duplication](http://go.microsoft.com/fwlink/?LinkId=522576).

## Set up DPM storage
To avoid fragmentation issues and maintain efficiency, DPM storage is allocated using VHDX files residing on the deduplicated volumes. 10 dynamic VHDX files of 1TB each are created on each volume and attached to DPM. Note that 3TB of overprovisioning of storage is done to take advantage of the storage savings produced by dedup. As dedup produces additional storage savings, new VHDX files can be created on these volumes to consume saved space. We tested the DPM sever with up to 30 VHDX files attached to it.

1.  Run the following command to create virtual hard disks that will be added later to the DPM server:

    ```
    New-SCVirtualDiskDrive -Dynamic -SCSI -Bus $Bus -LUN $Lun -JobGroup $JobGroupId -VirtualHardDiskSizeMB 1048576 -Path $Using:Path -FileName <VHDName>
    ```

2.  Then added the created virtual hard disks to the DPM server as follows:

    ```
    Import-Module "DataProtectionManager"
    Set-StorageSetting -NewDiskPolicy OnlineAll
    $dpmdisks = @()
    $dpmdisks = Get-DPMDisk -DPMServerName $env:computername | ? {$_.CanAddToStoragePool –
    eq $true -and $_.IsInStoragePool -eq $false -and $_.HasData -eq $false}
    Add-DPMDisk $dpmdisks
    ```

    Note that this step configures a storage pool as the disk or disks on which DPM stores replicas and recovery points for protected data. This pool is part of the DPM configuration and is separate from the Storage Spaces pool used to create the data volumes described in the previous section. For more information on DPM storage pools see [Configure disk storage and storage pools](http://go.microsoft.com/fwlink/?LinkId=522577).

## Set up the Windows File Server cluster
Dedup requires a special set of configuration options to support virtualized DPM storage due to the scale of data and size of individual files. These options are global to the cluster or the cluster node. Dedup must be enabled and the cluster settings must be individually configured on each node of the cluster.

1.  **Enable dedup on Windows File Server storage**— The Deduplication role must be installed on all nodes of the Windows File Server cluster. To do this run the following PowerShell command on each node of the cluster:

    ```
    Install-WindowsFeature -Name FileAndStorage-Services,FS-Data-Deduplication -ComputerName <node name>
    ```

2.  **Tune dedup processing for backup data files**—Run the following PowerShell command to set to start optimization without delay and not to optimize partial file writes. Note that by default Garbage Collection (GC) jobs are scheduled every week, and every fourth week the GC job runs in “deep GC” mode for a more exhaustive and time intensive search for data to remove. For the DPM workload, this “deep GC” mode does not result in any appreciative gains and reduces the amount of time in which dedup can optimize data. We therefore disable this deep mode.

    ```
    Set-ItemProperty -Path HKLM:\Cluster\Dedup -Name DeepGCInterval -Value 0xFFFFFFFF
    ```

3.  **Tune performance for large scale operations**—Run the following PowerShell script to:

    -   Disable additional processing and I/O when deep garbage collection runs

    -   Reserve additional memory for hash processing

    -   Enable priority optimization to allow immediate defragmentation of large files

    ```
    Set-ItemProperty -Path HKLM:\Cluster\Dedup -Name HashIndexFullKeyReservationPercent -Value 70
    Set-ItemProperty -Path HKLM:\Cluster\Dedup -Name EnablePriorityOptimization -Value 1
    ```

    These settings modify the following:

    -   HashIndexFullKeyReservationPercent: This value controls how much of the optimization job memory is used for existing chunk hashes, versus new chunk hashes. At high scale, 70% results in better optimization throughput than the 50% default.

    -   EnablePriorityOptimization: With files approaching 1TB, fragmentation of a single file can accumulate enough fragments to approach the per file limit. Optimization processing consolidates these fragments and prevents this limit from being reached. By setting this registry key, dedup will add an additional process to deal with highly fragmented deduped files with high priority.

## Set up DPM and dedup scheduling
Both backup and deduplication operations are I/O intensive. If they were to run at the same time, additional overhead to switch between the operations could be costly and result in less data being backed up or deduplicated on a daily basis. We recommended you configure dedicated and separate deduplication and backup windows. This helps ensure that the I/O traffic for each of these operations is efficiently distributed during daily system operation. The recommended guidelines for scheduling are:

-   Split days into non-overlapping backup and dedup windows.

-   Set up custom backup schedules.

-   Set up custom dedup schedules.

-   Schedule optimization in the daily dedup window.

-   Set up weekend dedup schedules separately, using that time for garbage collection and scrubbing jobs.

You can set up DPM schedules with the following PowerShell command:

```
Set-DPMConsistencyCheckWindow -ProtectionGroup $mpg -StartTime $startTime –
DurationInHours $duration
Set-DPMBackupWindow -ProtectionGroup $mpg -StartTime $startTime –DurationInHours
$duration
```

In this configuration, DPM is configured to back up virtual machines between 10 PM and 6 AM. Deduplication is scheduled for the remaining 16 hours of the day. Note that the actual dedup time you configure will depend on the volume size. See  [Sizing Volumes for Data Deduplication](http://go.microsoft.com/fwlink/?LinkId=522575) for more information. A 16 hour deduplication window starting at 6 AM after the backup window ends would be configured as follows from any individual cluster node:

```
#disable default schedule
Set-DedupSchedule * -Enabled:$false
#Remainder of the day after an 8 hour backup window starting at 10pm $dedupDuration = 16
$dedupStart = "6:00am"
#On weekends GC and scrubbing start one hour earlier than optimization job.
# Once GC/scrubbing jobs complete, the remaining time is used for weekend
# optimization.
$shortenedDuration = $dedupDuration - 1
$dedupShortenedStart = "7:00am"
#if the previous command disabled priority optimization schedule
#reenable it
if ((Get-DedupSchedule -name PriorityOptimization -ErrorAction SilentlyContinue) -ne $null)
{
Set-DedupSchedule -Name PriorityOptimization -Enabled:$true
}
#set weekday and weekend optimization schedules
New-DedupSchedule -Name DailyOptimization -Type Optimization -DurationHours $dedupDuration -Memory 50 -Priority Normal -InputOutputThrottleLevel None -Start $dedupStart -Days Monday,Tuesday,Wednesday,Thursday,Friday
New-DedupSchedule -Name WeekendOptimization -Type Optimization -DurationHours $shortenedDuration -Memory 50 -Priority Normal -InputOutputThrottleLevel None -Start $dedupShortenedStart -Days Saturday,Sunday
#re-enable and modify scrubbing and garbage collection schedules
Set-DedupSchedule -Name WeeklyScrubbing -Enabled:$true -Memory 50 -DurationHours $dedupDuration -Priority Normal -InputOutputThrottleLevel None -Start $dedupStart -StopWhenSystemBusy:$false -Days Sunday
Set-DedupSchedule -Name WeeklyGarbageCollection -Enabled:$true -Memory 50 -DurationHours $dedupDuration -Priority Normal -InputOutputThrottleLevel None -Start $dedupStart -StopWhenSystemBusy:$false -Days Saturday
#disable background optimization
if ((Get-DedupSchedule -name BackgroundOptimization -ErrorAction SilentlyContinue) -ne $null)
{
Set-DedupSchedule -Name BackgroundOptimization -Enabled:$false
}
```

Whenever the backup window is modified it’s vital that the deduplication window is modified along with it so they don’t overlap. The deduplication and backup window don’t have to fill up the full 24 hours of the day, but it’s highly recommended that they do to allow for variations in processing time due to expected daily changed in workloads and data churn.

## Implications for backup performance
After a set of files have been deduplicated there can be a slight performance cost when accessing the files. This is due to the additional processing required to access the file format used by deduplicated files. In this scenario, the files are a set of VHDX files that see continuous usage by DPM during the backup window. The impact of having these files deduplicated means that the backup and recovery operations can be slightly slower than without deduplication. As for any backup product, DPM is a write-heavy workload with read operations being most important during restore operations. The recommendations for addressing the implications for backup performance due to deduplication are:

-   Read/restore operations: Effects on read operations are typically negligible and don’t require any special considerations since the deduplication feature caches deduplicated chunks.

-   Write / backup operations: Plan for an increase in backup time of approximately 5% to 10 % when defining the backup window. (This is an increase compared to the expected backup time when writing to non-deduplicated volumes.)

## Monitoring
DPM and data deduplication can be monitored to ensure that:

-   Sufficient disk space is provisioned to store the backup data

-   DPM backup jobs are completing normally

-   Deduplication is enabled on the backup volumes

-   Deduplication schedules are set correctly

-   Deduplication processing is completing normally on a daily basis

-   Deduplication savings rate matches assumptions made for system configuration

The success of deduplication depends on the overall system hardware capabilities (including CPU processing speed, I/O bandwidth, storage capacity), correct system configuration, the average system load, and the daily amount of modified data.

You can monitor DPM using the DPM Central Console. See [Install Central Console](http://go.microsoft.com/fwlink/?LinkId=522578).

You can monitor dedup to check the dedup status, saving rate and schedule status using the following PowerShell commands:

Get status:

```
PS C:\> Get-DedupStatus
FreeSpace SavedSpace OptimizedFiles InPolicyFiles Volume
-------------- ---------- -------------- ------------- ------
280.26 GB 529.94 GB 36124 36125 X:
151.26 GB 84.19 GB 43017 43017 Z:
```

Get savings:

```
PS C:\> Get-DedupVolume
Enabled SavedSpace SavingsRate Volume
------- ---------- ----------- ------
True 529.94 GB 74 % X:
```

Get the schedule status using the Get-DedupSchedule cmdlet.

### Monitor events
Monitoring the event log can help understand deduplication events and status.

-   To view deduplication events, in **File Explorer**, navigate to **Applications and Services Logs** > **Microsoft** > **Windows** > **Deduplication**.

-   If the value **LastOptimizationResult = 0x00000000** appears in the Get-DedupStatus |fl Windows PowerShell results, the entire dataset was processed by the previous optimization job. If not then the system was unable to complete the deduplication processing and you might want to check your configuration settings, for example volume size.

For more detailed cmdlet examples, see [Monitor and Report for Data Deduplication](http://go.microsoft.com/fwlink/?LinkId=522579).

### Monitor backup storage
In our configuration example the 7.2 TB volumes are filled with 10 TB of "logical" data (the size of the data when it is not deduplicated) stored in 10 x 1 TB dynamic VHDX files. As these files accumulate additional backup data, they’ll slowly fill up the volume. If the savings percentage resulting from deduplication is high enough, all 10 files will be able to reach their maximum logical size but still fit in the 7.2 TB volume (potentially there might even be additional space to allocate additional VHDX files for DPM servers to use). But if the size savings from deduplication aren’t sufficient, the space on the volume might run out before the VHDX files reach their full logical size, and the volume will be full. To prevent volumes becoming full we recommend the following:

-   Be conservative in volume size requirements and allow for some overprovisioning of storage. It is recommended to allow for a buffer of at least 10% when planning for backup storage usage to allow for expected variation in deduplication savings and data churn.

-   Monitor the volumes used for backup storage to ensure that space utilization and deduplication savings rates are at expected levels.

If the volume becomes full the following symptoms result:

-   The DPM virtual machine will be put into a pause-critical state and no further backup jobs can be issued by that VM.

-   All backup jobs that use the VHDX files on the full volume will fail.

To recover from this condition and restore the system to normal operation, additional storage can be provisioned and a storage migration of the DPM virtual machine or its VHDX can be performed to free up space:

1.  Stop the DPM Server that owns the VHDX files on the full backup share.

2.  Create an additional volume and backup share using the same configuration and settings as used for the existing shares, including settings for NTFS and deduplication.

3.  **Migrate Storage** for the DPM Server virtual machine, and migrate at least one VHDX file from the full backup share to the new backup share created in step 2.

4.  Run a Data Deduplication garbage collection (GC) job on the source backup share that was full. The GC job should succeed and reclaim the free space.

5.  Restart the DPM Server virtual machine.

6.  A DPM consistency check job will be triggered during the next backup window for all data sources which previously failed.

7.  All backup jobs should now succeed.

## Summary
The combination of deduplication and DPM provides substantial space savings. This allows higher retention rates, more frequent backups, and better TCO for the DPM deployment. The guidance and recommendations in this document should provide you with the tools and knowledge to configure deduplication for DPM storage and see the benefits for yourself in your own deployment.

## Common questions
**Q:** DPM VHDX files need to be 1TB of size. Does this mean DPM cannot backup a VM or SharePoint or SQL DB or file volume of size > 1TB?

**A:** No. DPM aggregates multiple volumes into one to store backups. So, the 1TB file size doesn’t have any implications for data source sizes that DPM can backup.

**Q:** It looks as though DPM storage VHDX files must be deployed on remote SMB file shares only. What will happen if I store the backup VHDX files on dedup-enabled volumes on the same system where the DPM virtual machine is running?

**A:** As discussed above, DPM, Hyper-V and dedup are storage and compute intensive operations. Combining all three of them in a single system can lead to I/O and process intensive operations that could starve Hyper-V and its VMs. If you decide to experiment configuring DPM in a VM with the backup storage volumes on the same machine, you should monitor performance carefully to ensure that there is enough I/O bandwidth and compute capacity to maintain all three operations on the same machine.

**Q:** You recommend dedicated, separate deduplication and backup windows. Why can’t I enable dedup while DPM is backing up? I need to backup my SQL DB every 15 minutes.

**A:** Dedup and DPM are storage intensive operations and having both of them running at the same time can be inefficient and lead to I/O starvation. Therefore, to protect workloads more than once a day (for example SQL Server every 15 minutes) and to enable dedup at the same time, ensures there’s enough I/O bandwith and computer capacity to avoid resource starvation.

**Q:** Based on the configuration described, DPM needs to be running in a virtual machine. Why can’t I enable dedup on replica volume and shadow copy volumes directly rather than on VHDX files?

**A:** Dedup does deduplication per volume operating on individual files. Since dedup optimizes at the file level, it is not designed to support the VolSnap technology that DPM leverages to store its backup data. By running DPM in a VM, Hyper-V maps the DPM volume operations to the VHDX file level, allowing dedup to optimize backup data and provide larger storage savings.

**Q:** The above sample configuration has created only 7.2TB volumes. Can I create bigger or smaller volumes?

**A:** Dedup runs one thread per volume. As the volume size becomes bigger, dedup requires more time to complete its optimization. On the other hand with small volumes there is less data in which to find duplicate chunks, which can result in reduced savings. So, it is advisable to fine tune the volume size based on total churn and system hardware capabilities for optimal savings. More detailed information on determining volume sizes used with deduplication can be found in Sizing volumes for Deduplication in Windows Server. For more detailed information on determining volume sizes used with deduplication see [Sizing Volumes for Data Deduplication](http://go.microsoft.com/fwlink/?LinkId=522575).


