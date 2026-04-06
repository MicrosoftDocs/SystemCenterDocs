---
title: Create Cloud Service
description: The Create Cloud Service activity creates a new cloud service in Azure.
ms.custom: UpdateFrequency2
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 991105e1-71ad-43eb-b20e-1b31323a275f
author: Jeronika-MS
ms.author: v-gajeronika
monikerRange: '<=sc-orch-2019'
ms.update-cycle: 1095-days
---

# Create Cloud Service

The **Create Cloud Service** activity creates a new cloud service in Azure. It's part of **the Azure Cloud Services** category activity.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Create Cloud Service Required Properties

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Service DNS Prefix   | The DNS prefix name for the Azure cloud service.   | String   |
| Label   | A friendly name for the cloud service.   | String   |
| Description   | A description for the cloud service.   | String   |
| Location/Affinity Group   | Whether to create the cloud service in a certain location or affinity group.   | String   |
| Location/Affinity Group Value | The location where the cloud service will be created, or the name of an existing affinity group associated with the subscription. | String   |

## Create Cloud Service Optional Properties

There are no optional properties for this runbook activity.

## Create Cloud Service Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Service DNS Prefix   | The DNS prefix name for the Azure cloud service.   | String   |
| Label   | A friendly name for the cloud service.   | String   |
| Description   | A description for the cloud service.   | String   |
| Location/Affinity Group   | Whether to create the cloud service in a certain location or affinity group.   | String   |
| Location/Affinity Group Value | The location where the cloud service will be created, or the name of an existing affinity group associated with the subscription. | String   |

## Next steps

[Using Runbooks in System Center - Orchestrator](design-and-build-runbooks.md)
