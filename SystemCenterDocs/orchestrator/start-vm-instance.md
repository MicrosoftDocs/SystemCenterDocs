---
title: Start VM Instance
description: The Start VM Instance activity starts the specified virtual machine.
ms.custom: engagement-fy23, UpdateFrequency3
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: c0e4ae5d-a015-460c-94f0-fd39c64b1e44
author: jyothisuri
ms.author: jsuri
robots: noindex
monikerRange: '<=sc-orch-2019'
ms.date: 11/01/2024
---
# Start VM Instance

The **Start VM Instance** activity starts the specified virtual machine. It's part of the **Azure Virtual Machines** category activity.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Start VM Instance Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| VM Service Name   | The name of the cloud service containing the virtual machine.   | String   |
| VM Deployment Name  | The name of the deployment containing the virtual machine.   | String   |
| VM Instance Name   | The name of the virtual machine.   | String   |
| Wait for Completion | Whether to wait for this operation to complete in Microsoft Azure before moving on to the next activity. | True, False   |

## Start VM Instance Optional Properties

There are no optional properties for this runbook activity.

## Start VM Instance Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| VM Service Name   | The name of the cloud service containing the virtual machine.   | String   |
| VM Deployment Name  | The name of the deployment containing the virtual machine.   | String   |
| VM Instance Name   | The name of the virtual machine.   | String   |
| Wait for Completion | Whether to wait for this operation to complete in Microsoft Azure before moving on to the next activity. | Boolean   |
| Request ID   | The unique identifier of the request to Microsoft Azure.   | String   |

## Other Resources

[Using Runbooks in System Center - Orchestrator](design-and-build-runbooks.md)
