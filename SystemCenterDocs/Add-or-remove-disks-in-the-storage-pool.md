---
title: Add or remove disks in the storage pool
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 27d6c6a8-d8d6-4931-88e0-a2bf0f87de97
---
# Add or remove disks in the storage pool
You can add and remove disks from the storage pool.

## Add disks to the pool
You can add more disks to the storage pool as follows:

1.  Delete any existing volumes on the disk before you add it to the storage pool. [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] can’t use space in any preexisting volumes located on disks that are added to the pool.

2.  [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] regularly rescans the disks and volumes in the storage pool to automatically detect and update the storage pool space. Note that:

    -   If you add a disk that contains a volume to the storage pool and later delete that volume, when [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] rescans the disk, it will add the new unallocated space to the available storage pool.

    -   If the name of a disk is listed as “Unknown” on the **Disks** tab in the DPM Administrator Console, you can’t add the disk to the storage pool until the disk name is corrected. To do this, in **Device Manager**, expand **Disk drives**. Right\-click each disk listed as "Disk drive", and select **Uninstall**. On the **Action** menu, click **Scan for hardware changes** to reinstall the disk.

## Remove disks from the pool
A storage pool disk is both physically attached to the [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] server and programmatically attached by [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] to the storage pool. To remove a disk from the storage pool do the following:

1.  Physically remove the disk. [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] sends an alert that there is a missing volume, and it’s displayed on the **Disks** tab in the **Management** task area

2.  In the missing volume alert **Details** pane, click the link to remove the disk from this storage pool. This removes the programmatic attachment.

Note that if you remove the disk from the storage pool and later bring the disk online again, [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] can’t access the existing data on it. If [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] labels a disk as "missing volume" and you do not remove the disk from the storage pool, when you bring the disk online again, [!INCLUDE[dpm2012short](../Token/dpm2012short_md.md)] will remap the volumes on the disk and can access the existing data on it.

