---
title: List Container
description: The List Container activity returns a list of the containers under the specified storage account.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 6b2bb18f-00dd-44da-a4be-d2ec57f9a257
author: rayne-wiselman
ms.author: raynew
manager: carmonm
robots: noindex
---
# List Container

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

The **List Container** activity returns a list of the containers under the specified storage account. It is part of the Azure Storage category activity.

The activity publishes all of the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## List Container Required Properties

| **Element**   | **Description**   | **Valid Values** |
|:---|:---|:---|
| Storage Account Name | The name of the storage account. | String   |

## List Container Optional Properties

| **Element** | **Description**   | **Valid Values** |
|:---|:---|:---|
| Primary Key | The primary key associated with the storage account. | String   |

## List Container Published Data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Container Name   | The name of the container.   | String   |
| Url   | The absolute URI to the container.   | String   |
| ETag   | The entity tag for the container.   | String   |
| Last Modified Time   | Returns the date and time the container was last modified. | DateTime   |
| Storage Account Name | The name of the storage account.   | String   |
