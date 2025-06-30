---
title: Delete VM Instance
description: The Delete VM Instance activity deletes the specified virtual machine.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 40a56eae-4b1f-4110-a0a7-a1449e8bba6a
author: jyothisuri
ms.author: jsuri
robots: noindex
monikerRange: '<=sc-orch-2019'
---

# Delete VM Instance

The **Delete VM Instance** activity deletes the specified virtual machine. It's part of the **Azure Virtual Machines** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Delete VM Instance Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| VM Service Name   | The name of the cloud service containing the virtual machine.   | String   |
| VM Deployment Name  | The name of the deployment containing the virtual machine.   | String   |
| VM Instance Name   | The name of the virtual machine.   | String   |
| Wait for Completion | Whether to wait for this operation to complete in Azure before moving on to the next activity. | True, False   |

## Delete VM Instance Optional Properties

There are no optional properties for this runbook activity.

## Delete VM Instance Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| VM Service Name   | The name of the cloud service containing the virtual machine.   | String   |
| VM Deployment Name  | The name of the deployment containing the virtual machine.   | String   |
| VM Instance Name   | The name of the virtual machine.   | String   |
| Wait for Completion | Whether to wait for this operation to complete in Azure before moving on to the next activity. | Boolean   |
| Request ID   | The unique identifier of the request to Azure.   | String   |

## See Also

[Using Runbooks in System Center - Orchestrator](design-and-build-runbooks.md)
