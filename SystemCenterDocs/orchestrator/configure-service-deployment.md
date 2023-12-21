---
title: Configure Service Deployment activity in System Center - Orchestrator
description: The Configure Service Deployment activity is used in a runbook to configure a VMM service for deployment. It also lists configure optional properties.
ms.date: 04/25/2023
ms.prod: system-center
ms.technology: orchestrator
ms.topic: article
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.custom: UpdateFrequency3, engagement-fy23
---
# Configure Service Deployment activity

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

The Configure Service Deployment activity is used in a runbook to configure a VMM service for deployment.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Configurer required properties

| **Element**   | **Description** | **Valid Values**   |
|:---|:---|:---|
| Service Configuration Name |   |   |
| Service Template Name   |   |   |
| Deployment Target   |   | Cloud<br>HostGroup |

## Configure optional properties

| **Element**   | **Description** | **Valid Values** |
|:---|:---|:---|
| Cloud Name   |   |   |
| Cost Center   |   |   |
| Description   |   |   |
| Host Group Name   |   |   |
| Service Priority   |   |   |
| Service Template Release |   |   |

## Configure published data

No published data is provided for this activity.
