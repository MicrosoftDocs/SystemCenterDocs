---
title: Shutdown VM Instance
description: The Shutdown VM Instance activity shuts down the specified virtual machine.
ms.custom: na
ms.date: 05/08/2019
ms.prod: system-center
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: a60f46a3-7696-4857-8cd9-eecc2162c9ee
author: rayne-wiselman
ms.author: raynew
manager: carmonm
robots: noindex
---
# Shutdown VM Instance

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

The **Shutdown VM Instance** activity shuts down the specified virtual machine. It is part of the **Azure Virtual Machines** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Shutdown VM Instance Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| VM Service Name   | The name of the cloud service containing the virtual machine.   | String   |
| VM Deployment Name  | The name of the deployment containing the virtual machine.   | String   |
| VM Instance Name   | The name of the virtual machine.   | String   |
| Wait for Completion | Whether to wait for this operation to complete in Windows Azure before moving on to the next activity. | True, False   |

## Shutdown VM Instance Optional Properties

There are no optional properties for this runbook activity.

## Shutdown VM Instance Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| VM Service Name   | The name of the cloud service containing the virtual machine.   | String   |
| VM Deployment Name  | The name of the deployment containing the virtual machine.   | String   |
| VM Instance Name   | The name of the virtual machine.   | String   |
| Wait for Completion | Whether to wait for this operation to complete in Windows Azure before moving on to the next activity. | Boolean   |
| Request ID   | The unique identifier of the request to Windows Azure.   | String   |

## Other Resources

[Using Runbooks in System Center - Orchestrator](design-and-build-runbooks.md)
