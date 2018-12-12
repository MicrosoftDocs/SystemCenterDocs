---
title: Scale Tier Out activity in System Center - Orchestra
description: The Scale Tier Out activity is used in a runbook to add one virtual machine instance to a specified service tier.
ms.date: 01/22/2018
ms.prod: system-center
ms.technology: orchestrator
ms.topic: reference
author: rayne-wiselman
ms.author: raynew
manager: carmonm
---
# Scale Tier Out activity

The Scale Tier Out activity is used in a runbook to add one virtual machine instance to a specified service tier.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

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
