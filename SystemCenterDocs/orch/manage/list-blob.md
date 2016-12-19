---
title: List Blob
description: The List Blob activity returns all user-defined metadata, standard HTTP properties, and system properties for blobs in the specified container.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1a10dcef-501b-4678-b1dd-ffdd963fa430
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
List Blob
=========

Applies To: System Center 2016 - Orchestrator

The **List Blob** activity returns all user-defined metadata, standard HTTP properties, and system properties for blobs in the specified container. It is part of the **Azure Storage** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

List Blob Required Properties
-----------------------------

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Storage Account Name | The name of the storage account. | String   |
| Container Name   | The name of the container.   | String   |

List Blob Optional Properties
-----------------------------

| **Element** | **Description**   | **Valid values** |
|:---|:---|:---|
| Primary Key | The primary key associated with the storage account. | String   |

List Blob Published Data
------------------------

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

See Also
--------

#### Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)

