---
title: Snapshot Blob
description: The Snapshot Blob activity creates a read-only snapshot of a blob.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4817dd67-6ee5-4c2f-86dd-82b3ee90fa51
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Snapshot Blob

Applies To: System Center 2016 - Orchestrator

The **Snapshot Blob** activity creates a read-only snapshot of a blob. It is part of the **Azure Storage** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Snapshot Blob Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Storage Account Name | The name of the storage account. | String   |
| Container Name   | The name of the container.   | String   |
| Blob Name   | The name of the blob.   | String   |

## Snapshot Blob Optional Properties

| **Element** | **Description**   | **Valid values** |
|:---|:---|:---|
| Primary Key | The primary key associated with the storage account. | String   |

## Snapshot Blob Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Blob Name   | The name of the blob.   | String   |
| Container Name   | The name of the container.   | String   |
| Snapshot Time   | The time of the snapshot.   | Datetime   |
| Storage Account Name | The name of the storage account. | String   |

## See Also


#### Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)

