---
title: Add VM Disk
description: Describes the Add VM Disk activity, to add a disk to the user image repository.
ms.date: 11/01/2024
ms.service: system-center
ms.subservice: orchestrator
ms.topic: concept-article
author: Jeronika-MS
ms.author: v-gajeronika
ms.custom: UpdateFrequency2
monikerRange: '<=sc-orch-2019'
---

# Add VM Disk

The **Add VM Disk** activity adds a disk to the user image repository. It's part of the **Azure Virtual Machine Disks** category activity.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Add required properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Disk has OS?   | Specifies whether the disk contains an operation system.   | True, False   |
| Label   | Specifies the description of the disk.   | String   |
| Media Link   | Specifies the location of the blob in the Azure blob store where the media for the disk is located. | String   |
| Name   | Specifies a name for the disk.   | String   |
| OS Type   | The operating system type for the disk.   | Windows, Linux   |
| Wait for Completion | Whether to wait for this operation to complete in Azure before moving on to the next activity.  | True, False   |

## Add optional properties

There are no optional properties for this runbook activity.

## Add published data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Disk has OS?   | Specifies whether the disk contains an operation system.   | Boolean   |
| Label   | Specifies the description of the disk.   | String   |
| Media Link   | Specifies the location of the blob in the Azure blob store where the media for the disk is located. | String   |
| Name   | Specifies a name for the disk.   | String   |
| OS Type   | The operating system type for the disk.   | String   |
| Wait for Completion | Whether to wait for this operation to complete in Azure before moving on to the next activity.  | Boolean   |
| Request ID   | The unique identifier of the request to Azure.   | String   |
