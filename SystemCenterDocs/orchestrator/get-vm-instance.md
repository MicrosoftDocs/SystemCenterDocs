---
title: Get VM instance
description: The Get VM Instance activity retrieves the specified virtual machine.
ms.custom: na
ms.date: 4/25/2017
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: db87de08-2b60-48da-b908-23d0b83f5146
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
---

# Get VM instance

Applies To: System Center 2016 - Orchestrator

The **Get VM Instance** activity retrieves the specified virtual machine. It is part of the **Azure Virtual Machines** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Get VM Instance Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| VM Service Name   | The name of the cloud service containing the virtual machine. | String   |
| VM Deployment Name | The name of the deployment containing the virtual machine.   | String   |
| VM Instance Name   | The name of the virtual machine.   | String   |

## Get VM Instance Optional Properties

There are no optional properties for this runbook activity.

## Get VM Instance Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Availability Set For The VM   | The name of the availability set the virtual machine belongs to. Virtual machines specified in the same availability set are allocated to different nodes to maximize availability. | String   |
| Back End Subnet   | The name of the backend subnet to which the virtual machine belongs.   | String   |
| Configuration Set Type   | Contains the configuration type.   | String   |
| Data Disk Host Caching   | The platform caching behavior of the data disk blob for read/write efficiency.   | String   |
| Data Disk Label   | The description of the data disk in the image repository.   | String   |
| Data Disk Name   | The image in the image repository used to create the data disk for the virtual machine.   | String   |
| Disk Size in GB   | The size, in GB, of the VHD attached to the virtual machine.   | Integer   |
| Enable Direct Server Return   | Whether direct server return is enabled.   | Boolean   |
| Endpoint Name   | The name of the external endpoint.   | String   |
| Endpoint Protocol   | The transport protocol for the endpoint.   | String   |
| External Port Number   | The external port used for the endpoint.   | Integer   |
| Front End Subnet   | The name of the frontend subnet to which the virtual machine belongs.   | String   |
| Load Balancer Probe Protocol   | The protocol used to inspect the virtual machine availability status.   | String   |
| Load Balanced Endpoint Set Name | The name of the set of load balanced endpoints.   | String   |
| Local Port Number   | The internal port on which the virtual machine is listening to serve the endpoint.   | Integer   |
| Logical Unit Number   | The Logical Unit Number (LUN) for the data disk. The LUN specifies the slot in which the data drive appears when mounted for usage by the virtual machine.   | Integer   |
| OS Disk Host Caching   | Indicates whether the OS disk can be cached for greater efficiency during writes.   | String   |
| OS Disk Label   | The friendly name of the disk containing the guest OS image in the image repository.   | String   |
| OS Disk Media Link   | The URI of the location of a blob in the customer storage account that contains the OS image used to create the disk.   | String   |
| OS Disk Name   | The name an operating system image in the image repository.   | String   |
| OS Disk Source Image Name   | The name of the disk image used to create the virtual machine.   | String   |
| Port To Use For Status   | The port used to inspect the virtual machine availability status.   | Integer   |
| Raw XML Data   | The raw XML output returned by Windows Azure for this operation.   | String   |
| Relative Path Containing Status | The relative path name to inspect to determine the virtual machine availability status.   | String   |
| VM Instance Name   | The name of the virtual machine.   | String   |
| VM Instance Size   | The size allocated for the virtual machine.   | String   |
| VM Instance Type   | The type of the virtual machine.   | String   |
| VM Service Name   | The name of the cloud service containing the virtual machine.   | String   |
| VM Deployment Name   | The name of the deployment containing the virtual machine.   | String   |
| VM Instance Name   | The name of the virtual machine.   | String   |
| Virtual IP   | Indicates the virtual IP address of the virtual machine.   | String   |

