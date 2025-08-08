---
title: Delete VM Data Disk
description: The Delete VM Data Disk activity removes the specified data disk from a virtual machine.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 16b29d57-c3d9-407d-949f-94dc8b4e4ef0
author: jyothisuri
ms.author: jsuri
monikerRange: '<=sc-orch-2019'
---
# Delete VM Data Disk

The **Delete VM Data Disk** activity removes the specified data disk from a virtual machine. It's part of the **Azure Virtual Machine Disks** category activity.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Delete VM Data Disk Required Properties

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| VM Service Name   | The cloud service to remove the data disk from.   | String   |
| VM Deployment Name  | The deployment to remove the data disk from.   | String   |
| VM Instance Name   | The virtual machine to remove the data disk from.   | String   |
| Logical Unit Number | The Logical Unit Number (LUN) of the disk.   | 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15 |
| Wait for Completion | Whether to wait for this operation to complete in Azure before moving on to the next activity. | True, False   |

## Delete VM Data Disk Optional Properties

There are no optional properties for this runbook activity.

## Delete VM Data Disk Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| VM Service Name   | The cloud service to remove the data disk from.   | String   |
| VM Deployment Name  | The deployment to remove the data disk from.   | String   |
| VM Instance Name   | The virtual machine to remove the data disk from.   | String   |
| Logical Unit Number | The Logical Unit Number (LUN) of the disk.   | Integer   |
| Wait for Completion | Whether to wait for this operation to complete in Azure before moving on to the next activity. | Boolean   |
| Request ID   | The unique identifier of the request to Azure.   | String   |

## See Also

[Using Runbooks in System Center - Orchestrator](design-and-build-runbooks.md)
