---
title: List Blob
description: The List Blob activity returns all user-defined metadata, standard HTTP properties, and system properties for blobs in the specified container.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 1a10dcef-501b-4678-b1dd-ffdd963fa430
author: jyothisuri
ms.author: jsuri
monikerRange: '<=sc-orch-2019'
---

# List Blob

The **List Blob** activity returns all user-defined metadata, standard HTTP properties, and system properties for blobs in the specified container. It's part of the **Azure Storage** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## List Blob Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Storage Account Name | The name of the storage account. | String   |
| Container Name   | The name of the container.   | String   |

## List Blob Optional Properties

| **Element** | **Description**   | **Valid values** |
|:---|:---|:---|
| Primary Key | The primary key associated with the storage account. | String   |

## List Blob Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Blob Name   | The name of the blob.   | String   |
| Blob Type   | The type of the blob.   | String   |
| Blob URL   | The absolute URI to the blob.   | String   |
| Cache Control   | The blob's cache control value.   | String   |
| Container Name   | The name of the container.   | String   |
| Content Encoding   | The content encoding of the blob.   | String   |
| Content Language   | The content language of the blob.   | String   |
| Content MD5   | The MD5 hash of the blob.   | String   |
| ETag   | The entity tag for the blob.   | String   |
| Last Modified Time (UTC) | Returns the date and time the container was last modified.   | Datetime   |
| Lease Status   | The blob's lease status.   | String   |
| Length (Bytes)   | The size of the blob, in bytes.   | Integer   |
| Metadata   | Metadata associated with the blob in the format "Name1:Value1,Name2:Value2" | String   |
| Storage Account Name   | The name of the storage account.   | String   |
