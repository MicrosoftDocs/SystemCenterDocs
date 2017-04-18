---
title: Update OS Image
description: The Update OS Image activity updates an operating system image that is in your image repository.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 238dbd87-9e85-450d-b6da-08159767b9ea
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Update OS Image

Applies To: System Center 2016 - Orchestrator

The **Update OS Image** activity updates an operating system image that is in your image repository. It is part of the **Azure Virtual Machine Images** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Update OS Image Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Label   | Specifies the friendly name of the image.   | String   |
| Name   | The name of the operating system image to update.   | String   |
| OS Type   | The operating system type of the operating system image.   | Windows, Linux   |
| Media Link   | Specifies the location of the blob in Windows Azure blob store where the media for the image is located. | String   |
| Wait for Completion | Whether to wait for this operation to complete in Windows Azure before moving on to the next activity.   | True, False   |

## Update OS Image Optional Properties

There are no optional properties for this runbook activity.

## Update OS Image Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Label   | Specifies the friendly name of the image.   | String   |
| Name   | The name of the OS image to update.   | String   |
| OS Type   | The operating system type of the operating system image.   | String   |
| Media Link   | Specifies the location of the blob in Windows Azure blob store where the media for the image is located. | String   |
| Wait for Completion | Whether to wait for this operation to complete in Windows Azure before moving on to the next activity.   | Boolean   |
| Request ID   | The unique identifier of the request to Windows Azure.   | String   |

## See Also


#### Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)

