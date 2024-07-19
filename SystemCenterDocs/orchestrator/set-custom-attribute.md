---
title: Set Custom Attribute
description: The Set Custom Attribute activity is used in a runbook to create or update a custom attribute for an existing message.
ms.custom: UpdateFrequency3
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7655d0b0-8b28-495a-8431-e9962a6d5fcd
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
robots: noindex
monikerRange: '<=sc-orch-2019'
ms.date: 04/27/2023
---
# Set Custom Attribute

The Set Custom Attribute activity is used in a runbook to create or update a custom attribute for an existing message.

The following tables list the required properties and published data for this activity. For more information on configuring activities, see [HP Operations Manager Activities](operations-manager-activities.md).

## Set Custom Attribute required properties

| Element   | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| Message ID   | The ID of the message that contains the custom attribute.  | String   | No   |
| Attribute Name  | The name of the custom attribute to be created or updated. | String   | No   |
| Attribute Value | The value to assign to the custom attribute.   | String   | No   |

## Set Custom Attribute published data

| Element   | Description   | Value Type |
|:---|:---|:---|
| Message ID   | The ID of the message that contains the custom attribute.   | String   |
| Attribute Name  | The name of the custom attribute that was created or updated.   | String   |
| Attribute Value | The value that was assigned to the custom attribute.   | String   |
| HPOM Host   | The name or IP address of the HPOM management server.   | String   |
| HPOM Port   | The port used to connect to the HPOM management server.   | Integer   |
| HPOM Username   | The name of the HPOM used to connect to the HPOM management server. | String   |

## Other activities

The Integration Pack for HP Operations Manager integration contains the following additional activities:

- [Acknowledge Message](acknowledge-message.md)
- [Add Annotation to Message](add-annotation-to-message.md)
- [Create Message](create-message.md)
- [Delete Annotation](delete-annotation.md)
- [Delete Custom Attribute](delete-custom-attribute.md)
- [Get Annotation](get-annotation.md)
- [Get Message](get-message.md)
- [Launch Tool](launch-tool.md)
- [Monitor Message](monitor-message.md)
- [Own/Disown Message](own-or-disown-message.md)
- [Update Annotation](update-annotation.md)
- [Update Message](update-message.md)
