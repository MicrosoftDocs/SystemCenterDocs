---
title: Create Change with Template activity
description: The Create Change with Template activity is used to configure a change record based on an existing template.
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.subservice: orchestrator
ms.topic: concept-article
author: Jeronika-MS
ms.author: v-gajeronika
ms.custom: UpdateFrequency3, engagement-fy24
---
# Create Change with Template activity

The Create Change with Template activity is used to configure a change record based on an existing template.

>[!IMPORTANT]
>System Center -Orchestrator doesn't support the use of mandatory fields in child objects that the Create Change with Template activity creates. These template activities will fail in Service Manager if there are mandatory fields in any of the child objects it tries to create. This is because there is no way for the user to provide the mandatory properties for the associated activity.

The Create Change with Template activities create a change record by presenting the workflow author with a property grid of values associated with the change. This includes mandatory properties that will cause the create operation to be rejected by Service Manager if they aren't provided.

The configuration user interface for Create Change with Template doesn't provide a way to configure child work items. It can only access the parent change. Therefore, if any of the child work items contain mandatory properties, the creation of the change will be rejected by Service Manager.

The following published data elements are specific to Create Change with Template. Additional published data is generated based on the class that you select when you define the activity. For a list of the data elements published by each class, see [Service Manager Published Data](service-manager-published-data.md).

## Create Change with Template published data

| Element   | Description   |
|-------------------|----------------------------------------------------------------------------|
| Template ID   | The unique identifier of the template used to create the change   |
| Number of Objects | The number of objects returned by the Create Change with Template activity |
