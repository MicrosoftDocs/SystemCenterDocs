---
title: Get Entry
description: The Get Entry activity is used in a runbook to retrieve existing entries from HP Service Manager.
ms.custom: na
ms.date: 4/25/2017
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 8a13614b-bc3a-41dc-9620-2152c7268fe7
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
---

# Get Entry

Applies To: System Center 2016 - Orchestrator

The Get Entry activity is used in a runbook to retrieve existing entries from HP Service Manager.

The following tables list the required properties and published data for this activity. For more information on configuring activities, see [HP Service Manager Activities](service-manager-activities.md).

## Get Entry Required Properties

| Element | Description   | Valid Values   | Look up |
|:---|:---|:---|:---|
| Type   | The type of entry to be created   | Change, Incident, Configuration, ServiceDesk   | Yes   |
| Subtype | The Subtype of the entry to be closed based on the Type selected. | This is a dynamic property based on the configuration of the HP Service Manager server. | Yes   |

## Other Activities

The Integration Pack for HP Service Manager contains the following additional activities:

[Close Entry](close-entry.md)
[Create Entry](create-entry.md)
[Monitor Entry](monitor-entry.md)
[Update Entry](update-entry.md)
