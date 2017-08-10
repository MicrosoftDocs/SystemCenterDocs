---
title: Delete OS Image
description: The Delete OS Image activity deletes the specified operating system image from your image repository.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 92f0d221-ffe8-4187-9e70-ecea0954174b
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Delete OS Image

Applies To: System Center 2016 - Orchestrator

The **Delete OS Image** activity deletes the specified operating system image from your image repository. It is part of the **Azure Virtual Machine Images** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Delete OS Image Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Name   | The name of the operating system image.   | String   |
| Wait for Completion | Whether to wait for this operation to complete in Azure before moving on to the next activity. | True, False   |

## Delete OS Image Optional Properties

There are no optional properties for this runbook activity.

## Delete OS Image Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Name   | The name of the operating system image.   | String   |
| Wait for Completion | Whether to wait for this operation to complete in Azure before moving on to the next activity. | Boolean   |
| Request ID   | The unique identifier of the request to Azure.   | String   |

## See Also

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)
