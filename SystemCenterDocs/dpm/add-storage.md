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

DPM 2016 accepts volumes for storage. Hence, once a volume is added, DPM will format it to ReFS to use the new features of Modern Backup Storage. 

While you can directly give a volume to DPM, you may face issues in extending the volume if a need arises at a lter point of time. 
To take care of this, you can create a storage pool from the Disks available, create volumes on it and then expose them to DPM. These virtual volumes can then be extended as and when needed. 

Hence, to add a volume, and to expand it later if needed, here is the suggested workflow:

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

## Volume Exclusion

DPM servers may be managed by a team of Administrators. While there are guidelines on storage that should be used for backups, a wrong volume given to DPM as backup storage may lead to loss of critical data. Hence, with UR4, you can prevent such scenarios by configuring those volumes to not be shown as available for storage using PowerShell. 

For Example, to exclude F:\ and C:\MountPoint1, here are the steps: 

1. Run the Set0DPMGlobalPropery commandlet:

```
Set-DPMGlobalProperty -DPMStorageVolumeExclusion "F:,C:\MountPoint1"   
```
2. Rescan the storage through UI, or using Start-DPMDiskRescan commandlet.

The volumes and mountpoints thus configured will be excluded,
To remove volume exclusion, run the following: 
```
Set-DPMGlobalProperty -DPMStorageVolumeExclusion ""   
```
This, followed by a rescan will lead to all volumes and mount points to be available to be used as DPM storage (other than System Volumes)

## Backup Storage Migration

Once all your backups are on MBS, in scenarios as storage upgrade, or when a volume is getting full, there may be a need to migrate certain datasources from one volume to another. This can be achieved using PowerShell, or UI. The details can be found [here](https://go.microsoft.com/fwlink/?linkid=861519). 

Please note that the datasource being migrated should have all its recovery points on Modern Storage. Migration of datasources with backups on both disks and volumes (as in the case of DPM server upgrades when the disk backups havent expired) is not supported. 
Further, migration is like Modification of a PG. Hence, you cannot trigger an ad-hoc job while migration is in progress. The scheduled jobs will continue as configured. Further, at the time when migration completes, any running jobs in the PG will be pre-empted.

## Custom Size Allocation

DPM 2016 consumes storage thinly, as, and when needed. To do so DPM calculates the size of the data being backed up when its configured for protection. However, if a lot of files and folders are being backed up together, as in the case of a file server, size calculation can take long time. With DPM 2016, you can configure DPM to accept the volume size as default instead of calculating the size of each file, hence saving time. The corresponding registry key is "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\Configuration\DiskStorage" with the Key, "EnableCustomAllocation" as a DWORD set to 1 to enable custom size allocation, set to 0 for default size allocation with DPM.

