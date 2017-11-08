---
title: Create Object
description: The Create Object is used to create a new Service Manager record associated with a specified class.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: ef4f2dd4-3ba2-4781-a0a9-cd153feb8ea9
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Create Object

The Create Object is used to create a new Service Manager record associated with a specified class. This activity includes support for incidents and changes.

The following published data element is specific to Create Object. Additional published data is generated based on the class that you selected when you defined the object. For a list of the data elements published by each class, see Service Manager Published Data.

Certain classes contain a mandatory ID property which requires a GUID. Generating a GUID is the responsibility of the workflow author, and can be generated using a .NET scripting activity with the following procedure.

#### To create a class with an ID property

1.  Create a Run .NET Script activity using the following method: $GUID = \[guid\]::NewGUID().

2.  On the Published Data tab, define the GUID variable using the following settings:Name: guidType: StringVariable: GUID

When the .NET Script Activity runs, it will generate a GUID that you can subscribe to in the ID property of the activity you are creating.

## Create Object Published Data

| Element   | Description   |
|-------------------|--------------------------------------------------------------|
| Number of Objects | The number of objects returned by the Create Object activity |
