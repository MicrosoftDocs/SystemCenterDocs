---
title: Get VM Data Disk
description: The Get VM Data Disk activity retrieves the specified data disk from a virtual machine.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 55184e52-7605-48e9-81b3-0ad20e06a28e
author: jyothisuri
ms.author: jsuri
monikerRange: '<=sc-orch-2019'
---

# Get VM Data Disk

The **Get VM Data Disk** activity retrieves the specified data disk from a virtual machine. It's part of the **Azure Virtual Machine Disks** category activity.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Get VM Data Disk Required Properties

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| VM Service Name   | The cloud service the data disk is attached to.   | String   |
| VM Deployment Name  | The deployment the data disk is attached to.   | String   |
| VM Instance Name   | The virtual machine to which the data disk is attached. | String   |
| Logical Unit Number | The Logical Unit Number (LUN) of the disk.   | 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15 |

## Get VM Data Disk Optional Properties

There are no optional properties for this runbook activity.

## Get VM Data Disk Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| VM Service Name   | The cloud service the data disk is attached to.   | String   |
| VM Deployment Name  | The deployment the data disk is attached to.   | String   |
| VM Instance Name   | The virtual machine to which the data disk is attached.   | String   |
| Logical Unit Number | The Logical Unit Number (LUN) of the disk.   | Integer   |
| Host Caching   | Specifies the platform caching behavior of data disk blob for read/write efficiency.   | String   |
| Disk Name   | Specifies the name of the disk.   | String   |
| Disk Label   | Specifies the description of the data disk.   | String   |
| Media Link   | Specifies the location of the blob in Windows Azure blob store where the media for the disk is located. | String   |
| Disk Size in GB   | Specifies the size, in GB, of an empty disk to be attached to the role.   | Integer   |
