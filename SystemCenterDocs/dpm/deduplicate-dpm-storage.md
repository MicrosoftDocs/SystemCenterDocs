---
description: You can use data deduplication in DPM storage to find and remove duplicated data in a volume to ensure that data remains correct and complete.
ms.topic: concept-article
ms.service: system-center
keywords:
ms.date: 01/28/2026
title: Deduplicate DPM storage
ms.subservice: data-protection-manager
ms.assetid: af49cdc3-1f63-4c10-843a-d1cd27af473a
author: Jeronika-MS
ms.author: v-gajeronika
ms.custom: engagement-fy24
---

# Deduplicate DPM storage


System Center Data Protection Manager (DPM) can use data deduplication.

Data deduplication (dedup) finds and removes duplicated data in a volume while ensuring data remains correct and complete. Learn more about [deduplication planning](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831700(v=ws.11)).

- Dedup reduces storage consumption. Although the amount of redundancy for a set of data depends on the workload and data type, typically backup data shows strong savings when dedup is used.

- You can further reduce data redundancy with dedup when backed up data of similar types and workloads is processed together.

- Dedup is designed to be installed on primary data volumes without additional dedicated hardware so that it doesn't affect the primary workload on the server. The default settings are nonintrusive, as they allow data to age for five days before processing a particular file and have a default minimum file size of 32 KB. The implementation is designed for low memory and CPU usage.

- You can implement dedup on the following workloads:

    - General file shares: Group content publication and sharing, user home folders, and Folder Redirection/Offline Files

    - Software deployment shares: Software binaries, images, and updates

    - VHD libraries: Virtual hard disk (VHD) file storage for provisioning to hypervisors

    - VDI Deployments (Windows Server 2012 R2 only): Virtual Desktop Infrastructure (VDI) deployments using Hyper-V

    - Virtualized backup: Backup solutions (such as DPM running in a Hyper-V virtual machine) that save backup data to VHD/VHDX files on a Windows File Server

## DPM and deduplication

Using deduplication with DPM can result in large savings. The amount of space saved by deduplication when optimizing DPM backup data varies depending on the type of data being backed up. For example, a backup of an encrypted database server might result in minimal savings since the encryption process hides any duplicate data. However, backup of a large Virtual Desktop Infrastructure (VDI) deployment can result in large savings in the range of 70-90+%, since there's typically a large amount of data duplication between the virtual desktop environments. In the configuration described in the article, you run various test workloads and see savings ranging between 50% and 90%.

To use deduplication for DPM storage, run DPM in a Hyper-V virtual machine and store backup data to VHDs in shared folders with data deduplication enabled.

## Recommended deployment

To deploy DPM as a virtual machine backing up data to a deduplication volume, use the following deployment topology:

- DPM running in a virtual machine in a Hyper-V host cluster.

- DPM storage using VHD and VHDX files stored on an SMB 3.0 share on a file server.

- For the test example, the file server is configured as a scale-out file server (SOFS) deployed using storage volumes configured from Storage Spaces pools built using directly connected SAS drives. This deployment ensures performance at scale.

Note the following information:

- DPM supports this deployment for DPM 2012 R2 and later and for all workload data that DPM 2012 R2 and later can back up.

- All the Windows File Server nodes where DPM virtual hard disks reside and where deduplication is enabled must run Windows Server 2012 R2 with [Update Rollup November 2014](https://go.microsoft.com/fwlink/?LinkId=522571) or later.

- The article provides general recommendations and instructions for the scenario deployment. Whenever hardware-specific examples are given, the hardware deployed in the Microsoft Cloud Platform System (CPS) is used for reference.

- This example uses remote SMB 3.0 shares to store the backup data, so primary hardware requirements center around the File Server nodes rather than the Hyper-V nodes. The following hardware configuration is used in CPS for backup and production storage. The overall hardware is used for both backup and production storage, but the number of drives listed in the drive enclosures are only those used for backup.

    - Four node Scale Out File Server cluster

    - Per node configuration

        - 2x Intel(R) Xeon(R) CPU E5-2650 0 @ 2.00 GHz, 2001 MHz, 8 cores, 16 logical processors

        - 128 GB 1333 MHz RDIMM memory

        - Storage connections: 2 ports of SAS, 1 port of 10 GbE iWarp/RDMA

    - Four JBOD drive enclosures

        - 18 Disks in each JBOD - 16 x 4 TB HDDs + 2 x 800 GB SSDs

        - Dual path to each drive - Multipath I/O load-balancing policy set to fail over only

        - SSDs configured for write-back cache (WBC) and the rest for dedicated journal drives

## Set up dedup volumes

Consider how big volumes should be to support the deduplicated VHDX files containing DPM data. In CPS, create volumes of 7.2 TB each. The optimum volume size depends primarily on how much and how frequently the data on the volume changes, and on the data access throughput rates of the disk storage subsystem. If the deduplication processing can't keep up with the rate of daily data changes (the churn), the savings rate drops until the processing can complete. For more detailed information, see [Sizing Volumes for Data Deduplication](https://go.microsoft.com/fwlink/?LinkId=522575). The following general guidelines are recommended for dedup volumes:

- Use Parity Storage Spaces with enclosure-awareness for resiliency and increased disk utilization.

- Format NTFS with 64-KB allocation units and large file record segments to work better with dedup use of sparse files.

- In the hardware configuration above the recommended volume size of 7.2-TB volumes, configure volumes as follows:

    - Enclosure aware dual parity 7.2 TB + 1 GB Write-back cache

        - ResiliencySettingName == Parity

        - PhysicalDiskRedundancy == 2

        - NumberOfColumns == 7

        - Interleave == 256 KB (Dual parity performance at 64 KB interleave is much lower than at the default 256 KB interleave)

        - IsEnclosureAware == $true

        - AllocationUnitSize=64 KB

        - Large FRS

        Set up a new virtual disk in the specified storage pool as follows:

        ```
        New-VirtualDisk -Size 7.2TB -PhysicalDiskRedundancy 2 -ResiliencySettingName Parity -StoragePoolFriendlyName BackupPool -FriendlyName BackupStorage -NumberOfColumns 7 -IsEnclosureAware $true
        ```

    - Format each of these volumes as:

        ```
        Format-Volume -Partition <volume> -FileSystem NTFS -AllocationUnitSize 64 KB -UseLargeFRS -Force
        ```

        In the CPS deployment, configure these volumes as CSVs.

    - Within these volumes, DPM stores a series of VHDX files to hold the backup data. Enable deduplication on the volume after formatting it as follows:

        ```
        Enable-DedupVolume -Volume <volume> -UsageType HyperV
        Set-DedupVolume -Volume <volume> -MinimumFileAgeDays 0 -OptimizePartialFiles:$false
        ```

        This command also modifies the following volume-level dedup settings:

        - Set **UsageType** to **HyperV**: This setting results in dedup processing open files, which are required because the VHDX files used for backup storage by DPM remain open with DPM running in its virtual machine.

        - Disable PartialFileOptimization: This setting causes dedup to optimize all sections of an open file rather than scan for changed sections by using a minimum age.

        - Set MinFileAgeDays parameter to 0: With PartialFileOptimization disabled, MinFileAgeDays changes its behavior so that dedup only considers files that haven't changed in that many days. To make sure dedup begins processing the backup data in all DPM VHDX files without any delay, set MinFileAgeDays to 0.

For more information on setting up deduplication, see [Install and Configure Data Duplication](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831434(v=ws.11)).

## Set up DPM storage

To avoid fragmentation problems and maintain efficiency, allocate DPM storage by using VHDX files that reside on the deduplicated volumes. Create ten dynamic VHDX files of 1 TB each on each volume and attach them to DPM. Also, overprovision 3 TB of storage to take advantage of the storage savings that dedup provides. As dedup provides additional storage savings, you can create new VHDX files on these volumes to consume the saved space. We tested the DPM server with up to 30 VHDX files attached to it.

1. Run the following command to create virtual hard disks that you later add to the DPM server:

    ```
    New-SCVirtualDiskDrive -Dynamic -SCSI -Bus $Bus -LUN $Lun -JobGroup $JobGroupId -VirtualHardDiskSizeMB 1048576 -Path $Using:Path -FileName <VHDName>
    ```

1. Add the created virtual hard disks to the DPM server as follows:

    ```
    Import-Module "DataProtectionManager"
    Set-StorageSetting -NewDiskPolicy OnlineAll
    $dpmdisks = @()
    $dpmdisks = Get-DPMDisk -DPMServerName $env:computername | ? {$_.CanAddToStoragePool -
    eq $true -and $_.IsInStoragePool -eq $false -and $_.HasData -eq $false}
    Add-DPMDisk $dpmdisks
    ```

    This step configures a storage pool as the disk or disks on which DPM stores replicas and recovery points for protected data. This pool is part of the DPM configuration and is separate from the Storage Spaces pool used to create the data volumes described in the previous section. For more information on DPM storage pools, see [Configure disk storage and storage pools](/previous-versions/system-center/system-center-2012-R2/hh758075(v=sc.12)).

## Set up the Windows File Server cluster

Deduplication requires a special set of configuration options to support virtualized DPM storage due to the scale of data and size of individual files. These options are global to the cluster or the cluster node. You must enable deduplication and individually configure the cluster settings on each node of the cluster.

1. **Enable deduplication on Windows File Server storage**- Install the Deduplication role on all nodes of the Windows File Server cluster. To do this, run the following PowerShell command on each node of the cluster:

    ```powershell
    Install-WindowsFeature -Name FileAndStorage-Services,FS-Data-Deduplication -ComputerName <node name>
    ```

2. **Tune dedup processing for backup data files**- Run the following PowerShell command to set to start optimization without delay and not to optimize partial file writes. By default, garbage collection (GC) jobs are scheduled every week, and every fourth week, the GC job runs in "deep GC" mode for a more exhaustive and time-intensive search for data to remove. For the DPM workload, this "deep GC" mode doesn't result in any appreciative gains and reduces the amount of time in which deduplication can optimize data. Disable this deep mode.

    ```
    Set-ItemProperty -Path HKLM:\Cluster\Dedup -Name DeepGCInterval -Value 0xFFFFFFFF
    ```

3. **Tune performance for large scale operations**- Run the following PowerShell script to:

    - Disable extra processing and I/O when deep garbage collection runs

    - Reserve extra memory for hash processing

    - Enable priority optimization to allow immediate defragmentation of large files

    ```
    Set-ItemProperty -Path HKLM:\Cluster\Dedup -Name HashIndexFullKeyReservationPercent -Value 70
    Set-ItemProperty -Path HKLM:\Cluster\Dedup -Name EnablePriorityOptimization -Value 1
    ```

    These settings modify the following:

    - HashIndexFullKeyReservationPercent: This value controls how much of the optimization job memory is used for existing chunk hashes versus new chunk hashes. At high scale, 70% results in better optimization throughput than the 50% default.

    - EnablePriorityOptimization: With files approaching 1 TB, fragmentation of a single file can accumulate enough fragments to approach the per file limit. Optimization processing consolidates these fragments and prevents this limit from being reached. By setting this registry key, deduplication adds an extra process to deal with highly fragmented deduped files with high priority.

## Set up DPM and dedup scheduling

Both backup and deduplication operations are I/O intensive. If they run at the same time, the extra overhead to switch between the operations can be costly. You might back up or deduplicate less data on a daily basis. Configure dedicated and separate deduplication and backup windows. This configuration helps ensure that the I/O traffic for each of these operations is efficiently distributed during daily system operation. The recommended guidelines for scheduling are:

- Split days into non-overlapping backup and deduplication windows.

- Set up custom backup schedules.

- Set up custom deduplication schedules.

- Schedule optimization in the daily deduplication window.

- Set up weekend deduplication schedules separately. Use that time for garbage collection and scrubbing jobs.

Set up DPM schedules by using the following PowerShell command:

```powershell
Set-DPMConsistencyCheckWindow -ProtectionGroup $mpg -StartTime $startTime -
DurationInHours $duration
Set-DPMBackupWindow -ProtectionGroup $mpg -StartTime $startTime -DurationInHours
$duration
```

In this configuration, DPM backs up virtual machines between 10 PM and 6 AM. Deduplication is scheduled for the remaining 16 hours of the day. The actual deduplication time you configure depends on the volume size. For more information, see [Sizing Volumes for Data Deduplication](https://go.microsoft.com/fwlink/?LinkId=522575). A 16-hour deduplication window starting at 6 AM after the backup window ends would be configured as follows from any individual cluster node:

```powershell
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

Whenever you modify the backup window, modify the deduplication window along with it so that they don't overlap. The deduplication and backup window don't have to fill up the full 24 hours of the day. However, it's highly recommended that they do to allow for variations in processing time due to expected daily changes in workloads and data churn.

## Implications for backup performance

After a set of files is deduplicated, there's a slight performance cost when accessing the files. This cost comes from the extra processing required to access the file format used by deduplicated files. In this scenario, the files are a set of VHDX files that DPM sees continuous usage of during the backup window. The effect of having these files deduplicated means that the backup and recovery operations can be slightly slower than without deduplication. As with any backup product, DPM is a write-heavy workload with read operations being most important during restore operations. The recommendations for addressing the implications for backup performance due to deduplication are:

- Read and restore operations: Effects on read operations are typically negligible and don't require any special considerations since the deduplication feature caches deduplicated chunks.

- Write and backup operations: Plan for an increase in backup time of 5-10% when defining the backup window. This increase is compared to the expected backup time when writing to non-deduplicated volumes.

## Monitoring

You can monitor DPM and data deduplication to make sure that:

- You have enough disk space to store the backup data.

- DPM backup jobs finish normally.

- Deduplication is enabled on the backup volumes.

- Deduplication schedules are set correctly.

- Deduplication processing finishes normally each day.

- Deduplication savings rate matches the assumptions made for the system configuration.

The success of deduplication depends on the overall system hardware capabilities, including CPU processing speed, I/O bandwidth, and storage capacity. It also depends on correct system configuration, the average system load, and the daily amount of modified data.

Use the DPM Central Console to monitor DPM. For more information, see [Install Central Console](/previous-versions/system-center/system-center-2012-R2/hh758189(v=sc.12)).

To check the dedup status, saving rate, and schedule status, use the following PowerShell commands:

Get status:

```powershell
PS C:\> Get-DedupStatus
FreeSpace SavedSpace OptimizedFiles InPolicyFiles Volume
-------------- ---------- -------------- ------------- ------
280.26 GB 529.94 GB 36124 36125 X:
151.26 GB 84.19 GB 43017 43017 Z:
```

Get savings:

```powershell
PS C:\> Get-DedupVolume
Enabled SavedSpace SavingsRate Volume
------- ---------- ----------- ------
True 529.94 GB 74 % X:
```

Get the schedule status by using the `Get-DedupSchedule` cmdlet.

### Monitor events

Monitoring the event log can help you understand deduplication events and status.

- To view deduplication events, in **File Explorer**, go to **Applications and Services Logs** > **Microsoft** > **Windows** > **Deduplication**.

- If the value **LastOptimizationResult = 0x00000000** appears in the `Get-DedupStatus |fl` Windows PowerShell results, the previous optimization job processed the entire dataset. If the value doesn't appear, the system couldn't complete the deduplication processing. You might want to check your configuration settings, such as the volume size.

For more detailed cmdlet examples, see [Monitor and Report for Data Deduplication](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831505(v=ws.11)).

### Monitor backup storage

In this configuration example, the 7.2-TB volumes store 10 TB of "logical" data (the size of the data when it isn't deduplicated) in 10 x 1 TB dynamic VHDX files. As these files accumulate additional backup data, they slowly fill up the volume. If the savings percentage resulting from deduplication is high enough, all 10 files reach their maximum logical size and still fit in the 7.2-TB volume (potentially there might even be additional space to allocate extra VHDX files for DPM servers to use). But if the size savings from deduplication aren't sufficient, the space on the volume runs out before the VHDX files reach their full logical size and the volume is full. To prevent volumes from becoming full, follow these recommendations:

- Be conservative in volume size requirements and allow for some overprovisioning of storage. Allow for a buffer of at least 10% when planning for backup storage usage to account for expected variations in deduplication savings and data churn.

- Monitor the volumes used for backup storage to ensure that space utilization and deduplication savings rates are at expected levels.

If the volume becomes full, the following symptoms occur:

- The DPM virtual machine goes into a pause-critical state and can't issue any further backup jobs.

- All backup jobs that use the VHDX files on the full volume fail.

To recover from this condition and restore the system to normal operation, you can provision additional storage and perform a storage migration of the DPM virtual machine or its VHDX to free up space:

1. Stop the DPM Server that owns the VHDX files on the full backup share.

2. Create an additional volume and backup share using the same configuration and settings as used for the existing shares, including settings for NTFS and deduplication.

3. **Migrate Storage** for the DPM Server virtual machine and migrate at least one VHDX file from the full backup share to the new backup share created in step 2.

4. Run a Data Deduplication garbage collection (GC) job on the source backup share that was full. The GC job should succeed and reclaim the free space.

5. Restart the DPM Server virtual machine.

6. A DPM consistency check job triggers during the next backup window for all data sources that failed previously.

7. All backup jobs now succeed.

## Summary

The combination of deduplication and DPM provides substantial space savings. This combination supports higher retention rates, more frequent backups, and better TCO for the DPM deployment. The guidance and recommendations in this article provide you with the tools and knowledge to configure deduplication for DPM storage and see the benefits for yourself in your own deployment.

## Common questions

**Q:** DPM VHDX files need to be 1 TB in size. Does this requirement mean DPM can't back up a VM or SharePoint or SQL DB or file volume of size greater than 1 TB?

**A:** No. DPM aggregates multiple volumes into one to store backups. So, the 1-TB file size doesn't affect data source sizes that DPM can back up.

**Q:** It looks as though DPM storage VHDX files must be deployed on remote SMB file shares only. What happens if I store the backup VHDX files on dedup-enabled volumes on the same system where the DPM virtual machine is running?

**A:** As discussed earlier, DPM, Hyper-V, and deduplication are storage- and compute-intensive operations. Combining all three of them in a single system can lead to I/O- and process-intensive operations that starve Hyper-V and its VMs. If you decide to experiment with configuring DPM in a VM with the backup storage volumes on the same machine, monitor performance carefully to ensure that there's enough I/O bandwidth and compute capacity to maintain all three operations on the same machine.

**Q:** You recommend dedicated, separate deduplication and backup windows. Why can't I enable deduplication while DPM is backing up? I need to back up my SQL DB every 15 minutes.

**A:** Deduplication and DPM are storage-intensive operations. Running both of them at the same time can be inefficient and lead to I/O starvation. To protect workloads more than once a day (for example SQL Server every 15 minutes) and to enable deduplication at the same time, ensure that there's enough I/O bandwidth and computer capacity to avoid resource starvation.

**Q:** Based on the configuration described, DPM needs to be running in a virtual machine. Why can't I enable deduplication on replica volume and shadow copy volumes directly rather than on VHDX files?

**A:** Deduplication works per volume and operates on individual files. Since deduplication optimizes at the file level, it's not designed to support the VolSnap technology that DPM uses to store its backup data. By running DPM in a VM, Hyper-V maps the DPM volume operations to the VHDX file level, which allows deduplication to optimize backup data and provide larger storage savings.

**Q:** The preceding sample configuration creates only 7.2-TB volumes. Can I create bigger or smaller volumes?

**A:** Deduplication runs one thread per volume. As the volume size becomes bigger, deduplication requires more time to complete its optimization. On the other hand with small volumes, there's less data in which to find duplicate chunks, which can result in reduced savings. So, fine-tune the volume size based on total churn and system hardware capabilities for optimal savings. For more detailed information on determining volume sizes used with deduplication, see [Sizing Volumes for Data Deduplication](https://go.microsoft.com/fwlink/?LinkId=522575).
