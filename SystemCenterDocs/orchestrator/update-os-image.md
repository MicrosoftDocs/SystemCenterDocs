---
title: Update OS Image
description: The Update OS Image activity updates an operating system image that is in your image repository.
ms.custom: engagement-fy23, UpdateFrequency3
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 238dbd87-9e85-450d-b6da-08159767b9ea
author: jyothisuri
ms.author: jsuri
monikerRange: '<=sc-orch-2019'
ms.date: 11/01/2024
ms.update-cycle: 1095-days
---
# Update OS Image

The **Update OS Image** activity updates an operating system image that is in your image repository. It's part of the **Azure Virtual Machine Images** category activity.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Update OS Image Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Label   | Specifies the friendly name of the image.   | String   |
| Name   | The name of the operating system image to update.   | String   |
| OS Type   | The operating system type of the operating system image.   | Windows, Linux   |
| Media Link   | Specifies the location of the blob in Microsoft Azure blob store where the media for the image is located. | String   |
| Wait for Completion | Whether to wait for this operation to complete in Microsoft Azure before moving on to the next activity.   | True, False   |

## Update OS Image Optional Properties

There are no optional properties for this runbook activity.

## Update OS Image Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Label   | Specifies the friendly name of the image.   | String   |
| Name   | The name of the OS image to update.   | String   |
| OS Type   | The operating system type of the operating system image.   | String   |
| Media Link   | Specifies the location of the blob in Microsoft Azure blob store where the media for the image is located. | String   |
| Wait for Completion | Whether to wait for this operation to complete in Microsoft Azure before moving on to the next activity.   | Boolean   |
| Request ID   | The unique identifier of the request to Microsoft Azure.   | String   |

## Other Resources

[Using Runbooks in System Center - Orchestrator](design-and-build-runbooks.md)
