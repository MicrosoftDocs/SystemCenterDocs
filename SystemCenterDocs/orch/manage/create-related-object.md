---
title: Create Related Object
description: The Create Related Object activity is used to create a new Service Manager object that is related to other existing objects either by membership or by a hosted relationship.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 06e71bd9-60d6-4a75-b658-d34791a75e5b
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Create Related Object

Applies To: System Center 2016 - Orchestrator

The Create Related Object activity is used to create a new Service Manager object that is related to other existing objects either by membership or by a hosted relationship.

The following published data elements are specific to Create Related Object. Additional published data is generated based on the class that you select when you define the activity. For a list of the data elements published by each class, see Service Manager Published Data.

Certain classes contain a mandatory ID property which requires a GUID. Generating a GUID is the responsibility of the workflow author, and can be generated using a .NET scripting activity with the following procedure.

#### To create a class with an ID property

1.  Create a Run .NET Script activity using the following method: $GUID = \[guid\]::NewGUID().

2.  On the Published Data tab, define the GUID variable using the following settings:Name: guidType: StringVariable: GUID

When the .NET Script Activity runs, it will generate a GUID that you can subscribe to in the ID property of the activity you are creating.

## Create Related Object Published Data

|   |   |
|---------------------------|---------------------------------------------------------------------------------------|
| Element   | Description   |
| Relationship Type   | Describes how the source class and target class are related to each other   |
| Source Class   | The name of the source class used to build the relationship   |
| Source Object GUID   | The unique identifier (GUID) of a single source object used to build the relationship |
| Target Class   | The name of the target class used to build the relationship   |
| Target Object GUID   | The unique identifier (GUID) of a single target object used to build the relationship |
| System Center Object GUID | The unique identifier (GUID) for the object   |
| Number of Objects   | The number of objects returned by Create Related Object   |
