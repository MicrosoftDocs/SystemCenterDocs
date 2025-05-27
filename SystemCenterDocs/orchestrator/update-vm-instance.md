---
title: Update VM Instance
description: The Update VM Instance activity updates the specified virtual machine.
ms.custom: engagement-fy23, UpdateFrequency3
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f912974a-36a5-4bf5-a183-1923ba9bb5a9
author: jyothisuri
ms.author: jsuri
robots: noindex
monikerRange: '<=sc-orch-2019'
ms.date: 11/01/2024
---
# Update VM Instance

The **Update VM Instance** activity updates the specified virtual machine. It's part of the **Azure Virtual Machines** category activity.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Update VM Instance Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Service Name   | The name of the cloud service containing the virtual machine.   | String   |
| Deployment Name   | The name of the deployment containing the virtual machine.   | String   |
| VM Instance Name   | The name of the virtual machine.   | String   |
| XML Configuration File Path | The path to the configuration file to use to update the virtual machine.   | String   |
| Wait for Completion   | Whether to wait for this operation to complete in Microsoft Azure before moving on to the next activity. | True, False   |

## Update VM Instance Optional Properties

There are no optional properties for this activity.

## Update VM Instance Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Service Name   | The name of the cloud service containing the virtual machine.   | String   |
| Deployment Name   | The name of the deployment containing the virtual machine.   | String   |
| VM Instance Name   | The name of the virtual machine.   | String   |
| Wait for Completion | Whether to wait for this operation to complete in Microsoft Azure before moving on to the next activity. | Boolean   |
| Request ID   | The unique identifier of the request to Microsoft Azure.   | String   |

## Other Resources

[Using Runbooks in System Center - Orchestrator](design-and-build-runbooks.md)
