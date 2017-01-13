---
title: Create Change with Template
description: The Create Change with Template activity is used to configure a change record based on an existing template.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3da4a26-1781-4dc8-b0a9-74dd0a2d52a5
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Create Change with Template

Applies To: System Center 2016 - Orchestrator

The Create Change with Template activity is used to configure a change record based on an existing template.

<br><br><strong>Important </strong><br>Important System Center Orchestrator 2016 does not support the use of mandatory fields in child objects that the Create Change with Template activity creates. These template activities will fail in Service Manager if there are mandatory fields in any of the child objects it tries to create. This is because there is no way for the user to provide the mandatory properties for the associated activity.<br><br>

The Create Change with Template activities create a change record by presenting the workflow author with a property grid of values associated with the change. This includes mandatory properties that will cause the create operation to be rejected by Service Manager if they are not provided.

The configuration user interface for Create Change with Template does not provide a way to configure child work items. It can only access the parent change. Therefore, if any of the child work items contain mandatory properties, the creation of the change will be rejected by Service Manager.

The following published data elements are specific to Create Change with Template. Additional published data is generated based on the class that you select when you define the activity. For a list of the data elements published by each class, see [Service Manager Published Data](service-manager-published-data.md).

## Create Change with Template Published Data

|   |   |
|-------------------|----------------------------------------------------------------------------|
| Element   | Description   |
| Template ID   | The unique identifier of the template used to create the change   |
| Number of Objects | The number of objects returned by the Create Change with Template activity |
