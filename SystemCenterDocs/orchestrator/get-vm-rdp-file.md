---
title: Get VM RDP File
description: The Get VM RDP File activity retrieves the Remote Desktop Protocol configuration file from the specified virtual machine.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 7765b664-92ed-489c-ac4c-d75bed9527e7
author: jyothisuri
ms.author: jsuri
monikerRange: '<=sc-orch-2019'
---

# Get VM RDP File

The **Get VM RDP File** activity retrieves the Remote Desktop Protocol configuration file from the specified virtual machine. It's part of the **Azure Virtual Machines** category activity.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Get VM RDP File Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| VM Service Name   | The name of the cloud service containing the virtual machine. | String   |
| VM Deployment Name   | The name of the deployment containing the virtual machine.   | String   |
| VM Instance Name   | The name of the virtual machine.   | String   |
| Location to Save RDP File | The local path to which you want to save the RDP file.   | String   |
| RDP File Name   | The file name to use when saving the RDP file.   | String   |

## Get VM RDP File Optional Properties

There are no optional properties for this runbook activity.

## Get VM RDP File Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| VM Service Name   | The name of the cloud service containing the virtual machine. | String   |
| VM Deployment Name   | The name of the deployment containing the virtual machine.   | String   |
| VM Instance Name   | The name of the virtual machine.   | String   |
| Location to Save RDP File | The local path to which the RDP file was saved.   |   |
| RDP File Name   | The name of the RDP file for the virtual machine.   | String   |
