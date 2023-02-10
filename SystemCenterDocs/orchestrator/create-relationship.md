---
title: Create Relationship
description: The Create Relationship activity is used to create a relationship between two existing entities.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 63ab5e0c-4407-401b-9f43-59ca1a3a4915
author: jyothisuri
ms.author: jsuri
manager: mkluck
robots: noindex
---
# Create Relationship

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

The Create Relationship activity is used to create a relationship between two existing entities. For example, you can create a one-to-many relationship between incidents and customers.

The following published data elements are specific to Create Relationship. Additional published data is generated based on the class that you select when you define the activity. For a list of the data elements published by each class, see [Service Manager Published Data](service-manager-published-data.md).

## Create Relationship Published Data

| Element   | Description   |
|---------------------------|---------------------------------------------------------------------------------------|
| Relationship Type   | Describes how the source class and target class are related to each other   |
| Source Class   | The name of the source class used to build the relationship   |
| Source Object GUID   | The unique identifier (GUID) of a single source object used to build the relationship |
| Target Class   | The name of the target class used to build the relationship   |
| Target Object GUID   | The unique identifier (GUID) of a single target object used to build the relationship |
| System Center Object GUID | The unique identifier (GUID) for the object   |
| Number of Objects   | The number of objects returned by Create Relationship   |
