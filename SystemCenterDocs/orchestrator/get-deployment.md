---
title: Get Deployment
description: The Get Deployment activity returns configuration information, status, and system properties for a deployment.
ms.custom: engagement-fy23, UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 846005ef-f15b-42e1-a6f5-ead1324a788f
author: jyothisuri
ms.author: jsuri
monikerRange: '<=sc-orch-2019'
---

# Get Deployment

The **Get Deployment** activity returns configuration information, status, and system properties for a deployment. It's part of the **Azure Deployments** category activity.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Get Deployment Required Properties

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Service DNS Prefix | The DNS prefix name of the Microsoft Azure hosted. | String   |
| Deployment Slot   | The deployment slot of the deployment.   | Staging, Production |

## Get Deployment Optional Properties

There are no optional properties for this runbook activity.

## Get Deployment Published Data

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
| OS Version String   | The version of the Microsoft Azure Guest operating system on which this deployment runs. | String   |
| Private ID   | A unique identifier generated internally by Microsoft Azure for this deployment.   | String   |
| Raw XML Output   | The raw XML output returned by Microsoft Azure for this operation.   | String   |
| Upgrade Type   | The upgrade type designated for this deployment.   | String   |
| Status   | The status of the deployment.   | String   |
| Service DNS Prefix   | The DNS prefix name of the Microsoft Azure cloud service.   | String   |
| Deployment Slot   | The deployment slot of the deployment.   | String   |
| Deployment Name   | The name of the deployment.   | String   |
| Label   | A friendly name for the cloud service.   | String   |
