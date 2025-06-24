---
title: Delete VM Disk
description: The Delete VM Disk activity deletes the specified data or operating system disk from your image repository.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 02ec5f7f-abad-4144-b78c-f32dfc7312af
author: jyothisuri
ms.author: jsuri
robots: noindex
monikerRange: '<=sc-orch-2019'
---
# Delete VM Disk

The **Delete VM Disk** activity deletes the specified data or operating system disk from your image repository. It is part of the **Azure Virtual Machine Disks** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Delete VM Disk Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Disk Name   | The name of the disk.   | String   |
| Wait for Completion | Whether to wait for this operation to complete in Azure before moving on to the next activity. | True, False   |

## Delete VM Disk Optional Properties

There are no optional properties for this runbook activity.

## Delete VM Disk Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Disk Name   | The name of the disk.   | String   |
| Wait for Completion | Whether to wait for this operation to complete in Azure before moving on to the next activity. | Boolean   |
| Request ID   | The unique identifier of the request to Azure.   | String   |

## See Also

[Using Runbooks in System Center - Orchestrator](design-and-build-runbooks.md)
