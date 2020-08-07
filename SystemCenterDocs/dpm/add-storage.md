---
description: Learn about the new features when you upgrade to DPM 2016 and later. This article also provides an overview of how to upgrade your DPM installation.
manager: carmonm
ms.topic: article
author: rayne-wiselman
ms.author: raynew
ms.prod: system-center
keywords:
ms.date: 08/07/2020
title: Add Modern Backup Storage to DPM
ms.technology: data-protection-manager
ms.assetid: faebe568-d991-401e-a8ff-5834212f76ce
---

# Add Modern Backup Storage to DPM

::: moniker range="<=sc-dpm-1807"

Modern Backup Storage (MBS) was introduced in System Center Data Protection Manager (DPM) 2016 to deliver 50% storage savings, 3X faster backups, and more efficient, workload-aware storage.

- MBS is enabled automatically when you're running at least DPM 2016 on Windows Server 2016. If DPM is running on a version of Windows Server older than Windows Server 2016, it doesn't use MBS.
- MBS provides intelligent storage for short-term backup to disk.  MBS provides faster disk backup, consuming less disk space. Without MBS, each data source needs two volumes, one for the initial backup and the other for delta changes.
- MBS backups are stored on an ReFS disk. It uses ReFS block cloning, and VHDX technology, [Learn more](https://blogs.technet.microsoft.com/dpm/2016/10/19/introducing-dpm-2016-modern-backup-storage/).

> [!NOTE]
> DPM does not support deduplication on ReFS disk used for MBS backups.

DPM 2016 accepts volumes for storage. Once you add a volume, DPM formats the volume to ReFS to use the new features of Modern Backup Storage. Volumes cannot reside on a dynamic disk. Use only a basic disk.

While you can directly give a volume to DPM, you may face issues in extending the volume if a need arises later.
To prepare DPM for future expansion, use the available disks to create a storage pool, then create volumes on the storage pool, and expose the volumes to DPM. These virtual volumes can then be extended when needed.

The remainder of this article provides the detail on how to add a volume and to expand it later.

## Setting up MBS

Setting up MBS consists of the following procedures. Note that  you cannot attach locally created VHD (VHDX) files, and use them as storage on a physical DPM server.

1. Make sure you're running DPM 2016 or later on a VM running Windows Server 2016 or later.
2. Create a volume. To create a volume on a virtual disk in a storage pool:
    - Add a disk to the storage pool
    - Create a virtual disk from the storage pool, with layout set to Simple. You can then add additional disks, or extend the virtual disk.
    - Create volumes on the virtual disk.
3. Add the volumes to DPM.
4. Configure workload-aware storage.


## Create a volume

1. Create a storage pool in the File and Storage Services of Server Manager.
2. Add the available physical disks to the storage pool.
   - Adding only one disk to the pool keeps the column count to 1. You can then add disks as needed afterwards.
   - If multiple disks are added to the storage pool, the number of disks is stored as the number of columns. When more disks are added, they can only be a multiple of the number of columns.

     ![Add disks to storage pool](./media/add-storage/dpm2016-add-storage-1.png)

3. Create a virtual disk from the storage pool, with the layout set to Simple.

    ![Create virtual disk](./media/add-storage/dpm2016-add-storage-2.png)

4. Now add as many physical disks as needed.

    ![Add additional disks](./media/add-storage/dpm2016-add-storage-3.png)

5. Extend the virtual disk with the Simple layout, to reflect any physical disks you added.

    ![Extend virtual disks](./media/add-storage/dpm2016-add-storage-4.png)

6. Now, create volumes on the virtual disk.

    ![Create volume](./media/add-storage/dpm2016-add-storage-5.png)

    ![Select volume server and disk](./media/add-storage/dpm2016-add-storage-6.png)


## Add volumes to DPM storage


1. In the DPM Management console > **Disk Storage**, click **Rescan**.
2. In **Add Disk Storage**, click **Add**.
3. After the volumes are added, you can give them a friendly name.
4. Click **OK** to format the volumes to ReFS, so that DPM can use them as MBS.

    ![Review Disk Storage Allocation](./media/add-storage/dpm2016-add-storage-7.png)

## Configure workload-aware storage

Using workload-aware storage, the volumes can be selected to preferentially store specific workloads. For example, expensive volumes that support high IOPS can be configured to store workloads that need frequent, high-volume backups such as SQL Server with transaction logs. Workloads that are backed up less frequently, such as VMs, can be backed up to low-cost volumes.

You configure workload-aware storage using Windows PowerShell cmdlets.

### Update the volume properties

1. Run the **Update-DPMDiskStorage** to update the properties of a volume in the storage pool on a DPM server. The syntax is **Parameter Set: Volume**.
2. Run the cmdlet with these parameters.

    ```
    Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
    ```

    ![Review Disk Storage Allocation](./media/add-storage/dpm2016-add-storage-8.png)

3. The changes made using the PowerShell cmdlet are reflected in the DPM Management console.

    ![Review Disk Storage Allocation](./media/add-storage/dpm2016-add-storage-9.png)

## Volume Exclusion

DPM servers may be managed by a team of Administrators. While there are guidelines on storage that should be used for backups, a wrong volume given to DPM as backup storage may lead to loss of critical data. Hence, with DPM 2016 UR4 and later, you can prevent such scenarios by configuring those volumes to not be shown as available for storage using PowerShell.

For Example, to exclude F:\ and C:\MountPoint1, here are the steps:

1. Run the Set0DPMGlobalPropery commandlet:

    ```
    Set-DPMGlobalProperty -DPMStorageVolumeExclusion "F:,C:\MountPoint1"   
    ```
2. Rescan the storage through UI, or use Start-DPMDiskRescan cmdlet.

    The configured volumes and mountpoints are excluded.
3. To remove volume exclusion, run the following cmdlet:
    ```
    Set-DPMGlobalProperty -DPMStorageVolumeExclusion ""   
    ```
After removing volume exclusion, rescan the storage. All volumes and mount points, except System Volumes, are available for DPM storage.

## Backup Storage Migration

Once all your backups are on MBS, there may be a need to migrate certain datasources from one volume to another. For example, scenarios where you need to upgrade storage, or when a volume is getting full. You can use PowerShell or the user interface to migrate datasources. The details can be found [in this blog entry](https://go.microsoft.com/fwlink/?linkid=861519).

The migrating datasource should have all recovery points on Modern Storage. Migrating datasources with backups on disks and volumes (for example, DPM server upgrades when the disk backups haven't expired) is not supported.
Migration is similar to modification of a protection group. While migration is in progress, you cannot trigger an ad hoc job. The scheduled jobs continue as configured. When the migration completes, any running jobs in the protection group are preempted.

## Custom Size Allocation

DPM 2016 consumes storage thinly, as needed. Once DPM is configured for protection, it calculates the size of the data being backed up. If many files and folders are being backed up together, as in the case of a file server, size calculation can take long time. With DPM, you can configure DPM to accept the volume size as default instead of calculating the size of each file. The corresponding registry key is "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\Configuration\DiskStorage" with the Key, "EnableCustomAllocationOnReFSStorage" as a String set to 1 to enable custom size allocation, set to 0 for default size allocation with DPM.


::: moniker-end

::: moniker range="sc-dpm-2019"

Modern Backup Storage (MBS) was introduced in System Center Data Protection Manager (DPM) 2016 to deliver 50% storage savings, 3X faster backups, and more efficient, workload-aware storage. DPM 2019 introduces further performance improvements with MBS resulting in 50-70% faster backup with Windows Server 2019.

> [!NOTE]
> We recommend you to deploy DPM 2019 (using tiered volumes) on Windows Server 2019 to achieve enhanced backup performances.

- MBS is enabled automatically when you're running at least DPM 2016 on Windows Server 2016. If DPM is running on a version of Windows Server earlier than Windows Server 2016, it doesn't use MBS.
-   MBS provides intelligent storage for short-term backup to disk. MBS provides faster disk backup, consuming less disk space. Without MBS, each data source needs two volumes, one for the initial backup and the other for delta changes.
- MBS backups are stored on an ReFS disk. It uses ReFS block cloning, and VHDX technology.[Learn more](https://blogs.technet.microsoft.com/dpm/2016/10/19/introducing-dpm-2016-modern-backup-storage/).
- With DPM 2019 and later, you can use tiered volumes for DPM native storage which delivers 50-70% faster backups

> [!NOTE]
> DPM does not support deduplication on ReFS disk used for MBS backups.

DPM 2019 accepts volumes/disks for storage. Once you add a volume, DPM formats the volume to ReFS to use the new features of Modern Backup Storage. Volumes cannot reside on a dynamic disk, use only a basic disk.

> [!NOTE]
> If the physical disk is or will be larger than 2TB, the disk must be converted to GPT before creating the volume(s) for DPM.

You can directly give a volume to DPM, however, you may have issues in extending the volume if a need arises later. You can create additional volumes using storage pools, which could be exposed to DPM and extended as needed. The following sections provide the details on how to create a tiered volume, add a volume to DPM, and expand it later

## Set up MBS with Tiered Storage

DPM 2016 introduced Modern Backup Storage (MBS), improving storage utilization and performance. MBS uses ReFS as underlying filesystem. MBS is designed to make use of hybrid storage such as tiered storage. To achieve the scale and performance claimed by MBS, we recommend using a small percentage (4% of overall storage) of flash storage (SSD) with DPM 2019 as a tiered volume in combination with HDD for DPM native storage.

Once you configure tiered storage, the ReFs file system has the intelligence to store File System Metadata on the SSD tier. This improves the overall backup job time significantly. There is no further configuration required while configuring the protection groups, etc.

> [!NOTE]
> - Tiering is recommended for faster backups. However, this is not a mandatory requirement to configure DPM storage.
>- You cannot attach locally created VHD (VHDX) files, and use them as storage on a physical DPM server. Make sure you are running DPM 2019 or later deployed on a VM running on Windows Server 2016 or later.  
> - When deploying DPM in a virtual machine, DPM 2019 can be deployed in a VM running on Windows Server 2016 or Windows Server 2019. For best performance we strongly recommend DPM 2019 installed on Windows 2019 with the latest Windows update installed.  

Follow the steps in the procedures below to set up MBS with tiered storage. Follow the procedures in sequence, as listed below.

1. Configure DPM storage.
    > [!NOTE]
    > Migrate your current backups to a temporary volume using [Volume Migration](#migrate-data-to-newly-created-volumes), in case you wish to modify your existing storage to tiered storage.

    - Create a storage pool.
    - Create a virtual disk from the storage pool, with layout set to Simple. You can then add additional disks, or extend the virtual disk.
    - Create tiered/simple volumes on the virtual disk.

2.  Add the volumes to DPM.
3.  Migrate your data back to the newly created volumes using Volume Migration performed in Step 1.
    > [!NOTE]
    > Applicable only if you have migrated your earlier backups in Step 1.

4.  Configure workload-aware storage.

## Prerequisites

The tiered storage is configured using [Windows Storage Spaces](https://docs.microsoft.com/windows-server/storage/storage-spaces/overview). Following are the prerequisites for Windows Storage Spaces.

|Area | Requirement | Notes |
|---- |--------------|----|
|Disk bus types|- Serial Attached SCSI (SAS)<br><br> - Serial Advanced Technology Attachment (SATA) <br><br> - iSCSI and Fibre Channel Controllers.| When you configure Storage Spaces utilizing iSCSI and Fibre Channel (FC) disk controllers,  only non-resilient virtual disks (simple with any number of columns) are supported.|
|HBA considerations|- Simple host bus adapters (HBAs) that do not support RAID functionality are recommended <br><br> - If RAID-capable, HBAs must be in non-RAID mode with all RAID functionality disabled <br><br> - Adapters must not abstract the physical disks, cache data, or obscure any attached devices. This includes enclosure services that are provided by attached just-a-bunch-of-disks (JBOD) devices.|Storage Spaces is compatible only with HBAs where you can completely disable all RAID functionality.|

> [!NOTE]
> To configure tiered storage, Windows Storage Spaces requires minimum SSD disk size of 32 GB.

For more information on prerequisites for using Storage Spaces on a stand-alone server, see [Prerequisites to use Storage Spaces on a stand-alone server](https://docs.microsoft.com/windows-server/storage/storage-spaces/deploy-standalone-storage-spaces#prerequisites).

## Supported topology

To configure tiered storage, the storage can be directly attached to the DPM server or it can be from the external storage like SAN. The combination of directly attached storage and external storage can also be used.

Here are the possible storage combinations that are supported in both Physical DPM server or Virtual DPM Server scenario.

- Internal SSD and HDD
- External SSD and HDD
- Internal SSD, External HDD


> [!NOTE]
> - For DPM running on virtual machines, configuring tiered storage using Windows Storage Spaces is supported.
> - Hyper-V host presents both, the virtual SSD and HHD to the Virtual machine.
> - Virtual SSD should be carved out of physical SSD which could be directly attached to the Hyper-V host or from connected external storage.  

![Physical server deployment](./media/add-storage/physical-server-deployment.png)

### Resiliency

DPM supports all the three resiliency types supported by Windows Storage spaces. To configure mirror or parity mode resiliency for tiered volume multiple SSDs are required along with HDDs. When you configure simple resiliency type using a single SSD option, there might be data loss if the SSD becomes unavailable.

The below chart highlights some pros and cons of the three types of resiliency, supported by Windows Storage Spaces.

| TYPE | PRO | CON | Min Disks |
| --- | --- | --- | --- |
| Simple | - Max disk capacity (100%). <br><br> - Increased throughput. <br><br> - Stripes data across physical disks if applicable. | - No resiliency. <br><br> - Data loss guaranteed in case of physical disk failure.| 1 |
| Mirror | - Increased reliability.<br><br> - Greater data throughput and lower access latency than parity. <br><br> - Stripes the data across multiple physical drives. Can be configured for 2 or 3 copies of data. | - Reduced capacity (50%). <br><br> - Not supported on Iscsi or FC connected SAN. | 2 or 5 |
| Parity | - Stripes data and parity information across physical disks. <br><br> - Increased reliability. <br><br> - Increases resiliency through journaling. | - Reduced capacity, but not as much as mirroring. <br><br> - Not supported on Iscsi or FC connected SAN.br><br> -  Slightly reduced performance. | 3 |

For more information to help plan for the number of physical disks and the desired resiliency type for a stand-alone server deployment, use the guidelines documented [here](https://docs.microsoft.com/windows-server/storage/storage-spaces/deploy-standalone-storage-spaces#prerequisites).


## Configure DPM Storage

Windows Storage Spaces allows you to pool multiple physical disks together into one logical drive. Storage Spaces use thin provisioning which reserves the drive capacity as we store data to the drive. It provides an easy way to create software-defined storage using a server's local storage resources.


### Configure Storage spaces
Follow these steps: :

1. Open **Server Manager**.
2. Click **File and Storage Services**.
3. Click **Storage Pools**.
4. Select **New Storage Pool** option from **TASKS**.
5. Enter a name for the storage pool, click **Next**.
6. Include the physical disk to the storage pool.
   If  a disk is missing from the primordial pool, you can add it by selecting **Add Physical Disk** option from the **TASKS** drop-down menu.

   ![Include Physical Disc](./media/add-storage/include-phyiscal-disk-2019.png)

   >[!NOTE]
   > The primordial pool is created by default and is essentially a repository for disks that are available for use in a storage pool that you create. A disk can only belong to a single storage pool.

7. Check the media type of the disk included. At least one of the disks should be SSD, required for SSD Tiering.
   - Add all the disks including SSDs to the storage pool.
   - Add only one disk to the pool to keep the column count to 1. You can then add disks as needed afterwards.

     > [!NOTE]
     > - If you add multiple disks to the storage pool at a go, the number of disks is stored as the number of columns. When more disks are added, they can only be a multiple of the number of columns.
     > - For DPM running on virtual machines, expose the VHDs carved out of physical SSDs & HDDs of required size from the host computer to the VM, and use them as a tiered storage as explained above.

   The following image shows the check for disk type:

   ![Check disk type ](./media/add-storage/media-type-check-2019.png)

8. If the media-type for HDD or SSD disk is not recognized correctly, use the following command:

    *Set-PhysicalDisk -UniqueId \<UniqueId String\> -MediaType <HDD|SSD>*

    ![Set media type ](./media/add-storage/set-media-type-2019.png)

9. For each of these disks, set the allocation as **Automatic**.
   ![Disk allocation](./media/add-storage/allocation-2019.png)

10. Check the options made, and click **Create to create a new storage pool**.

    ![Create a new storage pool](./media/add-storage/new-storage-pool-2019.png)

After successful creation of the storage pool, the newly created storage pool gets listed under  **STORAGE POOL** . **PHYSICAL DISK** displays the disks that are present in the selected pool.

### Disable Write-Back Cache

Disable Write-Back Cache to disable auto caching at storage pool level (needed only for tiered storage).

To do this, go to PowerShell and execute the following commands:

```
Set-StoragePool -FriendlyName <String> [-WriteCacheSizeDefault <UInt64>]
 ```
Choose -WriteCacheSizeDefault value as 0.

 ![Storage pool friendly name](./media/add-storage/ps-command-2019.png)
::: moniker-end

### Create virtual disks
Follow these steps:

1. In the **VIRTUAL DISK** pane, select **New Virtual Disk** from **TASKS** drop-down menu.

    ![Virtual Disk](./media/add-storage/virtual-disk-2019.png)

2. Choose the storage pool from which you want to create a virtual disk.

    ![Choose Storage Pool](./media/add-storage/choose-storage-pool-2019.png)

3. Provide a name for the virtual disk.

4. Select **Create storage tiers on this virtual disk** to create a tiered storage.   

    > [!NOTE]
    > Tiered Storage is possible only when the storage pool contains a mixture of SSD and HDD.

    ![Create tier storage](./media/add-storage/tier-create-2019.png)
5. Click **Next** and select **Enable enclosure awareness (if required)**.

    ![Enable Enclosure Awareness](./media/add-storage/enclosure-awareness-2019.png)

6. Select **Simple Layout** and click **Next**.

7. **Fixed Provisioning** is the default selection.  Click **Next**.
8. Provide the size for **Faster Tier** and **Standard Tier**.  **Faster Tier** corresponds to SSD and  **Standard Tier** corresponds to HDD. The size of the Faster Tier should be 4% the size of Standard Tier (For E.g. If the total requirement is 100 GB – if HDD is 96 GB, SDD should be 4 GB. Click **Next**.

    ![Tier](./media/add-storage/tier-size-2019.png)

9. Confirm the configurations and click **Create**.

    ![Create tiered storage](./media/add-storage/tier-size-2019.png)

### Create a volume

Follow these steps:
1. Select the virtual disk that you created and launch the **New Volume Wizard**.

    ![New Volume Wizard](./media/add-storage/new-volume-wizard-2019.png)

3. In the **New Volume Wizard**, click **Next**, assign drive letter, and specify the size.

    ![Assign Drive Letter](./media/add-storage/drive-letter-2019.png)

4. Click **Finish** to create a new volume.
5. Format the volume that you created, from **Disk Management** console to ReFS.

### Disable Auto-Caching at file system level

1.  Go to PowerShell.
2.  Use the following command:
    ```
    fsutil behavior disableWriteAutoTiering
    ```

    Usage:  fsutil behavior set disableWriteAutoTiering \<volume pathname\> <1|0>)
    Values:

        0 - Enable write auto tiering on the given volume (default)

        1 - Disable write auto tiering on the given volume

    Example:   fsutil behavior set disableWriteAutoTiering C: 1

    ![fsutil behavior](./media/add-storage/fsutil-behavior-2019.png)

Note that you can skip this step if more than 10% of SSD is available. This can be disabled later if there is a performance degradation in terms of backup speeds.

Now, add the newly created volumes to DPM storage using the procedure detailed below.

## Add volumes to DPM storage

Follow these steps:

1. In the DPM Management console > **Disk Storage**, click **Rescan**.
2. In **Add Disk Storage**, click **Add**.
3. After the volumes are added, you can give them a friendly name.
4. Click **OK** to format the volumes to ReFS, so DPM can use them as MBS.

    ![Review Disk Storage Allocation](./media/add-storage/dpm2016-add-storage-7.png)


## Migrate data to newly created volumes

In case you had upgraded your existing storage to a tiered storage, you can migrate your data by using Volume Migration. You can use PowerShell or the user interface to migrate data sources. [Learn more](volume-to-volume-migration.md).


Migration of data source should have all recovery points on Modern Storage.

> [!NOTE]
> - Migration of  data sources with backups on disks and volumes (for example, DPM server upgrades when the disk backups haven't expired) is not supported.
>- Migration is similar to modification of a protection group. While migration is in progress, you cannot trigger an ad hoc job. Scheduled jobs continue as configured. When the migration completes, current jobs in the protection group are preempted.



## Configure workload-aware storage

Using workload-aware storage, the volumes can be selected to preferentially store specific workloads. For example, expensive volumes that support high IOPS can be configured to store workloads that need frequent, high-volume backups such as SQL Server with transaction logs. Workloads that are backed up less frequently, such as VMs, can be backed up to low-cost volumes.

You can configure workload-aware storage using Windows PowerShell cmdlets.

### Update the volume properties

1. Run the **Update-DPMDiskStorage** to update the properties of a volume in the storage pool on a DPM server. The syntax is **Parameter Set: Volume**.
2. Run the cmdlet with these parameters.

    ```
    Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
    ```

    ![Review Disk Storage Allocation](./media/add-storage/dpm2016-add-storage-8.png)

    Changes made using the PowerShell cmdlet are reflected in the DPM Management console.

    ![Review Disk Storage Allocation](./media/add-storage/dpm2016-add-storage-9.png)

## Volume Exclusion

DPM servers may be managed by a team of Administrators. While there are guidelines on storage that should be used for backups, a wrong volume given to DPM as backup storage may lead to loss of critical data. Hence, with DPM 2016 UR4 and later, you can prevent such scenarios by configuring those volumes to not be shown as *available* for storage using PowerShell.

For Example, to exclude F:\ and C:\MountPoint1, use these steps:

1. Run the Set0DPMGlobalPropery commandlet:

    ```
    Set-DPMGlobalProperty -DPMStorageVolumeExclusion "F:,C:\MountPoint1"   
    ```
2. Rescan the storage through UI, or use Start-DPMDiskRescan cmdlet.

    The configured volumes and mountpoints are excluded.
3. To remove volume exclusion, run the following cmdlet:
    ```
    Set-DPMGlobalProperty -DPMStorageVolumeExclusion ""   
    ```
After removing volume exclusion, rescan the storage. All volumes and mount points, except System Volumes, are available for DPM storage.

## Custom Size Allocation

DPM 2019 consumes storage thinly, as needed. Once DPM is configured for protection, it calculates the size of the data being backed up. If many files and folders are being backed up together, as in the case of a file server, size calculation can take long time.

With DPM 2016 and later, you can configure DPM to accept the volume size as default instead of calculating the size of each file. The corresponding registry key is *HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\Configuration\DiskStorage* with the Key, *EnableCustomAllocationOnReFSStorage* as a string set to 1 to enable custom size allocation, set to 0 for default size allocation with DPM.
