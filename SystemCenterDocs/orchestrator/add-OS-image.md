---
title: Add OS Image
description: The Add OS Image activity adds an operating system image that is currently stored in a storage account in your subscription to the image repository.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 0d88f548-97ef-4fb4-9f1c-4f45b0afc796
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Add OS Image

Applies To: System Center 2016 - Orchestrator

The **Add OS Image** activity adds an operating system image that is currently stored in a storage account in your subscription to the image repository. It is part of the **Azure Virtual Machine Images** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Add OS Image Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Label   | Specifies the friendly name of the image.   | String   |
| Name   | Specifies a name for the operating system image that Windows Azure uses to identify the image when creating one or more virtual machines. | String   |
| OS Type   | The operating system type of the opertaing system image.   | Windows, Linux   |
| Media Link   | Specifies the location of the blob in Windows Azure blob store where the media for the image is located.   | String   |
| Wait for Completion | Whether to wait for this operation to complete in Windows Azure before moving on to the next activity.   | True, False   |

## Add OS Image Optional Properties

There are no optional properties for this runbook activity.

## Add OS Image Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Label   | Specifies the friendly name of the image.   | String   |
| Name   | Specifies a name for the operating system image that Windows Azure uses to identify the image when creating one or more virtual machines. | String   |
| OS Type   | The operating system type of the operating system image.   | String   |
| Media Link   | Specifies the location of the blob in Windows Azure blob store where the media for the image is located.   | String   |
| Wait for Completion | Whether to wait for this operation to complete in Windows Azure before moving on to the next activity.   | Boolean   |
| Request ID   | The unique identifier of the request to Windows Azure.   | String   |

## See Also

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)
