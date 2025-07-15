---
title: Update Entry
description: The Update Entry activity is used in a runbook to modify the existing entries in HP Service Manager.
ms.custom: UpdateFrequency3
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 65533371-d3ac-4960-bb88-50b6383fab83
author: jyothisuri
ms.author: jsuri
robots: noindex
monikerRange: '<=sc-orch-2019'
ms.date: 11/01/2024
ms.update-cycle: 1095-days
---
# Update Entry

The Update Entry activity is used in a runbook to modify the existing entries in HP Service Manager.

The following tables list the required properties and published data for this activity. For more information on configuring activities, see [HP Service Manager Activities](service-manager-activities.md).

## Update Entry Required Properties

| Element | Description   | Valid Values   | Look up   |
|:---|:---|:---|:---|
| Type   | The type of entry to be updated   | Change, Incident, ServiceDesk, Configuration   | Yes   |
| Subtype | The Subtype of the entry to be updated based on the Type selected.   | This is a dynamic property based on the configuration of the HP Service Manager server.   | Yes   |
| Fields  | A list of field values to be applied to the entry when it is updated. | This list is dynamically populated with the required fields for the selected Type and Subtype as configured on the HP Service Manager server. | A lookup will be provided for any applicable dynamic property. |

## Other Activities

The Integration Pack for HP Service Manager contains the following additional activities:

[Close Entry](close-entry.md)

[Create Entry](create-entry.md)

[Get Entry](get-entry.md)

[Monitor Entry](monitor-entry.md)
