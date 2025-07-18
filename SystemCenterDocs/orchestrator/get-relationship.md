---
title: Get Relationship
description: The Get Relationship activity is used to generate a list of objects from two different classes that are related by the criteria you specify.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 7ccabcbe-6594-4db6-813d-a0dfaa3258df
author: jyothisuri
ms.author: jsuri
---

# Get Relationship

The Get Relationship activity is used to generate a list of objects from two different classes that are related by the criteria you specify.

The following published data elements are specific to Get Relationship. Additional published data is generated based on the class that you select when you define the activity. For a list of the data elements published by each class, see [Service Manager Published Data](service-manager-published-data.md).

## Get Relationship Published Data

| Element   | Description   |
|----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Number of Objects   | The number of objects returned by the Get Relationship activity.   |
| Object Class   | The name of a class for which you want to define a relationship to the related class.   |
| Object GUID   | The unique identifier (GUID) of a single object in the object class that is used to define the relationship to another class. |
| Related Class   | The name of a class for which you want to define a relationship to the object class.  |
| Related Object GUID   | The unique identifier (GUID) of a single object in the second class that is used to define the relationship.  |
| Relationship Object GUID | The unique identifier (GUID) of the items returned by the Get Relationship activity.  |
