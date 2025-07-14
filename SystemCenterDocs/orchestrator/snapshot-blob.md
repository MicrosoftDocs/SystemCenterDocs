---
title: Snapshot Blob
description: The Snapshot Blob activity creates a read-only snapshot of a blob.
ms.custom: UpdateFrequency3
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 4817dd67-6ee5-4c2f-86dd-82b3ee90fa51
author: jyothisuri
ms.author: jsuri
robots: noindex
monikerRange: '<=sc-orch-2019'
ms.date: 11/01/2024
ms.update-cycle: 1095-days
---
# Snapshot Blob

The **Snapshot Blob** activity creates a read-only snapshot of a blob. It's part of the **Azure Storage** category activity.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

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

## Other Resources

[Using Runbooks in System Center - Orchestrator](design-and-build-runbooks.md)
