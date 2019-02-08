---
description: Learn about the new features when you upgrade to DPM 2016. This article also provides an overview of how to upgrade your DPM installation.
manager: carmonm
ms.topic: article
author: rayne-wiselman
ms.author: raynew
ms.prod: system-center
keywords:
ms.date: 07/19/2018
title: Add Modern Backup Storage to DPM
ms.technology: data-protection-manager
ms.assetid: faebe568-d991-401e-a8ff-5834212f76ce
---

# Add Modern Backup Storage to DPM

Modern Backup Storage (MBS) is provided by System Center Data Protection Manager (DPM) to deliver 50% storage savings, 3X faster backups, and more efficient, workload-aware storage.

- MBS is enabled automatically when you're running at least DPM 2016 on Windows Server 2016. If DPM is running on a version of Windows Server older than Windows Server 2016, it doesn't use MBS.
- MBS provides intelligent storage for short-term backup to disk.  MBS provides faster disk backup, consuming less disk space. Without MBS, each datasource needs two volumes, one for the initial backup and the other for delta changes.
- MBS backups are stored on an ReFS disk. It uses ReFS block cloning, and VHDX technology, [Learn more](https://blogs.technet.microsoft.com/dpm/2016/10/19/introducing-dpm-2016-modern-backup-storage/).

DPM 2016 accepts volumes for storage. Once you add a volume, DPM formats the volume to ReFS to use the new features of Modern Backup Storage. Volumes cannot reside on a dynamic disk. Use only a basic disk.

While you can directly give a volume to DPM, you may face issues in extending the volume if a need arises later.
To prepare DPM for future expansion, use the available disks to create a storage pool, then create volumes on the storage pool, and expose the volumes to DPM. These virtual volumes can then be extended when needed.

The remainder of this article provides the detail on how to add a volume and to expand it later.

## Setting up MBS

Setting up MBS consists of the following steps. Please note you cannot attach locally created VHD (VHDX) files, and use them as storage on a physical DPM server.

1. Make sure you're running DPM 2016 or later on a VM running Windows Server 2016 or later.
2. To create a volume on a virtual disk in a storage pool:<br/>
    - Add a disk to the storage pool<br/>
    - Create a virtual disk from the storage pool, with layout set to Simple. You can then add additional disks, or extend the virtual disk.<br/>
    - Create volumes on the virtual disk.<br/>
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

DPM servers may be managed by a team of Administrators. While there are guidelines on storage that should be used for backups, a wrong volume given to DPM as backup storage may lead to loss of critical data. Hence, with UR4, you can prevent such scenarios by configuring those volumes to not be shown as available for storage using PowerShell.

For Example, to exclude F:\ and C:\MountPoint1, here are the steps:

1. Run the Set0DPMGlobalPropery commandlet:

```
Set-DPMGlobalProperty -DPMStorageVolumeExclusion "F:,C:\MountPoint1"   
```
2. Rescan the storage through UI, or use Start-DPMDiskRescan cmdlet.

The configured volumes and mountpoints are excluded.
To remove volume exclusion, run the following cmdlet:
```
Set-DPMGlobalProperty -DPMStorageVolumeExclusion ""   
```
After removing volume exclusion, rescan the storage. All volumes and mount points, except System Volumes, are available for DPM storage.

## Backup Storage Migration

Once all your backups are on MBS, there may be a need to migrate certain datasources from one volume to another. For example, scenarios where you need to upgrade storage, or when a volume is getting full. You can use PowerShell or the user interface to migrate datasources. The details can be found [in this blog entry](https://go.microsoft.com/fwlink/?linkid=861519).

The migrating datasource should have all recovery points on Modern Storage. Migrating datasources with backups on disks and volumes (for example, DPM server upgrades when the disk backups haven't expired) is not supported.
Migration is similar to modification of a protection group. While migration is in progress, you cannot trigger an ad hoc job. The scheduled jobs continue as configured. When the migration completes, any running jobs in the protection group are pre-empted.

::: moniker range="sc-dpm-2019"
## Faster backups with Tiered storage using SSDs

DPM 2016 introduced Modern Backup Storage, improving storage utilization and performance. MBS uses ReFS as underlying file system. MBS is designed to make use of hybrid storage such as tiered storage.

To achieve the scale and performance claimed by MBS, we recommend using a small percentage (2% of overall storage) of flash storage (SSD) with DPM 2019 as a tiered volume in combination with DPM HDD storage.


> [!NOTE]
> Ensure the tiered storage volume is configured with state storage device (SSD).

Use the following procedure:
1.	**Volume migration**

    Migrate your current backups to a temporary volume using Volume Migration.
2.	**Setup Windows Storage Spaces**

    Storage Spaces allow you to pool multiple physical disks together into one logical drive. Storage Spaces use thin provisioning, which reserves the drive capacity as we store data to the drive. It provides an easy way to create software-defined storage using a server's local storage resources.

    **Steps to setup Storage Spaces**
    1.	Open **Server Manager**.
    2.	Click **File and Storage Services**.

        >[!NOTE]

        > The primordial pool is created by default and is essentially a repository for disks that are available for use in a storage pool that you create. A disk can only belong to a single storage pool.

        If a disk is missing from the primordial pool, you can add it by choosing the *Add Physical Disk* option from the **TASKS** drop-down menu. Add all disks including SSDs to the storage pool.

    3.	Click **Storage Pools**.
    4.	Select **New Storage Pool** from **TASKS**.
    5.	Enter a name for the storage pool, click **Next**.
    6.	Include the physical disk to the storage pool.
    7.	Check the media-type of the disk included. At least one of the disks should be SSD.
    8.	If the media-type for HDD or SSD disk is not recognized correctly, use the following command:
        *Set-PhysicalDisk -FriendlyName <DiskName> -MediaType <HDD|SSD>*
    9.	For each of these disks, set the allocation as **Automatic**.
    10.	Confirm the choices and click **Create** to create a new storage pool.

        After the storage pool is created, it  gets listed in the **STORAGE POOLS** pane. **PHYSICAL DISK** pane displays the disks that are present in the selected pool.

    **Steps to create virtual disk**
        1.	In the **VIRTUAL DISK** pane, select New Virtual Disk from **TASKS** drop-down menu.
        2.	Choose the storage pool from which you want to create a virtual disk.
        3.	Provide a name for the virtual disk.
        4.	Select **Create storage tiers** on this virtual disk to create a tiered storage.  

        >[!NOTE]
        > Tiered Storage is possible only when the storage pool contains a mixture of SSD and HDD).
        5.	Click **Next** and select **Enable enclosure awareness**.
        6.	Select **Simple Layout** and click **Next**.
        7.	Fixed Provisioning is the default selection. Click **Next**.
        8.	Provide the size for Faster Tier and Standard Tier. Here, Faster Tier corresponds to SSD & Standard Tier corresponds to HDD.

        The size of the Faster Tier should be 4% the size of Standard Tier (For E.g. If the total requirement is 100 GB – if HDD is 96 GB, SDD should be 4 GB). Click **Next**.
        9.	Confirm the configurations and click Create.
        Once you have created virtual disk, disable Write-Back Cache to disable auto caching (storage pool level)

    **Steps to set Write-Back Cache Size to 0**:
    1.	Go to PowerShell.
    2.	Execute the following commands:

        *Set-StoragePool
        -Name <String>
        [-WriteCacheSizeDefault <UInt64>]
        [-AutoWriteCacheSize <Boolean>]*

            *Choose -WriteCacheSizeDefault value as 0 and -AutoWriteCacheSize value as False*

    **Create a Volume form the virtual disk**:
    1.	Select the virtual disk that you created and launch the **New Volume** Wizard.
    2.	In the **New Volume** wizard, click **Next**, assign drive letter, specify the size.
    3.	Click **Finish** to create a new volume.
    4.	Format the volume that you created, from **Disk Management** console to ReFS.

    **Disable Auto-Caching at file system level
        Steps to disable Auto-Caching**
    1.	Go to PowerShell.
    2.	Use the following command:

        *fsutil behavior disableWriteAutoTiering
        (Usage:  fsutil behavior set disableWriteAutoTiering <volume pathname> <1|0>)*

    	**Values**:

        0 - Enable write auto tiering on the given volume (default)

        1 - Disable write auto tiering on the given volume

               E.g.:   fsutil behavior set disableWriteAutoTiering C: 1

3.	Add  the newly created volumes to DPM storage using the [step mentioned here](https://docs.microsoft.com/system-center/dpm/add-storage?view=sc-dpm-1807#add-volumes-to-dpm-storage).
4.	Migrate your data back to the newly created volumes using Volume Migration performed in Step 1.

::: moniker-end

## Custom Size Allocation

DPM 2016 consumes storage thinly, as needed. Once DPM is configured for protection, it calculates the size of the data being backed up. If many files and folders are being backed up together, as in the case of a file server, size calculation can take long time. With DPM 2016, you can configure DPM to accept the volume size as default instead of calculating the size of each file. The corresponding registry key is "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\Configuration\DiskStorage" with the Key, "EnableCustomAllocationOnReFSStorage" as a String set to 1 to enable custom size allocation, set to 0 for default size allocation with DPM.
