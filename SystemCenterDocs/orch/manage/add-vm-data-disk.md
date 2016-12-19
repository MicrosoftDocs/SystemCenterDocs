---
title: Add VM Data Disk
description: The Add VM Data Disk activity adds a data disk to a virtual machine.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 29ca91cb-1d7f-43b1-a967-23e7cdf2918c
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
Add VM Data Disk
================

Applies To: System Center 2016 - Orchestrator

The **Add VM Data Disk** activity adds a data disk to a virtual machine. It is part of the **Azure Virtual Machine Disks** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

Add VM Data Disk Required Properties
------------------------------------

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| VM Service Name   | The cloud service to add the data disk to.   | String   |
| VM Deployment Name   | The deployment to add the data disk to.   | String   |
| VM Instance Name   | The virtual machine to add the data disk to.   | String   |
| Select Data Disk Option | Specifies where the data disk to add to the virtual machine is located.   | DiskInBlobStorage, DiskInImageRepository, MountedDiskImageInBlobStorage |
| Host Caching   | Specifies the platform caching behavior of data disk blob for read/write efficiency.   | None, ReadOnly, ReadWrite   |
| Disk Name   | Specifies the name of the disk.   | String   |
| Disk Label   | Specifies the description of the data disk.   | String   |
| Source Media Link   | Specifies the location of a blob in account storage which is mounted as a data disk when the virtual machine is created. | String   |
| Media Link   | Specifies the location of the blob in Windows Azure blob store where the media for the disk is located.   | String   |
| Disk Size in GB   | Specifies the size, in GB, of an empty disk to be attached to the virtual machine.   | Integer   |
| Wait for Completion   | Whether to wait for this operation to complete in Windows Azure before moving on to the next activity.   | True, False   |

Add VM Data Disk Optional Properties
------------------------------------

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Logical Unit Number | Specifies the Logical Unit Number (LUN) for the disk. The LUN specifies the slot in which the data drive appears when mounted for usage by the virtual machine. | 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15 |

Add VM Data Disk Published Data
-------------------------------

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| VM Service Name   | The cloud service to add the data disk to.   | String   |
| VM Deployment Name  | The deployment to add the data disk to.   | String   |
| VM Instance Name   | The virtual machine to add the data disk to.   | String   |
| Logical Unit Number | Specifies the Logical Unit Number (LUN) for the disk. The LUN specifies the slot in which the data drive appears when mounted for usage by the virtual machine. | Integer   |
| Host Caching   | Specifies the platform caching behavior of data disk blob for read/write efficiency.   | String   |
| Disk Name   | Specifies the name of the disk.   | String   |
| Disk Label   | Specifies the description of the data disk.   | String   |
| Source Media Link   | Specifies the location of a blob in account storage which is mounted as a data disk when the virtual machine is created.   | String   |
| Media Link   | Specifies the location of the blob in Windows Azure blob store where the media for the disk is located.   | String   |
| Disk Size in GB   | Specifies the size, in GB, of an empty disk to be attached to the virtual machine.   | Integer   |
| Wait for Completion | Whether to wait for this operation to complete in Windows Azure before moving on to the next activity.   | Boolean   |
| Request ID   | The unique identifier of the request to Windows Azure.   | String   |

See Also
--------

#### Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)

