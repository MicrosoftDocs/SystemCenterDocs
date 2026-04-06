---
title: Add VM Data Disk
description: The Add VM Data Disk activity adds a data disk to a virtual machine.
ms.custom: engagement-fy23, UpdateFrequency2
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 29ca91cb-1d7f-43b1-a967-23e7cdf2918c
author: Jeronika-MS
ms.author: v-gajeronika
monikerRange: '<=sc-orch-2019'
ms.update-cycle: 1095-days
---

# Add VM Data Disk

The **Add VM Data Disk** activity adds a data disk to a virtual machine. It's part of the **Azure Virtual Machine Disks** category activity.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Add VM Data Disk Required Properties

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| VM Service Name   | The cloud service to add the data disk to.   | String   |
| VM Deployment Name   | The deployment to add the data disk to.   | String   |
| VM Instance Name   | The virtual machine to add the data disk to.   | String   |
| Select Data Disk Option | Specifies where the data disk to add to the virtual machine is located.   | DiskInBlobStorage, DiskInImageRepository, MountedDiskImageInBlobStorage |
| Host Caching   | Specifies the platform caching behavior of data disk blob for read/write efficiency.   | None, ReadOnly, ReadWrite   |
| Disk Name   | Specifies the name of the disk.   | String   |
| Disk Label   | Specifies the description of the data disk.   | String   |
| Source Media Link   | Specifies the location of a blob in account storage, which is mounted as a data disk when the virtual machine is created. | String   |
| Media Link   | Specifies the location of the blob in Microsoft Azure blob store where the media for the disk is located.   | String   |
| Disk Size in GB   | Specifies the size, in GB, of an empty disk to be attached to the virtual machine.   | Integer   |
| Wait for Completion   | Whether to wait for this operation to complete in Microsoft Azure before moving on to the next activity.   | True, False   |

## Add VM Data Disk Optional Properties

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Logical Unit Number | Specifies the Logical Unit Number (LUN) for the disk. The LUN specifies the slot in which the data drive appears when mounted for usage by the virtual machine. | 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15 |

## Add VM Data Disk Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| VM Service Name   | The cloud service to add the data disk to.   | String   |
| VM Deployment Name  | The deployment to add the data disk to.   | String   |
| VM Instance Name   | The virtual machine to add the data disk to.   | String   |
| Logical Unit Number | Specifies the Logical Unit Number (LUN) for the disk. The LUN specifies the slot in which the data drive appears when mounted for usage by the virtual machine. | Integer   |
| Host Caching   | Specifies the platform caching behavior of data disk blob for read/write efficiency.   | String   |
| Disk Name   | Specifies the name of the disk.   | String   |
| Disk Label   | Specifies the description of the data disk.   | String   |
| Source Media Link   | Specifies the location of a blob in account storage, which is mounted as a data disk when the virtual machine is created.   | String   |
| Media Link   | Specifies the location of the blob in Microsoft Azure blob store where the media for the disk is located.   | String   |
| Disk Size in GB   | Specifies the size, in GB, of an empty disk to be attached to the virtual machine.   | Integer   |
| Wait for Completion | Whether to wait for this operation to complete in Microsoft Azure before moving on to the next activity.   | Boolean   |
| Request ID   | The unique identifier of the request to Microsoft Azure.   | String   |

## Next steps

[Using Runbooks in System Center - Orchestrator](design-and-build-runbooks.md)
