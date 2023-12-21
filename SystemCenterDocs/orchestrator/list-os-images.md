---
title: List OS Images
description: The List OS Images activity retrieves a list of the operating system images from the image repository.
ms.custom: UpdateFrequency3
ms.date: 04/27/2023
ms.prod: system-center
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b89cdf77-e3d9-4513-a0c6-657bdc0ef3c7
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
robots: noindex
monikerRange: '<=sc-orch-2019'
---
# List OS Images

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

The **List OS Images** activity retrieves a list of the operating system images from the image repository. It's part of the **Azure Virtual Machine Images** category activity.

The activity publishes all the data from the required and optional properties into published data. The following tables list the required and optional properties and published data for this activity.

## List OS Images required properties

There are no required properties for this runbook activity.

## List OS Images optional properties

There are no optional properties for this runbook activity.

## List OS Images published data

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Label   | Specifies the friendly name of the image.   | String   |
| Name   | The name of the operating system image.   | String   |
| OS Type   | The operating system type of the operating system image.   | String   |
| Media Link   | Specifies the location of the blob in Windows Azure blob store where the media for the image is located.   | String   |
| Affinity Group  | The affinity in which the media is located. The Affinity Group value is derived from the storage account that contains the blob in which the media is located. | String   |
| Category   | The repository classification of the image.   | String   |
| Disk Size in GB | The size, in GB, of the image.   | Integer   |
| Location   | The geo-location in which this media is located. The location value is derived from the storage account that contains the blob in which the media is located.  | String   |
| Raw XML Body   | The raw XML output returned by Windows Azure for this operation.   | String   |
