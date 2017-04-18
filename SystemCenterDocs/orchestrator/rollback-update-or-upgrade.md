---
title: Rollback Update or Upgrade
description: The Rollback Update or Upgrade activity cancels an in progress configuration change (update) or upgrade and returns the deployment to its state before the upgrade or configuration change was started.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a4c09c8f-5c17-4603-97fb-1d8b1e577ef7
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Rollback Update or Upgrade

Applies To: System Center 2016 - Orchestrator

The **Rollback Update or Upgrade** activity cancels an in progress configuration change (update) or upgrade and returns the deployment to its state before the upgrade or configuration change was started. It is part of the **Azure Deployments** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Rollback Update or Upgrade Required Properties

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Service DNS Prefix | The DNS prefix name of the Windows Azure cloud service.   | String   |
| Deployment Slot   | The deployment slot for the deployment.   | Staging, Production |
| Rollback Mode   | Specifies whether the rollback should proceed automatically.   | Auto, Manual   |
| Force Rollback   | Specifies whether the rollback should proceed even when it will cause local data to be lost from some role instances. | True, False   |

## Rollback Update or Upgrade Optional Properties

There are no optional properties for this runbook activity.

## Rollback Update or Upgrade Published Data

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
| OS Version String   | The version of the Windows Azure Guest OS on which this deployment runs.   | String   |
| Private ID   | A unique identifier generated internally by Windows Azure for this deployment.   | String   |
| Raw XML Output   | The raw XML output returned by Windows Azure for this operation.   | String   |
| Request ID   | The unique identifier of the request to Windows Azure.   | String   |
| Upgrade Type   | The upgrade type designated for this deployment.   | String   |
| Status   | The status of the deployment.   | String   |
| Service DNS Prefix   | The DNS prefix name of the Windows Azure cloud service.   | String   |
| Deployment Slot   | The deployment slot of the deployment.   | String   |
| Deployment Name   | The name of the deployment.   | String   |
| Rollback Mode   | Specifies whether the rollback should proceed automatically.   | String   |
| Force Rollback   | Specifies whether the rollback should proceed even when it will cause local data to be lost from some role instances. | Boolean   |
| Label   | A name for the cloud service that is base-64 encoded.   | String   |

## See Also


#### Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)

