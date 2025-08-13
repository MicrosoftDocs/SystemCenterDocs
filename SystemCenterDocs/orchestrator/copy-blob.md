---
title: Copy Blob
description: The Copy Blob activity copies a blob to a destination within the storage account.
ms.custom: UpdateFrequency2
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: b3512761-a75f-44f0-8fbb-42c683dc2391
author: jyothisuri
ms.author: jsuri
monikerRange: '<=sc-orch-2019'
---
# Copy Blob

The **Copy Blob** activity copies a blob to a destination within the storage account. It's part of the **Azure Storage** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Copy Blob Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Storage Account Name   | The name of the storage account.   | String   |
| Source Container Name   | The name of the source container.   | String   |
| Source Blob Name   | The name of the source blob.   | String   |
| Destination Container Name | The name of the destination container. | String   |
| Destination Blob Name   | The name of the destination blob.   | String   |

## Copy Blob Optional Properties

| **Element** | **Description**   | **Valid values** |
|:---|:---|:---|
| Primary Key | The primary key associated with the storage account. | String   |

## Copy Blob Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Storage Account Name   | The name of the storage account.   | String   |
| Source Container Name   | The name of the source container.   | String   |
| Source Blob Name   | The name of the source blob.   | String   |
| Destination Container Name | The name of the destination container. | String   |
| Destination Blob Name   | The name of the destination blob.   | String   |

## Next steps

[Using Runbooks in System Center - Orchestrator](design-and-build-runbooks.md)
