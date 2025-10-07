---
title: Update Object
description: The Update Object activity is used to change the values of one or more properties of an existing object.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 8aacf84b-0606-4bf7-b094-865108bbfae7
author: Jeronika-MS
ms.author: v-gajeronika
---
# Update Object

The Update Object activity is used to change the values of one or more properties of an existing object.

The following published data element is specific to Update Object activity. Additional published data is generated based on the class that you select when you define the activity. For a list of data elements published by each class, see [Service Manager Published Data](service-manager-published-data.md).

>[!NOTE]
>To resolve an incident, if you don't set the **Resolved Date**, the incident SLAs that use the **Resolved Date** will keep running and expire. Ensure that you set the **Resolved Date** when you resolve an incident.

## Update Object Published Data

| Element   | Description   |
|---------------------------|-----------------------------------------------------------------|
| System Center Object GUID | The unique identifier (GUID) of the single object to be updated |
