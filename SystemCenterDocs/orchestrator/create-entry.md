---
title: Create Entry
description: The Create Entry activity is used in a runbook to create new incident, service desk request or change request entries in HP Service Manager.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 63632ffe-5b0d-476a-971f-952b616d7a38
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Create Entry

Applies To: System Center 2016 - Orchestrator

The Create Entry activity is used in a runbook to create new incident, service desk request or change request entries in HP Service Manager.

The following tables list the required properties and published data for this activity. For more information on configuring activities, see [HP Service Manager Activities](../orch/manage/service-manager-activities.md).

## Create Entry Required Properties

| Element | Description   | Valid Values   | Look up   |
|:---|:---|:---|:---|
| Type   | The type of entry to be created   | Configuration, Change, Incident, ServiceDesk   | Yes   |
| Subtype | The Subtype of the entry to be closed based on the Type selected.   | This is a dynamic property based on the configuration of the HP Service Manager server.   | Yes   |
| Fields  | A list of field values to be applied to the entry when it is created. | This list is dynamically populated with the required fields for the selected Type and Subtype as configured on the HP Service Manager server. | A lookup will be provided for any applicable dynamic property. |

## Other Activities

The Integration Pack for HP Service Manager contains the following additional activities:

[Close Entry](close-entry.md)

[Get Entry](get-entry.md)

[Monitor Entry](monitor-entry.md)

[Update Entry](../orch/manage/update-entry.md)
