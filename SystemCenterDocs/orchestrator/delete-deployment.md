---
title: Delete Deployment
description: The Delete Deployment activity deletes the specified deployment.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 40e827f1-2dfa-4a05-81c8-e23bfd8643ec
author: jyothisuri
ms.author: jsuri
robots: noindex
monikerRange: '<=sc-orch-2019'
---
# Delete Deployment

The **Delete Deployment** activity deletes the specified deployment. It's part of the **Azure Deployments** category activity.

>[!IMPORTANT]
>The delete deployment activity will delete all roles under the deployment. This includes the deletion of any virtual machines under the deployment.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Delete Deployment Required Properties

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Service DNS Prefix  | The DNS prefix name of the Azure cloud service.   | String   |
| Deployment Slot   | The deployment slot of the deployment.   | Staging, Production |
| Wait for Completion | Whether to wait for this operation to complete in Azure before moving on to the next activity. | True, False   |

## Delete Deployment Optional Properties

There are no optional properties for this runbook activity.

## Delete Deployment Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Request ID   | The unique identifier of the request to Azure.   | String   |
| Service DNS Prefix  | The DNS prefix name of the Azure cloud service.   | String   |
| Deployment Slot   | The deployment slot of the deployment.   | String   |
| Wait for Completion | Whether to wait for this operation to complete in Azure before moving on to the next activity. | Boolean   |

## See Also

[Using Runbooks in System Center - Orchestrator](design-and-build-runbooks.md)
