---
title: Close Entry
description: The Close Entry activity is used in a runbook to close existing entries in HP Service Manager.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fe2b849f-269d-4fa7-b1b4-b9691613173e
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Close Entry

Applies To: System Center 2016 - Orchestrator

The Close Entry activity is used in a runbook to close existing entries in HP Service Manager.

The following tables list the required properties and published data for this activity. For more information on configuring activities, see [HP Service Manager Activities](../orch/manage/service-manager-activities.md).

## Close Entry Required Properties

| Element | Description   | Valid Values   | Look up   |
|:---|:---|:---|:---|
| Type   | The type of entry to be closed   | Change, Incident, ServiceDesk   | Yes   |
| Subtype | The Subtype of the entry to be closed based on the Type selected.   | This is a dynamic property based on the configuration of the HP Service Manager server.   | Yes   |
| Fields  | A list of field values to be applied to the entry when it is closed. | This list is dynamically populated with the required fields for the selected Type and Subtype as configured on the HP Service Manager server. | A lookup will be provided for any applicable dynamic property. |

## Other Activities

The Integration Pack for HP Service Manager contains the following additional activities:

[Create Entry](../orch/manage/create-entry.md)

[Get Entry](../orch/manage/get-entry.md)

[Monitor Entry](../orch/manage/monitor-entry.md)

[Update Entry](../orch/manage/update-entry.md)

