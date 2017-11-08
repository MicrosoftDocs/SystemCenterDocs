---
title: Create Checkpoint
description: The Create Checkpoint is used to save the state of a virtual hard disk that is attached to a virtual machine and all of the disk's contents, including application data files.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: df444439-f5e2-4132-8326-47be1f785b46
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Create Checkpoint

The Create Checkpoint is used to save the state of a virtual hard disk that is attached to a virtual machine and all of the disk's contents, including application data files. For virtual machines on Hyper-V and VMware ESX Server hosts, a checkpoint also saves the hardware configuration information.

You can create a checkpoint as a temporary backup before you update the operating system or an application, or before you make a configuration change on a virtual machine. The checkpoint allows you to restore the virtual machine to its previous state if the operation fails or adversely affects the virtual machine. You can create checkpoints only for a virtual machine that is deployed on a virtual machine host. You cannot create checkpoints for a virtual machine that is stored in the library. For a virtual machine that is running on a Hyper-V or VMware host, you can create a checkpoint without stopping the virtual machine. For a virtual machine that is running on a Virtual Server host, you must shut down the virtual machine before you create a checkpoint.

You can create multiple checkpoints for a single virtual machine. Be aware that checkpoints use hard disk space, and, when allowed to proliferate, can affect the performance of a virtual machine when it is running, during migration, and when storing it to the library. Therefore, it is a best practice to remove unnecessary checkpoints.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Create Checkpoint Required Properties

| Element | Description   | Valid Values |
|:---|:---|:---|
| VM ID   | The unique identifier (GUID) of the virtual machine for which the checkpoint is being created |   |

## Create Checkpoint Optional Properties

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Checkpoint Name | The name of the checkpoint   |   |
| Description   | An alphanumeric description of your choice for the checkpoint |   |

## Create Checkpoint Published Data

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Accessibility   | Public or Internal   |   |
| Added Time   | The date and time that the checkpoint was added, in the format yyyy-mm-dd hh:mm:ss AM or PM   |   |
| Checkpoint ID   | The unique identifier (GUID) of the checkpoint   |   |
| Checkpoint Name   | The name of the checkpoint   |   |
| ID   | The unique identifier (GUID) of the checkpoint inside the platform; for example, Hyper-V, VMWare, or Virtual Server |   |
| Description   | An alphanumeric description of the checkpoint   |   |
| Enabled   | True or False. If False, the virtual machine cannot be started.   |   |
| Modified Time   | The most recent modification date and time for the checkpoint, in the format yyyy-mm-dd hh:mm:ss AM or PM   |   |
| Most Recent Task   | The last recorded task for the checkpoint, for example, Start virtual machine   |   |
| Parent Checkpoint ID | The unique identifier (GUID) of the parent of the checkpoint   |   |
| Virtual Disk Drives  | The list of virtual disk drive names recorded for the checkpoint   |   |
| VM ID   | The unique identifier (GUID) of the virtual machine for which the checkpoint was created   |   |
| VM Name   | The name of the virtual machine for which the checkpoint was created   |   |
