---
title: Swap Deployment
description: The Swap Deployment activity initiates a virtual IP swap between the staging and production deployment environments for a service.
ms.custom: engagement-fy23, UpdateFrequency3
ms.date: 01/30/2023
ms.prod: system-center
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: addb97e7-9815-4690-861e-3a2f6153f4d4
author: jyothisuri
ms.author: jsuri
manager: mkluck
robots: noindex
---
# Swap Deployment

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

The **Swap Deployment** activity initiates a virtual IP swap between the staging and production deployment environments for a service. It's part of the **Azure Deployments** category activity.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Swap Deployment Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Service DNS Prefix  | The DNS prefix name of the Microsoft Azure cloud service.   | String   |
| Wait for Completion | Whether to wait for this operation to complete in Microsoft Azure before moving on to the next activity. | True, False   |

## Swap Deployment Optional Properties

There are no optional properties for this runbook activity.

## Swap Deployment Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Request ID   | The unique identifier of the request to Microsoft Azure.   | String   |
| Service DNS Prefix  | The DNS prefix name of the Microsoft Azure cloud service.   | String   |
| Wait for Completion | Whether to wait for this operation to complete in Microsoft Azure before moving on to the next activity. | Boolean   |

## Other Resources

[Using Runbooks in System Center - Orchestrator](design-and-build-runbooks.md)
