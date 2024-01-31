---
title: Scale Tier Out activity in System Center - Orchestrator
description: The Scale Tier Out activity is used in a runbook to add one virtual machine instance to a specified service tier. It also lists the associated properties.
ms.date: 04/25/2023
ms.service: system-center
ms.subservice: orchestrator
ms.topic: article
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.custom: UpdateFrequency3, engagement-fy23
---
# Scale Tier Out activity

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

The Scale Tier Out activity is used in a runbook to add one virtual machine instance to a specified service tier.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Required properties

| **Element**  |  **Valid Values**   |
|:---|:---|
| Service Name |   |
| Tier Name   |  |  
| Start Action |  Default: Don't turn on the virtual machine |
| Stop Action  | Default: Save State   |

## Optional properties

| **Element**   | **Description**   |
|:---|:---|
| Virtual Machine Name | The name that VMM uses to identify the virtual machine. |   
| Computer Name   | The actual computer name of the virtual machine.   |   
| Description   |   |   

## Published data

This activity has no published data.
