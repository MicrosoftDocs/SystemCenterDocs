---
title: Get Checkpoint
description: The Get Checkpoint activity is used to retrieve a virtual machine checkpoint based on the filters you specify so that it can be used to restore the virtual machine to a previous state.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 047a8606-628d-4689-bfbc-336163cc52ba
author: Jeronika-MS
ms.author: v-gajeronika
---

# Get Checkpoint

The Get Checkpoint activity is used to retrieve a virtual machine checkpoint based on the filters you specify so that it can be used to restore the virtual machine to a previous state.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Get Checkpoint Filters

| Element   | Description   |
|:---|:---|
| Accessibility   | Public or Internal   |  
| Added Time   | The date and time that the checkpoint was added, in the format yyyy-mm-dd hh:mm:ss AM or PM   |  
| Checkpoint ID   | The unique identifier (GUID) of the checkpoint   |  
| Checkpoint Name   | The name of the checkpoint   |  
| ID   | The unique identifier (GUID) of the checkpoint inside the platform; for example, Hyper-V, VMware, or Virtual Server   |  
| Description   | An alphanumeric description of the checkpoint   |  
| Disk I/O (IOPS)   | The disk I/O performance, measured by the number of I/O operations per second (IOPS) that can be performed with acceptable latency |  
| Enabled   | True or False. If False, the virtual machine can't be started.   |  
| Modified Time   | The date and time that the checkpoint was modified in the format yyyy-mm-dd hh:mm:ss AM or PM   |  
| Most Recent   | True or False   |  
| Parent Checkpoint ID | The unique identifier (GUID) of the parent of the checkpoint   |  
| VM ID   | The unique identifier (GUID) of the virtual machine for which the checkpoint was created   |  

## Get Checkpoint Published Data

| Element   | Description   |
|:---|:---|
| Accessibility   | Public or Internal   |  
| Added Time   | The date and time that the checkpoint was added, in the format yyyy-mm-dd hh:mm:ss AM or PM   |  
| Checkpoint ID   | The unique identifier (GUID) of the checkpoint   |  
| Checkpoint Name   | The name of the checkpoint   |  
| ID   | The unique identifier (GUID) of the checkpoint inside the platform; for example, Hyper-V, VMware, or Virtual Server   |  
| Description   | An alphanumeric description of the checkpoint   |  
| Disk I/O (IOPS)   | The disk I/O performance, measured by the number of I/O operations per second (IOPS) that can be performed with acceptable latency |  
| Enabled   | True or False. If False, the virtual machine can't be started.   |  
| Modified Time   | The date and time that the checkpoint was modified in the format yyyy-mm-dd hh:mm:ss AM or PM   |  
| Most Recent   | True or False   |  
| Most Recent Task   | The last recorded task for the checkpoint, for example, Start virtual machine   |  
| Parent Checkpoint ID | The unique identifier (GUID) of the parent of the checkpoint   |  
| VM Name   | The name of the virtual machine for which the checkpoint was created   |  
| VM ID   | The unique identifier (GUID) of the virtual machine for which the checkpoint was created   |  
| Virtual Disk Drives  | The list of virtual disk drive names recorded for the checkpoint   |  
