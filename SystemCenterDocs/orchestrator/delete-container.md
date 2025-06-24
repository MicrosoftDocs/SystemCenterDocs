---
title: Delete Container
description: The Delete Container activity marks the specified container for deletion.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 299c0f5b-287f-4e68-8657-1cb8696b1668
author: jyothisuri
ms.author: jsuri
robots: noindex
monikerRange: '<=sc-orch-2019'
---
# Delete Container

The **Delete Container** activity marks the specified container for deletion. The container and any blobs contained within it are later deleted during garbage collection. It's part of the **Azure Storage** category activity.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

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

[Using Runbooks in System Center - Orchestrator](design-and-build-runbooks.md)
