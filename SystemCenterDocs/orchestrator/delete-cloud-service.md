---
title: Delete Cloud Service
description: The Delete Cloud Service activity deletes the specified cloud service from Azure.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 54232d7c-117c-4eb5-839e-cdb8e2f4c2f2
author: jyothisuri
ms.author: jsuri
robots: noindex
monikerRange: '<=sc-orch-2019'
---
# Delete Cloud Service

The **Delete Cloud Service** activity deletes the specified cloud service from Azure. It's part of the **Azure Cloud Services** category activity.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Delete Cloud Service Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Service DNS Prefix | The DNS prefix name of the Azure cloud service. | String   |

## Delete Cloud Service Optional Properties

There are no optional properties for this runbook activity.

## Delete Cloud Service Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Service DNS Prefix | The DNS prefix name of the Azure cloud service. | String   |

## See Also

[Using Runbooks in System Center - Orchestrator](design-and-build-runbooks.md)
