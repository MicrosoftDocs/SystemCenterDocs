---
title: Create New Disk
description: The Create New Disk activity is used to create a new disk and add it to a virtual machine.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 6565cdb0-f0f7-4d4a-a08d-f4016806e0c6
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Create New Disk

Applies To: System Center 2016 - Orchestrator

The Create New Disk activity is used to create a new disk and add it to a virtual machine.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Create New Disk Required Properties

| Element   | Description    |
|:---|:---|
| Bus   | The IDE or SCSI bus to which to attach the disk. If you select &lt;Auto&gt; then the first available value will be selected.   |   
| Bus Type   | IDE or SCSI   |   
| Disk Type   | Dynamic or Fixed   |   
| File Name   | The name of the VHD on which the new disk will be based   |   
| Logical Unit Number (LUN) | The logical unit number (LUN) for the VHD object on an IDE or SCSI bus. If you select &lt;Auto&gt; then the first available value will be selected. |   
| Size (MB)   | The size of the Virtual Disk in megabytes (MB)   |   
| VM ID   | The unique identifier (GUID) of the virtual machine for which the disk was created   |   

## Create New Disk Optional Properties

| Element   | Description   |
|:---|:---|
| Boot Volume   | True or False. If True, the virtual machine is started from the disk.   |   
| System Volume | True or False. If True, the disk contains the operating system for the virtual machine. |   

## Create New Disk Published Data

| Element   | Description   
|:---|:---|
| Accessibility   | Public or Internal   |   
| Added Time   | The date and time that the disk was added, in the format yyyy-mm-dd hh:mm:ss AM or PM   |   
| Boot Volume   | True or False. If True, the virtual machine is started from the disk.   |   
| Bus   | The IDE or SCSI bus to which to attach the disk   |   
| Bus Type   | IDE or SCSI   |   
| Disk Type   | Dynamic or Fixed   |   
| Enabled   | True or False. If False, the virtual machine cannot be started.   |   
| File Name   | The name of the VHD on which the new disk will be based   |   
| Is VHD   | True or False   |   
| LUN   | The logical unit number (LUN) for the VHD object on an IDE or SCSI bus   |   
| Modified Time   | The last modified date and time of the disk, in the format yyyy-mm-dd hh:mm:ss AM or PM |   
| Pass-through Disk   | A list of names of pass-through disks   |   
| Size (MB)   | The size of the Virtual Disk in MB   |   
| System Volume   | True or False. If True, the disk contains the operating system for the virtual machine. |   
| Virtual Disk Drive Name | The name of the virtual disk drive   |   
| Virtual Hard Disk Path  | The location of the VHD used to create the disk   |   
| VM ID   | The unique identifier (GUID) of the virtual machine for which the disk was created   |   
