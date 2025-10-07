---
title: Change Deployment OS
description: The Change Deployment OS activity changes the underlying guest operating system of a deployment.
ms.custom: UpdateFrequency2
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 88be6019-d575-4212-b57e-a0fe71f19090
author: Jeronika-MS
ms.author: v-gajeronika
monikerRange: '<=sc-orch-2019'
---
# Change Deployment OS

The **Change Deployment OS** activity changes the underlying guest operating system of a deployment. It's part of the **Azure Deployments** category activity.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Change Deployment OS Required Properties

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Service DNS Prefix  | The DNS prefix name of the Azure cloud service.   | String   |
| Deployment Slot   | The deployment slot for the deployment.   | Staging, Production |
| Wait for Completion | Whether to wait for this operation to complete in Azure before moving on to the next activity. | True, False   |
| OS Family Number   | The operating system family.   | Integer   |
| OS Version String   | The operating system version.   | String   |

## Change Deployment OS Optional Properties

There are no optional properties for this runbook activity.

## Change Deployment OS Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| All Instances Ready   | Whether all instances of the deployment are ready.   | Boolean   |
| All Instances Stopped   | Whether all instances of the deployment are stopped.   | Boolean   |
| Configuration File XML   | The base-64 encoded configuration file of the deployment.   | String   |
| Current Upgrade Domain   | An integer value that identifies the current upgrade domain.   | Integer   |
| Current Upgrade Domain State | The state of the current upgrade domain.   | String   |
| Deployment URL   | The URL used to access the cloud service deployment.   | String   |
| Is Upgrading   | Whether the deployment is currently upgrading.   | Boolean   |
| Number of Upgrade Domains   | The number of upgrade domains in the deployment.   | Integer   |
| OS Family Number   | The OS family that this deployment runs under.   | Integer   |
| OS Version String   | The version of the Azure Guest OS on which this deployment runs.   | String   |
| Private ID   | A unique identifier generated internally by Azure for this deployment.   | String   |
| Raw XML Output   | The raw XML output returned by Azure for this operation.   | String   |
| Request ID   | The unique identifier of the request to Azure.   | String   |
| Upgrade Type   | The upgrade type designated for this deployment.   | String   |
| Status   | The status of the deployment.   | String   |
| Service DNS Prefix   | The DNS prefix name of the Azure cloud service.   | String   |
| Deployment Slot   | The deployment slot of the deployment.   | String   |
| Deployment Name   | The name of the deployment.   | String   |
| Label   | A friendly name for the cloud service.   | String   |
| Wait for Completion   | Whether to wait for this operation to complete in Azure before moving on to the next activity. | Boolean   |

## Next steps

[Using Runbooks in System Center - Orchestrator](design-and-build-runbooks.md)
