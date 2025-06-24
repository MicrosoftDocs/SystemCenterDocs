---
title: Regenerate Storage Account Key
description: The Regenerate Storage Account Key activity regenerates the primary or secondary access key for the specified storage account.
ms.custom: UpdateFrequency3
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1483a1dd-43fb-446f-a7e6-a18f6760b7a6
author: jyothisuri
ms.author: jsuri
robots: noindex
monikerRange: '<=sc-orch-2019'
ms.date: 11/01/2024
---
# Regenerate Storage Account Key

The **Regenerate Storage Account Key** activity regenerates the primary or secondary access key for the specified storage account. It's part of the **Azure Storage** category activity.

>[!NOTE]
>Using this activity will publish the new storage account key to the Orchestrator databus. If you choose to use this activity, ensure to appropriately protect the key after regeneration.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## Regenerate Storage Account Key required properties

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Storage Account Name | The name of the storage account.   | String   |
| Key Type   | Specifies which key to regenerate. | Primary, Secondary |

## Regenerate Storage Account Key optional properties

There are no optional properties for this runbook activity.

## Regenerate Storage Account Key published data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Primary Key   | The primary access key for the storage account.   | String   |
| Secondary Key   | The secondary access key for the storage account. | String   |
| Storage Account Name | The name of the storage account.   | String   |
