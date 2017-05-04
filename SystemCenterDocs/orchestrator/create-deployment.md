---
title: Create Deployment
description: The Create Deployment activity uploads a new service package and creates a new deployment on staging or production.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: c0fc7ec4-32ab-4f96-a9cf-3a696cc512ad
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Create Deployment

Applies To: System Center 2016 - Orchestrator

The **Create Deployment** activity uploads a new service package and creates a new deployment on staging or production. It is part of the **Azure Deployments** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Create Deployment Required Properties

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Service DNS Prefix   | The DNS prefix name of the Azure cloud service.   | String   |
| Deployment Slot   | The deployment slot for the deployment.   | Staging, Production |
| Deployment Name   | The name for the deployment. The deployment name must be unique among other deployments for the cloud service.   | String   |
| Label   | A friendly name for the cloud service.   | String   |
| Service Configuration File Path | The path to the service configuration file for the deployment.   | String   |
| Service Package URL   | A URL that refers to the location of the service package in the Blob service. The service package can be located either in a storage account beneath the same subscription or a Shared Access Signature (SAS) URI from any storage account. | String   |
| Start Deployment Immediately   | Indicates whether to start the deployment immediately after it is created.   | True, False   |
| Treat Warnings as Errors   | Indicates whether to treat package validation warnings as errors. If set to true, the Create Deployment activity fails if there are validation warnings on the service package.   | True, False   |
| Wait for Completion   | Whether to wait for this operation to complete in Azure before moving on to the next activity.   | True, False   |

## Create Deployment Optional Properties

There are no optional properties for this runbook activity.

## Create Deployment Published Data

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
| Service Package URL   | A URL that refers to the location of the service package in the Blob service. The service package can be located either in a storage account beneath the same subscription or a Shared Access Signature (SAS) URI from any storage account. | String   |
| Start Deployment Immediately   | Indicates whether to start the deployment immediately after it is created.   | Boolean   |
| Treat Warnings as Errors   | Indicates whether to treat package validation warnings as errors. If set to true, the Create Deployment activity fails if there are validation warnings on the service package.   | Boolean   |
| Wait for Completion   | Whether to wait for this operation to complete in Azure before moving on to the next activity.   | Boolean   |

## See Also

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)
