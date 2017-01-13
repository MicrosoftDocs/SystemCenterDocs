---
title: Create New Disk from VHD
description: The Create New Disk from VHD activity is used to create a new disk from a VHD and add the disk to an existing virtual machine.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 46968478-f49f-487a-ab84-07d9e2506718
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Create New Disk from VHD

Applies To: System Center 2016 - Orchestrator

The Create New Disk from VHD activity is used to create a new disk from a VHD and add the disk to an existing virtual machine.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Create New Disk from VHD Required Properties

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Bus   | The IDE or SCSI bus to which to attach the disk. If you select &lt;Auto&gt;, the first available value will be selected.   |   |
| Bus Type   | IDE or SCSI   |   |
| File Name   | The name of the VHD on which the new disk will be based. If you select &lt;Auto&gt;, the name will be generated based on the name of the virtual machine to which the disk will be added together with a unique identifier. |   |
| Logical Unit Number (LUN) | The logical unit number (LUN) for the VHD object on an IDE or SCSI bus. If you select &lt;Auto&gt;, the first available value will be selected.   |   |
| Virtual Hard Disk Path   | The location of the VHD used to create the disk   |   |
| VM ID   | The unique identifier (GUID) of the virtual machine to which the disk will be added   |   |

## Create New Disk from VHD Optional Properties

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Boot Volume   | True or False. If True, the virtual machine is started from the disk.   |   |
| System Volume | True or False. If True, the disk contains the operating system for the virtual machine. |   |

## Create New Disk from VHD Published Data

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Accessibility   | Public or Internal   |   |
| Added Time   | The date and time that the disk was added, in the format yyyy-mm-dd hh:mm:ss AM or PM   |   |
| Boot Volume   | True or False. If True, the virtual machine is started from the disk.   |   |
| Bus   | The IDE or SCSI bus to which to attach the disk   |   |
| Bus Type   | IDE or SCSI   |   |
| Description   | An alphanumeric description of the disk   |   |
| Enabled   | True or False. If False, the virtual machine cannot be started.   |   |
| File Name   | The name of the VHD on which the new disk will be based   |   |
| Is VHD   | True or False   |   |
| LUN   | The logical unit number (LUN) for the VHD object on an IDE or SCSI bus   |   |
| Modified Time   | The last modified date and time of the virtual disk, in the format yyyy-mm-dd hh:mm:ss AM or PM |   |
| Pass-through Disk   | A list of names of pass-through disks   |   |
| System Volume   | True or False. If True, the disk contains the operating system for the virtual machine.   |   |
| Virtual Disk Drive ID   | The unique identifier (GUID) of the virtual disk drive   |   |
| Virtual Disk Drive Name | The name of the virtual disk drive   |   |
| Virtual Hard Disk Path  | The location of the VHD used to create the disk   |   |
| VM ID   | The unique identifier (GUID) of the virtual machine for which the disk was created   |   |
