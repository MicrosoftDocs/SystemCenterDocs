---
title: Get Disk
description: The Get Disk activity is used to retrieve an existing virtual disk based on the filters that you specify.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 18befb12-ce3b-48e3-98fc-7d7b6ff34ff9
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Get Disk

Applies To: System Center 2016 - Orchestrator

The Get Disk activity is used to retrieve an existing virtual disk based on the filters that you specify.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Get Disk Required Properties

| Element   | Description   |
|:---|:---|
| Accessibility   | Public or Internal   |  
| Added Time   | The date and time that the disk was added, in the format yyyy-mm-dd hh:mm:ss AM or PM   |  
| Bus   | The IDE or SCSI bus to which to attach the disk   |  
| Bus Type   | IDE or SCSI   |  
| Enabled   | True or False. If False, the virtual machine cannot be started.   |  
| Is VHD   | True or False   |  
| LUN   | The logical unit number (LUN) for the VHD object on an IDE or SCSI bus   |  
| Modified Time   | The last modified date and time of the disk, in the format yyyy-mm-dd hh:mm:ss AM or PM   |  
| Pass-through Disk   | A list of names of pass-through disks   |  
| Template ID   | The unique identifier (GUID) of the template that was used to create the disk   |  
| Virtual Hard Disk Path  | The location of the VHD used to create the disk   |  
| Virtual Disk Drive Name | The name of the virtual disk drive   |  
| VM ID   | The unique identifier (GUID) of the virtual machine for which the virtual disk was created |  

## Get Disk Published Data

| Element   | Description   |
|:---|:---|
| Accessibility   | Public or Internal   |  
| Added Time   | The date and time that the disk was added, in the format yyyy-mm-dd hh:mm:ss AM or PM   |  
| Bus   | The IDE or SCSI bus to which to attach the disk   |  
| Bus Type   | IDE or SCSI   |  
| Enabled   | True or False. If False, the virtual machine cannot be started.   |  
| Is VHD   | True or False   |  
| LUN   | The logical unit number (LUN) for the VHD object on an IDE or SCSI bus   |  
| Modified Time   | The last modified date and time of the Virtual Disk, in the format yyyy-mm-dd hh:mm:ss AM or PM  |  
| Pass-through Disk   | A list of names of pass-through disks   |  
| Template ID   | The unique identifier (GUID) of the template that was used to create the disk   |  
| Virtual Hard Disk Path  | The location of the VHD used to create the disk   |  
| Virtual Disk Drive Name | The name of the virtual disk drive   |  
| VM ID   | The unique identifier (GUID) of the virtual machine for which the Virtual Disk Drive was created |  
