---
title: Configure Service Deployment activity in System Center - Orchestrator
description: The Configure Service Deployment activity is used in a runbook to configure a VMM service for deployment. It also lists configure optional properties.
ms.date: 11/01/2024
ms.service: system-center
ms.subservice: orchestrator
ms.topic: article
author: jyothisuri
ms.author: jsuri
ms.custom: UpdateFrequency3, engagement-fy23
---
# Configure Service Deployment activity

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

## Next steps

[Design and build runbooks in System Center 2016 Orchestrator](design-and-build-runbooks.md)
