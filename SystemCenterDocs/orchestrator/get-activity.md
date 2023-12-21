---
title: Get Activity
description: The Get Activity activity is used to query for activity records for the selected activity class.
ms.custom: UpdateFrequency3
ms.date: 4/25/2017
ms.prod: system-center
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 60938aea-2ad0-42b2-b425-09d02b3d5053
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
---

# Get Activity

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

The Get Activity activity is used to query for activity records for the selected activity class.

The following published data elements are specific to Get Activity. Additional published data is generated based on the class that you select when you define the activity. For a list of the data elements published by each class, see [Service Manager Published Data](service-manager-published-data.md).

## Get Activity Published Data

| Element   | Description   |
|-------------------|---------------------------------------------------------------------|
| Object GUID   | The unique identifier (GUID) of the single activity to be retrieved |
| Number of Objects | The number of objects returned by Get Activity   |
