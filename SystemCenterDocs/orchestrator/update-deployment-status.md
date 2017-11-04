---
title: Update Deployment Status
description: The Update Deployment Status activity initiates a change in deployment status.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: affe5f1b-7ae3-496c-89eb-35d8a74c8ea5
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Update Deployment Status

The Update Deployment Status activity initiates a change in deployment status. It is part of the Azure Deployments category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Update Deployment Status Required Properties

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Service DNS Prefix  | The DNS prefix name of the Windows Azure cloud service.   | String   |
| Deployment Slot   | The deployment slot for the deployment.   | Staging, Production |
| Deployment Status   | The new status for the deployment.   | Running, Suspended  |
| Wait for Completion | Whether to wait for this operation to complete in Windows Azure before moving on to the next activity. | True, False   |

## Update Deployment Status Optional Properties

There are no optional properties for this runbook activity.

## Update Deployment Status Published Data

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
| Wait for Completion   | Whether to wait for this operation to complete in Windows Azure before moving on to the next activity. | Boolean   |
| Deployment Status   | The new status of the deployment.   | String   |

## See Also


#### Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)

