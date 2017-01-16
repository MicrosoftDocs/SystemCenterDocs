---
title: Scale Tier Out in System Center 2016
description: The Scale Tier Out activity is used in a runbook to add one virtual machine instance to a specified service tier.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8297cf61-e82a-49e9-8052-4aca023b46d2
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Scale Tier Out in System Center 2016

Applies To: System Center 2016 - Orchestrator

The Scale Tier Out activity is used in a runbook to add one virtual machine instance to a specified service tier.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Scale Tier Out Required Properties

| **Element**  |  **Valid Values**   |
|:---|:---|
| Service Name |   |
| Tier Name   | - |  
| Start Action |  Default: Don't turn on the virtual machine |
| Stop Action  | Default: Save State   |

## Scale Tier Out Optional Properties

| **Element**   | **Description**   |
|:---|:---|
| Virtual Machine Name | The name that VMM uses to identify the virtual machine. |   
| Computer Name   | The actual computer name of the virtual machine.   |   
| Description   |   |   

## Scale Tier Out Published Data

This activity has no published data.

## See Also


#### Other Resources

[Using Runbooks in System Center 2016 Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)
