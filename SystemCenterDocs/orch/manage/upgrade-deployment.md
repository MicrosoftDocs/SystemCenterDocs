---
title: Upgrade Deployment
description: The Upgrade Deployment activity initiates an upgrade to a deployment.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b7260dc1-2314-4474-849b-7f6c627b5280
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Upgrade Deployment

Applies To: System Center 2016 - Orchestrator

The Upgrade Deployment activity initiates an upgrade to a deployment. It is part of the Azure Deployments category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Upgrade Deployment Required Properties

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Service DNS Prefix  | The DNS prefix name of the Windows Azure cloud service.   | String   |
| Deployment Slot   | The deployment slot for the deployment.   | Staging, Production |
| Upgrade Type   | The type of upgrade to initiate.   | Auto, Manual   |
| Label   | A friendly name for the cloud service.   | String   |
| Role To Upgrade   | The name of the specific role to upgrade.   | String   |
| Service Package URL | A URL that refers to the location of the service package in the Blob service. The service package can be located either in a storage account beneath the same subscription or a Shared Access Signature (SAS) URI from any storage account. | String   |
| Wait for Completion | Whether to wait for this operation to complete in Windows Azure before moving on to the next activity.   | True, False   |

## Upgrade Deployment Optional Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Configuration File Path | The path to the service configuration file for the deployment. | String   |

## Upgrade Deployment Published Data

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
| OS Version String   | The version of the Windows Azure Guest OS on which this deployment runs.   | String   |
| Private ID   | A unique identifier generated internally by Windows Azure for this deployment.   | String   |
| Raw XML Output   | The raw XML output returned by Windows Azure for this operation.   | String   |
| Request ID   | The unique identifier of the request to Windows Azure.   | String   |
| Upgrade Type   | The upgrade type designated for this deployment.   | String   |
| Status   | The status of the deployment.   | String   |
| Service DNS Prefix   | The DNS prefix name of the Windows Azure cloud service.   | String   |
| Deployment Slot   | The deployment slot of the deployment.   | String   |
| Deployment Name   | The name of the deployment.   | String   |
| Label   | A friendly name for the cloud service.   | String   |
| Configuration File Path   | The path to the service configuration file for the deployment.   | String   |
| Service Package URL   | A URL that refers to the location of the service package in the Blob service. The service package can be located either in a storage account beneath the same subscription or a Shared Access Signature (SAS) URI from any storage account. | String   |
| Role To Upgrade   | The name of the specific role to upgrade.   | String   |
| Wait for Completion   | Whether to wait for this operation to complete in Windows Azure before moving on to the next activity.   | Boolean   |

## See Also


#### Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)

