---
title: Walk Upgrade Domain
description: The Walk Upgrade Domain activity specifies the next upgrade domain to be walked during manual in-place upgrade or configuration change.
ms.custom: engagement-fy23, UpdateFrequency3
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: upgrade-and-migration-article
ms.assetid: 80432b66-bbce-4fbf-b26e-a4e457f76265
author: jyothisuri
ms.author: jsuri
robots: noindex
monikerRange: '<=sc-orch-2019'
ms.date: 11/01/2024
---
# Walk Upgrade Domain

The **Walk Upgrade Domain** activity specifies the next upgrade domain to be walked during manual in-place upgrade or configuration change. It's part of the **Azure Deployments** category activity.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Walk Upgrade Domain Required Properties

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Service DNS Prefix   | The DNS prefix name of the Microsoft Azure cloud service.   | String   |
| Deployment Slot   | The deployment slot for the deployment.   | Staging, Production |
| Domain ID to Upgrade | A value that identifies the upgrade domain to walk.   | Integer   |
| Wait for Completion  | Whether to wait for this operation to complete in Microsoft Azure before moving on to the next activity. | True, False   |

## Walk Upgrade Domain Optional Properties

There are no optional properties for this runbook activity.

## Walk Upgrade Domain Published Data

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
| OS Version String   | The version of the Microsoft Azure Guest OS on which this deployment runs.   | String   |
| Private ID   | A unique identifier generated internally by Microsoft Azure for this deployment.   | String   |
| Raw XML Output   | The raw XML output returned by Microsoft Azure for this operation.   | String   |
| Request ID   | The unique identifier of the request to Microsoft Azure.   | String   |
| Upgrade Type   | The upgrade type designated for this deployment.   | String   |
| Status   | The status of the deployment.   | String   |
| Service DNS Prefix   | The DNS prefix name of the Microsoft Azure cloud service.   | String   |
| Deployment Slot   | The deployment slot of the deployment.   | String   |
| Deployment Name   | The name of the deployment.   | String   |
| Label   | A friendly name for the cloud service.   | String   |
| Domain ID to Upgrade   | A value that identifies the upgrade domain to walk.   | Integer   |
| Wait for Completion   | Whether to wait for this operation to complete in Microsoft Azure before moving on to the next activity. | True, False   |

## Other Resources

[Using Runbooks in System Center - Orchestrator](design-and-build-runbooks.md)
