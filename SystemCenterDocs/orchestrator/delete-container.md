---
title: Delete Container
description: The Delete Container activity marks the specified container for deletion.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 299c0f5b-287f-4e68-8657-1cb8696b1668
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Delete Container

Applies To: System Center 2016 - Orchestrator

The **Delete Container** activity marks the specified container for deletion. The container and any blobs contained within it are later deleted during garbage collection. It is part of the **Azure Storage** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Delete Container Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Storage Account Name | The name of the storage account. | String   |
| Container Name   | A name for the container.   | String   |

## Delete Container Optional Properties

| **Element** | **Description**   | **Valid values** |
|:---|:---|:---|
| Primary Key | The primary key associated with the storage account. | String   |

## Delete Container Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Container Name   | The name of the container.   | String   |
| Storage Account Name | The name of the storage account. | String   |

## See Also

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)
