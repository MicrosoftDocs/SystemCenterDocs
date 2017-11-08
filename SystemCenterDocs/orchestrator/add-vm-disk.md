---
title: Add VM Disk
description: The Add VM Disk activity adds a disk to the user image repository.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: c191f3ce-e580-41cd-8ae6-ef853ebf2b5c
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Add VM Disk

The **Add VM Disk** activity adds a disk to the user image repository. It is part of the **Azure Virtual Machine Disks** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Add VM Disk Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Disk has OS?   | Specifies whether the disk contains an operation system.   | True, False   |
| Label   | Specifies the description of the disk.   | String   |
| Media Link   | Specifies the location of the blob in the Azure blob store where the media for the disk is located. | String   |
| Name   | Specifies a name for the disk.   | String   |
| OS Type   | The operating system type for the disk.   | Windows, Linux   |
| Wait for Completion | Whether to wait for this operation to complete in Azure before moving on to the next activity.  | True, False   |

## Add VM Disk Optional Properties

There are no optional properties for this runbook activity.

## Add VM Disk Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Disk has OS?   | Specifies whether the disk contains an operation system.   | Boolean   |
| Label   | Specifies the description of the disk.   | String   |
| Media Link   | Specifies the location of the blob in the Azure blob store where the media for the disk is located. | String   |
| Name   | Specifies a name for the disk.   | String   |
| OS Type   | The operating system type for the disk.   | String   |
| Wait for Completion | Whether to wait for this operation to complete in Azure before moving on to the next activity.  | Boolean   |
| Request ID   | The unique identifier of the request to Azure.   | String   |

## See Also

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)
