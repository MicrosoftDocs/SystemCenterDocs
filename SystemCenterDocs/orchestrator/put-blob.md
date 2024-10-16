---
title: Put Blob
description: The Put Blob activity creates a new block blob from the specified file, or updates the content of an existing block blob.
ms.custom: UpdateFrequency3
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 81fab0b3-5c85-4434-826c-eebf098c7511
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
robots: noindex
monikerRange: '<=sc-orch-2019'
ms.date: 04/27/2023
---
# Put Blob



The **Put Blob** activity creates a new block blob from the specified file, or updates the content of an existing block blob. It's part of the **Azure Storage** category activity.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Put Blob required properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Storage Account Name   | The name of the storage account. | String   |
| Container Name   | The name of the container.   | String   |
| Blob Name   | A name for the blob.   | String   |
| File to Upload (File Path) | The file to upload.   | String   |

## Put Blob optional properties

| **Element** | **Description**   | **Valid values** |
|:---|:---|:---|
| Primary Key | The primary key associated with the storage account.   | String   |
| Metadata   | Metadata to associate with the blob. Should be in the format "Name1:Value1,Name2:Value2" | String   |

## Put Blob published data

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
| File To Upload (File Path) | The file to upload.   | String   |
| Last Modified Time (UTC)   | Returns the date and time the container was last modified.   | Datetime   |
| Lease Status   | The blob's lease status.   | String   |
| Length (Bytes)   | The size of the blob, in bytes.   | Integer   |
| Metadata   | Metadata associated with the blob. Should be in the format "Name1:Value1,Name2:Value2" | String   |
| Storage Account Name   | The name of the storage account.   | String   |
