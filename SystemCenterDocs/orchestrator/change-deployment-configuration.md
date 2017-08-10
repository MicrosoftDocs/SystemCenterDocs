---
title: Change Deployment Configuration
description: The Change Deployment Configuration activity initiates a change to the deployment configuration.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: e4769f6f-dad7-4132-8d3c-917eee12d18a
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Change Deployment Configuration

Applies To: System Center 2016 - Orchestrator

The **Change Deployment Configuration** activity initiates a change to the deployment configuration. It is part of the Azure Deployments category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Change Deployment Configuration Required Properties

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Service DNS Prefix   | The DNS prefix name of the Azure cloud service.   | String   |
| Deployment Slot   | The deployment slot for the deployment.   | Staging, Production |
| Service Configuration File Path | The path to the service configuration file for the deployment.   | String   |
| Wait for Completion   | Whether to wait for this operation to complete in Azure before moving on to the next activity. | True, False   |

## Change Deployment Configuration Optional Properties

There are no optional properties for this runbook activity.

## Change Deployment Configuration Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| All Instances Ready   | Whether all instances of the deployment are ready.   | Boolean   |
| All Instances Stopped   | Whether all instances of the deployment are stopped.   | Boolean   |
| Configuration File XML   | The base-64 encoded configuration file of the deployment.   | String   |
| Current Upgrade Domain   | An integer value that identifies the current upgrade domain.   | Integer   |
| Current Upgrade Domain State   | The state of the current upgrade domain.   | String   |
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
| Service Configuration File Path | The path to the service configuration file for the deployment.   | String   |
| Wait for Completion   | Whether to wait for this operation to complete in Azure before moving on to the next activity. | Boolean   |

## See Also

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)
