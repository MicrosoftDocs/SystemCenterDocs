---
title: Reimage VM Instance
description: The Reimage Role Instance activity requests a reimage of a role instance that is running in a deployment.
ms.custom: UpdateFrequency3
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 2ab3be4a-3f87-4f77-9a35-7d077a84cfd0
author: jyothisuri
ms.author: jsuri
robots: noindex
monikerRange: '<=sc-orch-2019'
ms.date: 11/01/2024
ms.update-cycle: 1095-days
---
# Reimage VM Instance

The **Reimage Role Instance** activity requests a reimage of a role instance that is running in a deployment. It's part of the **Azure Deployments** category activity.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Reimage Role Instance required properties

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Service DNS Prefix  | The DNS prefix name of the Windows Azure cloud service.   | String   |
| Deployment Slot   | The deployment slot for the deployment.   | Staging, Production |
| Instance Name   | The name of the role instance.   | String   |
| Wait for Completion | Whether to wait for this operation to complete in Windows Azure before moving on to the next activity. | True, False   |

## Reimage Role Instance optional properties

There are no optional properties for this runbook activity.

## Reimage Role Instance published data

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
| OS Family Number   | The operating system family that this deployment runs under.   | Integer   |
| OS Version String   | The version of the Windows Azure Guest operating system on which this deployment runs.   | String   |
| Private ID   | A unique identifier generated internally by Windows Azure for this deployment.   | String   |
| Raw XML Output   | The raw XML output returned by Windows Azure for this operation.   | String   |
| Request ID   | The unique identifier of the request to Windows Azure.   | String   |
| Upgrade Type   | The upgrade type designated for this deployment.   | String   |
| Status   | The status of the deployment.   | String   |
| Service DNS Prefix   | The DNS prefix name of the Windows Azure cloud service.   | String   |
| Deployment Slot   | The deployment slot of the deployment.   | String   |
| Deployment Name   | The name of the deployment.   | String   |
| Label   | A friendly name for the cloud service.   | String   |
| Instance Name   | The name of the role instance.   | String   |
| Wait for Completion   | Whether to wait for this operation to complete in Windows Azure before moving on to the next activity. | Boolean   |
