---
title: Get Object
description: The Get Object activity is used to search for a record based on a set of filter criteria.
ms.custom: na
ms.date: 4/25/2017
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: e1217c55-4f07-4892-8480-65ea1d453be1
author: cfreemanwa
ms.author: raynew
manager: carmonm
---
# Get Object

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

The Get Object activity is used to search for a record based on a set of filter criteria. The Get Object activity supports incidents, changes, and activities.

The following published data element is specific to Get Object. Additional published data is generated based on the class that you select when you define the activity. For a list of the data elements published by each class, see [Service Manager Published Data](service-manager-published-data.md).

## Get Object Published Data

| Element   | Description   |
|-------------------|-----------------------------------------------------------|
| Number of Objects | The number of objects returned by the Get Object activity |
