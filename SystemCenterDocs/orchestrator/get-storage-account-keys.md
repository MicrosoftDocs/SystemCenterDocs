---
title: Get Storage Account Keys
description: The Get Storage Account Keys activity returns the primary and secondary access keys for the specified storage account.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 3d8d8e98-4d80-4a4e-af7f-07ab5e8d8d9c
author: jyothisuri
ms.author: jsuri
monikerRange: '<=sc-orch-2019'
---

# Get Storage Account Keys

The **Get Storage Account Keys** activity returns the primary and secondary access keys for the specified storage account. It's part of the **Azure Storage** category activity.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Get Storage Account Keys Required Properties

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Storage Account Name | The name of the storage account. | String   |

## Get Storage Account Keys Optional Properties

There are no optional properties for this runbook activity.

## Get Storage Account Keys Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Primary Key   | The primary access key for the storage account.   | String   |
| Secondary Key   | The secondary access key for the storage account. | String   |
| Storage Account Name | The name of the storage account.   | String   |
