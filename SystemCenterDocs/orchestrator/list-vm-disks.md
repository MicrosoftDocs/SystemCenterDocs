---
title: List VM Disks
description: The List VM Disks activity retrieves a list of the disks in your image repository.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 43d6d155-7f84-45eb-aa36-9a7ed4a3b95a
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# List VM Disks

The **List VM Disks** activity retrieves a list of the disks in your image repository. It is part of the **Azure Virtual Machine Disks** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## List VM Disks required properties

There are no required properties for this runbook activity.

## List VM Disks optional properties

There are no optional properties for this runbook activity.

## List VM Disks published data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Affinty Group   | The affinity group in which the disk is located. The AffinityGroup value is derived from storage account that contains the blob in which the media is located. | String   |
| Attached To Deployment   | The deployment in which the disk is being used.   | String   |
| Attached To Cloud service | The cloud service in which the disk is being used.   | String   |
| Attached To VM Instance   | The virtual machine that the disk is attached to.   | String   |
| Disk Has OS?   | Specifies whether the disk contains an operation system.   | Boolean   |
| Disk Size in GB   | The size, in GB, of the disk.   | Integer   |
| Is Corrupted   | Returns whether there is a consistency failure detected with this disk.   | Boolean   |
| Label   | Specifies the description of the disk.   | String   |
| Location   | The geo-location in which the disk is located. The Location value is derived from storage account that contains the blob in which the disk is located.   | String   |
| Media Link   | Specifies the location of the blob in Windows Azure blob store where the media for the disk is located.   | String   |
| Name   | The name of the disk.   | String   |
| OS Type   | The operating system type of the disk.   | String   |
| Raw XML Body   | The raw XML output returned by Windows Azure for this operation.   | String   |
| Source Image Name   | The name of the OS Image from which the disk was created.   | String   |
