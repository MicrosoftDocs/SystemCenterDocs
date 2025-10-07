---
title: Create Object
description: The Create Object is used to create a new Service Manager record associated with a specified class.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: how-to
ms.assetid: ef4f2dd4-3ba2-4781-a0a9-cd153feb8ea9
author: Jeronika-MS
ms.author: v-gajeronika
---
# Create Object

The Create Object is used to create a new Service Manager record associated with a specified class. This activity includes support for incidents and changes.

The following published data element is specific to Create Object. Additional published data is generated based on the class that you selected when you defined the object. For a list of data elements published by each class, see Service Manager Published Data.

Certain classes contain a mandatory ID property, which requires a GUID. Generating a GUID is the responsibility of the workflow author and can be generated using a .NET scripting activity with the following procedure.

### Create a class with an ID property

1. Create a Run .NET Script activity using the following method: `$GUID = \[guid\]::NewGUID()`.

2. On the **Published Data** tab, define the GUID variable using the following settings:
    1. Name: guid
    2. Type: String
    3. Variable: GUID

When the .NET Script Activity runs, it will generate a GUID that you can subscribe to in the ID property of the activity you're creating.

## Create Object Published Data

| Element   | Description   |
|-------------------|--------------------------------------------------------------|
| Number of Objects | The number of objects returned by the Create Object activity |
