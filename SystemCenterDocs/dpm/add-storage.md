---
description: Learn about the new features when you upgrade to DPM 2016. This article also provides an overview of how to upgrade your DPM installation.
manager:  carmonm
ms.topic:  article
author:  markgalioto
ms.author: markgal
ms.prod:  system-center-threshold
keywords:
ms.date:  10/14/2016
title:  Upgrade to DPM 2016
ms.technology:  system-center-2016
ms.assetid:  faebe568-d991-401e-a8ff-5834212f76ce
---

# Add Storage to DPM 2016

>Applies To: System Center 2016

DPM 2016 comes with Modern Backup Storage which delivers 50% storage savings, 3x faster backups, and more efficient storage with Workload-Aware storage. Modern Backup Storage can be used by setting up DPM 2016 on Windows Server 2016.

If DPM 2016 runs on an older version of Windows Server, DPM 2016 will protect the workloads the legacy way. More information on preparing storage to back up the legacy way can be found here.

DPM 2016 accepts volumes for storage. Hence, once a volume is added, DPM will format it to ReFS to use the new features of Modern Backup Storage. To add a volume, and to expand it later if needed, here is the suggested workflow:

1.	Setup DPM 2016 on a VM
2.	Create a volume on a virtual Disk in a Storage Pool:

    a.	Add a disk to a Storage Pool and create a virtual disk with Simple Layout

    b.	Add any more disks, and extend the virtual disk

    c.	Create Volumes on the virtual disk

3.	Add these volumes to DPM
4.	Configure Workload-Aware Storage

## Create a volume for DPM Modern Backup Storage

DPM 2016 accepts volumes as disk storage.  This helps customers in maintaining full control over the storage.  While the volume can be coming from a single disk, for future extension purposes, we propose creating volume out of a disk crated out of storage spaces.  This will help in expanding volume needed for backup storage.  This section provides best practice for creating a volume with this configuration.

First step is to create a Virtual Disk.  Through the File and Storage Services section of the Server Manager, create a Storage Pool, and add the available disks to it. Create a Virtual Disk from that Storage Pool with Simple Layout.

Step 1: Add the disks to a Storage Pool and create a virtual disk with Simple Layout. Adding only one disk to the pool will keep the column count as 1. This will give the freedom to add as many disks as needed later. 
If multiple disks are added to the pool while creating it, the number of disks will be stored as the number of columns, and when more disks are added, they can only be a multiple of the number of columns.

![Review Disk Storage Allocation](./media/add-storage/dpm2016-add-storage-1.png)

Create a virtual disk out of this Storage Pool and select the layout to be Simple

![Review Disk Storage Allocation](./media/add-storage/dpm2016-add-storage-2.png)

Step 2: Now add as many disks as needed and extend the virtual disk, with Simple layout.

![Review Disk Storage Allocation](./media/add-storage/dpm2016-add-storage-3.png)

Extend the Virtual Disk to reflect the added disks.

![Review Disk Storage Allocation](./media/add-storage/dpm2016-add-storage-4.png)

Step 3: Create Volumes on the Storage Pool

After creating the Virtual Disk with sufficient storage, create volumes on the Virtual Disk.
![Review Disk Storage Allocation](./media/add-storage/dpm2016-add-storage-5.png)

![Review Disk Storage Allocation](./media/add-storage/dpm2016-add-storage-6.png)

## Adding volumes to DPM Disk Storage

To add a volume to DPM, in the Management pane, Rescan the Storage and Click on Add. This will give a list of all the volumes available to be added for DPM Storage. After they are added to the list of selected volumes, they can also be given a Friendly name for easy recall. Clicking on OK will format these volumes to ReFS to enable DPM to use the benefits of Modern Backup Storage.

![Review Disk Storage Allocation](./media/add-storage/dpm2016-add-storage-7.png)

## Configure Workload-Aware Storage

With Workload Aware Storage, the volumes can be selected to preferentially store certain kinds of workloads. For example, expensive volumes that support high IOPS can be configured to store only the workloads that require frequent, high-volume backups like SQL with Transaction Logs. Other workloads that are backed up less frequently, say VMs, can be backed up to other low-cost volumes.

This can be done through PowerShell commandlet, Update-DPMDiskStorage, which updates the properties of a volume in the storage pool on a DPM server.

**Update-DPMDiskStorage**

**Syntax**

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

![Review Disk Storage Allocation](./media/add-storage/dpm2016-add-storage-8.png)

The changes made through PowerShell are reflected in the UI.

![Review Disk Storage Allocation](./media/add-storage/dpm2016-add-storage-9.png)
