---
title: Monitor Object
description: The Monitor Object activity uses filter criteria to look for new and updated records that satisfy the criteria that you specify.
ms.custom: UpdateFrequency3
ms.date: 12/02/2016
ms.prod: system-center
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b7b5b75e-f73b-45ad-83d8-dca98079d88f
author: jyothisuri
ms.author: jsuri
manager: mkluck
robots: noindex
---
# Monitor Object

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

The Monitor Object activity uses filter criteria to look for new and updated records that satisfy the criteria that you specify. Only one Monitor Object activity can be used per workflow.

The following published data element is specific to Monitor Object. Additional published data is generated based on the class that you select when you define the activity. For a list of the data elements published by each class, see [Service Manager Published Data](service-manager-published-data.md).

## Monitor Object published data

| Element   | Description   |
|-------------------|---------------------------------------------------------------|
| Number of Objects | The number of objects returned by the Monitor Object activity |
