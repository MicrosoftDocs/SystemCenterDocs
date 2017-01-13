---
title: Update Object
description: The Update Object activity is used to change the values of one or more properties of an existing object.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8aacf84b-0606-4bf7-b094-865108bbfae7
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Update Object

Applies To: System Center 2016 - Orchestrator

The Update Object activity is used to change the values of one or more properties of an existing object.

The following published data element is specific to Update Object activity. Additional published data is generated based on the class that you select when you define the activity. For a list of the data elements published by each class, see [Service Manager Published Data](service-manager-published-data.md).

<br><br><strong>Note </strong><br>To resolve an incident, if you don't set the **Resolved Date**, the incident SLAs that use the **Resolved Date** will keep running and expire. Ensure that you set the **Resolved Date** when you resolve an incident.<br><br>

## Update Object Published Data

|   |   |
|---------------------------|-----------------------------------------------------------------|
| Element   | Description   |
| System Center Object GUID | The unique identifier (GUID) of the single object to be updated |
