---
title: Get Entry
description: The Get Entry activity is used in a runbook to retrieve the existing entries from HP Service Manager.
ms.custom: UpdateFrequency3, engagement-fy24
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8a13614b-bc3a-41dc-9620-2152c7268fe7
author: jyothisuri
ms.author: jsuri
monikerRange: '<=sc-orch-2019'
ms.date: 11/01/2024
---

# Get Entry

The Get Entry activity is used in a runbook to retrieve the existing entries from HP Service Manager.

The following tables list the required properties and published data for this activity. For more information on configuring activities, see [HP Service Manager Activities](service-manager-activities.md).

## Get Entry Required Properties

| Element | Description   | Valid Values   | Look up |
|:---|:---|:---|:---|
| Type   | The type of entry to be created.  | Change, Incident, Configuration, ServiceDesk   | Yes   |
| Subtype | The Subtype of the entry to be closed based on the Type selected. | This is a dynamic property based on the configuration of the HP Service Manager server. | Yes   |

## Other Activities

The Integration Pack for HP Service Manager contains the following additional activities:

- [Close Entry](close-entry.md)
- [Create Entry](create-entry.md)
- [Monitor Entry](monitor-entry.md)
- [Update Entry](update-entry.md)
