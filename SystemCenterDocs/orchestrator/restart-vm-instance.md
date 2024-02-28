---
title: Restart VM Instance
description: The Restart VM Instance activity restarts the specified virtual machine.
ms.custom: engagement-fy23, UpdateFrequency3
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b3e3176a-582d-4531-b882-441293114bc6
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
robots: noindex
monikerRange: '<=sc-orch-2019'
ms.date: 04/27/2023
---
# Restart VM Instance

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

The **Restart VM Instance** activity restarts the specified virtual machine. It's part of the **Azure Virtual Machines** category activity.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Restart VM Instance required properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| VM Service Name   | The name of the cloud service containing the virtual machine.   | String   |
| VM Deployment Name  | The name of the deployment containing the virtual machine.   | String   |
| VM Instance Name   | The name of the virtual machine.   | String   |
| Wait for Completion | Whether to wait for this operation to complete in Microsoft Azure before moving on to the next activity. | True, False   |

## Restart VM Instance optional properties

There are no optional properties for this runbook activity.

## Restart VM Instance published data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| VM Service Name   | The name of the cloud service containing the virtual machine.   | String   |
| VM Deployment Name  | The name of the deployment containing the virtual machine.   | String   |
| VM Instance Name   | The name of the virtual machine.   | String   |
| Wait for Completion | Whether to wait for this operation to complete in Microsoft Azure before moving on to the next activity. | True, False   |
| Request ID   | The unique identifier of the request to Microsoft Azure.   | String   |
