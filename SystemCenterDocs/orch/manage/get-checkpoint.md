---
title: Get Checkpoint
description: The Get Checkpoint activity is used to retrieve a virtual machine checkpoint based on the filters you specify so that it can be used to restore the virtual machine to a previous state.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 047a8606-628d-4689-bfbc-336163cc52ba
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
Get Checkpoint
==============

Applies To: System Center 2016 - Orchestrator

The Get Checkpoint activity is used to retrieve a virtual machine checkpoint based on the filters you specify so that it can be used to restore the virtual machine to a previous state.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

Get Checkpoint Filters
----------------------

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Accessibility   | Public or Internal   |   |
| Added Time   | The date and time that the checkpoint was added, in the format yyyy-mm-dd hh:mm:ss AM or PM   |   |
| Checkpoint ID   | The unique identifier (GUID) of the checkpoint   |   |
| Checkpoint Name   | The name of the checkpoint   |   |
| ID   | The unique identifier (GUID) of the checkpoint inside the platform; for example, Hyper-V, VMWare, or Virtual Server   |   |
| Description   | An alphanumeric description of the checkpoint   |   |
| Disk I/O (IOPS)   | The disk I/O performance, measured by the number of I/O operations per second (IOPS) that can be performed with acceptable latency |   |
| Enabled   | True or False. If False, the virtual machine cannot be started.   |   |
| Modified Time   | The date and time that the checkpoint was modified in the format yyyy-mm-dd hh:mm:ss AM or PM   |   |
| Most Recent   | True or False   |   |
| Parent Checkpoint ID | The unique identifier (GUID) of the parent of the checkpoint   |   |
| VM ID   | The unique identifier (GUID) of the virtual machine for which the checkpoint was created   |   |

Get Checkpoint Published Data
-----------------------------

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Accessibility   | Public or Internal   |   |
| Added Time   | The date and time that the checkpoint was added, in the format yyyy-mm-dd hh:mm:ss AM or PM   |   |
| Checkpoint ID   | The unique identifier (GUID) of the checkpoint   |   |
| Checkpoint Name   | The name of the checkpoint   |   |
| ID   | The unique identifier (GUID) of the checkpoint inside the platform; for example, Hyper-V, VMWare, or Virtual Server   |   |
| Description   | An alphanumeric description of the checkpoint   |   |
| Disk I/O (IOPS)   | The disk I/O performance, measured by the number of I/O operations per second (IOPS) that can be performed with acceptable latency |   |
| Enabled   | True or False. If False, the virtual machine cannot be started.   |   |
| Modified Time   | The date and time that the checkpoint was modified in the format yyyy-mm-dd hh:mm:ss AM or PM   |   |
| Most Recent   | True or False   |   |
| Most Recent Task   | The last recorded task for the checkpoint, for example, Start virtual machine   |   |
| Parent Checkpoint ID | The unique identifier (GUID) of the parent of the checkpoint   |   |
| VM Name   | The name of the virtual machine for which the checkpoint was created   |   |
| VM ID   | The unique identifier (GUID) of the virtual machine for which the checkpoint was created   |   |
| Virtual Disk Drives  | The list of virtual disk drive names recorded for the checkpoint   |   |
