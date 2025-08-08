---
title: Create Incident with Template
description: The Create Incident with Template activity is used to create a new incident from an existing Incident Template.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 02bcec02-12cc-4dd1-858c-beecbb7cbd3c
author: jyothisuri
ms.author: jsuri
---
# Create Incident with Template

The Create Incident with Template activity is used to create a new incident from an existing Incident Template. You've the option to overwrite template values with the existing incident values or apply template values.

>[!IMPORTANT]
>Orchestrator doesn't support mandatory fields in child activities that the Create Incident with Template activity creates. These template activities will fail in Service Manager if there are mandatory fields in any of the child activities it tries to create because there is no way for the user to provide the mandatory properties for the associated activity.

The Create Incident with Template activities create an incident record by presenting the workflow author with a property grid of values associated with the change. This includes mandatory properties that will cause the create operation to be rejected by Service Manager if they aren't provided.

The configuration user interface for Create Incident with Template doesn't provide a way to configure child work items. It can only access the parent incident. Therefore, if any of the child work items contain mandatory properties, the creation of the incident will be rejected by Service Manager.

The following published data elements are specific to Create Incident with Template activity. Additional published data is generated based on the class that you select when you define the activity. For a list of data elements published by each class, see [Service Manager Published Data](service-manager-published-data.md).

## Create Incident with Template Published Data

| Element   | Description   |
|---------------------------|------------------------------------------------------------------------------|
| System Center Object GUID | The unique identifier (GUID) of the incident   |
| Number of Objects   | The number of objects returned by the Create Incident with Template activity |
