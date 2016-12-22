---
title: Update Disk
description: The Update Disk activity is used to add more disk space and to change some of the properties of an existing disk.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49456582-3214-450f-afca-cbe812fdaed7
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
Update Disk
===========

Applies To: System Center 2016 - Orchestrator

The Update Disk activity is used to add more disk space and to change some of the properties of an existing disk.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

Update Disk Required Properties
-------------------------------

| Element | Description   | Valid Values |
|:---|:---|:---|
| VM ID   | The unique identifier (GUID) of the virtual machine for which the disk was created |   |

Update Disk Optional Properties
-------------------------------

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Additional Size (GB)   | The amount of disk space in GB to add to the disk   |   |
| Bus   | The IDE or SCSI bus to which to attach the disk   |   |
| Bus Type   | IDE or SCSI   |   |
| Compact   | True or False. Compacting only works on a dynamically expanding virtual hard disk to reduce the size of the VHD file as much as possible. |   |
| Disk Type   | Dynamic or Fixed   |   |
| Logical Unit Number (LUN) | The logical unit number (LUN) for the VHD object on an IDE or SCSI bus   |   |

Update Disk Published Data
--------------------------

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Accessibility   | Public or Internal   |   |
| Added Time   | The date and time that the Virtual Disk was added, in the format yyyy-mm-dd hh:mm:ss AM or PM   |   |
| Additional Size (GB)   | The amount of disk space in gigabytes (GB) to add to the disk   |   |
| Boot Volume   | True or False. If True, the virtual machine is started from the disk.   |   |
| Bus   | The IDE or SCSI bus to which to attach the disk   |   |
| Bus Type   | IDE or SCSI   |   |
| Compact   | True or False. Compacting only works on a dynamically expanding virtual hard disk to reduce the size of the VHD file as much as possible. |   |
| Disk Type   | Dynamic or Fixed   |   |
| Enabled   | True or False. If False, the virtual machine cannot be started.   |   |
| File Name   | The name of the VHD on which the new disk will be based   |   |
| Is VHD   | True or False   |   |
| LUN   | The logical unit number (LUN) for the VHD object on an IDE or SCSI bus   |   |
| Modified Time   | The last modified date and time of the Virtual Disk, in the format yyyy-mm-dd hh:mm:ss AM or PM   |   |
| Pass-through Disk   | A list of names of pass-through disks   |   |
| System Volume   | True or False. If True, the disk contains the operating system for the virtual machine.   |   |
| Virtual Disk Drive Name | The name of the virtual disk drive   |   |
| Virtual Hard Disk Path  | The location of the VHD used to create the disk   |   |
| VM ID   | The unique identifier (GUID) of the virtual machine for which the disk was created   |   |
