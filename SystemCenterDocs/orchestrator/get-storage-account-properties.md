---
title: Get Storage Account Properties
description: The Get Storage Account Properties activity returns system properties for the specified storage account.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: db5fcc47-994c-4e79-b3b2-78c85919ae9d
author: jyothisuri
ms.author: jsuri
monikerRange: '<=sc-orch-2019'
---

# Get Storage Account Properties

The **Get Storage Account Properties** activity returns system properties for the specified storage account. It's part of the **Azure Storage** category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Get Storage Account Properties Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Storage Account Name | The name of the storage account. | String   |

## Get Storage Account Properties Optional Properties

There are no optional properties for this runbook activity.

## Get Storage Account Properties Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Affinity Group   | The affinity group with which this storage account is associated.   | String   |
| Description   | A description for the storage account.   | String   |
| Geographic Primary Region   | Indicates the primary geographical region in which the storage account exists at this time.   | String   |
| Geographic Replication Enabled | Indicates whether the data in the storage account is replicated across more than one geographic location so as to enable resilience in the face of catastrophic service loss. | Boolean   |
| Geographic Secondary Region   | Indicates the geographical region in which the storage account is being replicated.   | String   |
| Label   | A label for the storage account.   | String   |
| Last Geographic Failover Time  | A timestamp that indicates the most recent instance of a failover to the secondary region.   | Datetime   |
| Location   | The geo-location specified when the storage account was created. This property is only returned if the storage account is not associated with an affinity group.   | String   |
| Service Name   | The name of the storage account.   | String   |
| Service URL   | The Service Management API request URI used to perform requests against the storage account.   | String   |
| Status   | The status of the storage account at the time the operation was called.   | String   |
| Status of Primary   | Indicates whether the primary storage region is available.   | String   |
| Status of Secondary   | Indicates whether the secondary storage region is available.   | String   |
| Storage Account Name   | The name of the storage account.   | String   |
