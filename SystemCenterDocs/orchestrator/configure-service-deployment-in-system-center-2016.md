---
title: Configure Service Deployment in System Center 2016
description: The Configure Service Deployment activity is used in a runbook to configure a VMM service for deployment.
ms.custom: UpdateFrequency2
ms.date: 12/02/2016
ms.prod: system-center
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 36c001be-fb36-4bc1-a590-e23c2a8b42e6
author: jyothisuri
ms.author: jsuri
manager: mkluck
robots: noindex
---
# Configure Service Deployment in System Center 2016

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

The Configure Service Deployment activity is used in a runbook to configure a VMM service for deployment.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Configure Service Deployment Required Properties

| **Element**   | **Description** | **Valid Values**   |
|:---|:---|:---|
| Service Configuration Name |   |   |
| Service Template Name   |   |   |
| Deployment Target   |   | Cloud<br>HostGroup |

## Configure Service Deployment Optional Properties

| **Element**   | **Description** | **Valid Values** |
|:---|:---|:---|
| Cloud Name   |   |   |
| Cost Center   |   |   |
| Description   |   |   |
| Host Group Name   |   |   |
| Service Priority   |   |   |
| Service Template Release |   |   |

## Configure Service Deployment Published Data

No published data is provided for this activity.

## Next steps

[Design and build runbooks in System Center 2016 Orchestrator](design-and-build-runbooks.md)
