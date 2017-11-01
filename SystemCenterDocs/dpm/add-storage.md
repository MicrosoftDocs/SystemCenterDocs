---
description: Learn about the new features when you upgrade to DPM 2016. This article also provides an overview of how to upgrade your DPM installation.
manager:  carmonm
ms.topic:  article
author:  markgalioto
ms.author: markgal
ms.prod:  system-center-threshold
keywords:
ms.date:  11/01/2017
title:  Upgrade to DPM 2016
ms.technology:  system-center-2016
ms.assetid:  faebe568-d991-401e-a8ff-5834212f76ce
---

# Add storage to DPM 2016

>Applies To: System Center 2016

Modern Backup Storage (MBS) is provided by System Center Data Protection Manager (DPM) to deliver 50% storage savings, 3X faster backups, and more efficient, workload-aware storage. 

- MBS is enabled automatically when you're running at least DPM 2016 on Windows Server 2016. If DPM is running on a version of Windows Server older than Windows Server 2016, it doesn't use MBS.
- MBS provides intelligent storage for short-term backup to disk.  MBS provides faster disk backup, consuming less disk space. Without MBS, each datasource needs two volumes, one for the the initial backup and the other for delta changes.
- MBS backups are stored on an ReFS disk. It uses ReFS block cloning, and VHDX technology, [Learn more](https://blogs.technet.microsoft.com/dpm/2016/10/19/introducing-dpm-2016-modern-backup-storage/). 


## Setting up MBS

Setting up MBS consists of the following steps:

1. Make sure you're running DPM 2016 or later on a VM running Windows Server 2016 or later.
2. Create a volume on a virtual disk in a storage pool. To do this:
    a. Add a disk to the storage pool
    b. Create a virtual disk from the storage pool, with layout set to Simple. You can then add additional disks, or extend the virtual disk.
    c. Create volumes on the virtual disk
3. Add the volumes to DPM.
4. Configure workload-aware storage.


    

## Create a volume

1. Create a storage pool in the File and Storage Services of Server Manager.
2. Add the available physical disks to the storage pool.
    - Adding only one disk to the pool keeps the column count to 1. You can then add disks as needed afterwards.
    - If multiple disks are added to the pool, the number of disks will be stored as the number of columns. This means that when more disks are added, they can only be a multiple of the number of columns.
    
    ![Add disks to storage pool](./media/add-storage/dpm2016-add-storage-1.png)

3. Create a virtual disk from the storage pool, with the layout set to Simple.

    ![Create virtual disk](./media/add-storage/dpm2016-add-storage-2.png)
     
4. Now add as many physical disks as needed.
    
    ![Add additional disks](./media/add-storage/dpm2016-add-storage-3.png)

5. Extend the virtual disk with the Simple layout, to reflect any physical disks you added.

    ![Extend virtual disks](./media/add-storage/dpm2016-add-storage-4.png)

6. Now, create volumes on the virtual disk.

    ![Create volume](./media/add-storage/dpm2016-add-storage-5.png)
    ![Select volume server and sisk](./media/add-storage/dpm2016-add-storage-6.png)


## Add volumes to DPM storage


1. In the DPM Management console > **Disk Storage**, click **Rescan**.
2. In **Add Disk Storage**, click **Add**. 
3. After the volumes are added, you can give them a friendly name.
4. Click **OK** to format the volumes to ReFS, so that DPM can use them as MBS.


![Review Disk Storage Allocation](./media/add-storage/dpm2016-add-storage-7.png)

## Configure workload-aware storage

Using workload-aware storage, the volumes can be selected to preferentially store specific workloads. For example, expensive volumes that support high IOPS can be configured to store workloads that need frequent, high-volume backups such as SQL Server with transaction logs.  Workloads that are backed up less frequently,for example VMs, can be backed up to low-cost volumes.

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
