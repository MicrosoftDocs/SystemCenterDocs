---
title: Reboot Role Instance
description: The Reboot Role Instance activity requests a reboot of a role instance that is running in a deployment.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 817a1bdc-c48e-4c9d-82a1-f864cc6293b6
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Reboot Role Instance

> Applies To: System Center 2016 - Orchestrator

The **Reboot Role Instance** activity requests a reboot of a role instance that is running in a deployment. It is part of the **Azure Deployments** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Reboot Role Instance required properties

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Service DNS Prefix  | The DNS prefix name of the Windows Azure cloud service.   | String   |
| Deployment Slot   | The deployment slot for the deployment.   | Staging, Production |
| Instance Name   | The name of the role instance.   | String   |
| Wait for Completion | Whether to wait for this operation to complete in Windows Azure before moving on to the next activity. | True, False   |

## Reboot Role Instance optional properties

There are no optional properties for this runbook activity.

## Reboot Role Instance published data

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
