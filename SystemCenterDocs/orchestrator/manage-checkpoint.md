---
title: Manage Checkpoint
description: The Manage Checkpoint activity is used to restore a virtual machine to the state when the checkpoint was created or to remove a checkpoint that is no longer needed.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: ab911e0f-d549-4e63-ba67-fe2641ca5136
author: jyothisuri
ms.author: jsuri
---
# Manage Checkpoint

The Manage Checkpoint activity is used to restore a virtual machine to the state when the checkpoint was created or to remove a checkpoint that is no longer needed.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Manage Checkpoint required properties

| Element | Description   | Valid Values |
|:---|:---|:---|
| ID   | The unique identifier (GUID) of the checkpoint inside the platform; for example, Hyper-V, VMware, or Virtual Server |   |
| Action  | Remove or Restore   |   |

## Manage Checkpoint published data

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Accessibility   | Public or Internal   |   |
| Action   | Remove or Restore   |   |
| Added Time   | The date and time that the checkpoint was added, in the format yyyy-mm-dd hh:mm:ss AM or PM   |   |
| Checkpoint ID   | The unique identifier (GUID) of the checkpoint   |   |
| Checkpoint Name   | The name of the checkpoint   |   |
| ID   | The unique identifier (GUID) of the checkpoint inside the platform; for example, Hyper-V, VMware, or Virtual Server |   |
| Description   | An alphanumeric description of the checkpoint   |   |
| Enabled   | True or False. If False, the virtual machine can't be started.   |   |
| Modified Time   | The modification date and time for the checkpoint, in the format yyyy-mm-dd hh:mm:ss AM or PM   |   |
| Most Recent Task   | The last recorded task for the checkpoint, for example, Start virtual machine   |   |
| Parent Checkpoint ID | The unique identifier (GUID) of the parent of the checkpoint   |   |
| Virtual Disk Drives  | The list of virtual disk drive names recorded for the checkpoint   |   |
| VM ID   | The unique identifier (GUID) of the virtual machine for which the checkpoint was created   |   |
| VM Name   | The name of the virtual machine for which the checkpoint was created   |   |
