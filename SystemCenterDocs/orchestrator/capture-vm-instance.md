---
title: Capture VM Instance
description: The Capture VM Instance activity makes a running virtual machine available as an image for reuse.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 568d336c-ed98-4ca1-8783-265a8dd0c6db
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Capture VM Instance

The **Capture VM Instance** activity makes a running virtual machine available as an image for reuse. For Windows-based virtual machines, the image should be sysprepped before capture. After performing the capture, the virtual machine is deleted. This activity is part of the **Azure Virtual Machines** category activity.

>[!CAUTION]
>This activity deletes the virtual machine after it is captured.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Capture VM Instance Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Service Name   | The name of the cloud service containing the virtual machine.   | String   |
| Deployment Name   | The name of the deployment containing the virtual machine.   | String   |
| VM Instance Name   | The name of the virtual machine.   | String   |
| Target Image Name   | Specifies the image name of the captured virtual machine.   | String   |
| Target Image Label  | Specifies the friendly name of the captured virtual machine.   | String   |
| Wait for Completion | Whether to wait for this operation to complete in Azure before moving on to the next activity. | True, False   |

## Capture VM Instance Optional Properties

There are no optional properties for this runbook activity.

## Capture VM Instance Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Service Name   | The name of the cloud service containing the virtual machine.   | String   |
| Deployment Name   | The name of the deployment containing the virtual machine.   | String   |
| VM Instance Name   | The name of the virtual machine.   | String   |
| Target Image Name   | Specifies the image name of the captured virtual machine.   | String   |
| Target Image Label  | Specifies the friendly name of the captured virtual machine.   | String   |
| Wait for Completion | Whether to wait for this operation to complete in Azure before moving on to the next activity. | Boolean   |
| Request ID   | The unique identifier of the request to Azure.   | String   |

## See Also

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)
