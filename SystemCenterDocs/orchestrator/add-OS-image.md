---
title: Add OS Image
description: The Add OS Image activity adds an operating system image that is currently stored in a storage account in your subscription to the image repository.
ms.custom: UpdateFrequency2
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0d88f548-97ef-4fb4-9f1c-4f45b0afc796
author: jyothisuri
ms.author: jsuri
robots: noindex
monikerRange: '<=sc-orch-2019'
---
# Add OS Image

The **Add OS Image** activity adds an operating system image that is currently stored in a storage account in your subscription to the image repository. It's part of the **Azure Virtual Machine Images** category activity.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Add OS Image Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Label   | Specifies the friendly name of the image.   | String   |
| Name   | Specifies a name for the operating system image that Windows Azure uses to identify the image when creating one or more virtual machines. | String   |
| OS Type   | The operating system type of the operating system image.   | Windows, Linux   |
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

## Next steps

[Using Runbooks in System Center - Orchestrator](design-and-build-runbooks.md)
