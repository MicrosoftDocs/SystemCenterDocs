---
title: Set Custom Attribute
description: The Set Custom Attribute activity is used in a runbook to create or update a custom attribute for an existing message.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7655d0b0-8b28-495a-8431-e9962a6d5fcd
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Set Custom Attribute

Applies To: System Center 2016 - Orchestrator

The Set Custom Attribute activity is used in a runbook to create or update a custom attribute for an existing message.

The following tables list the required properties and published data for this activity. For more information on configuring activities, see [HP Operations Manager Activities](../../orchestrator/hp-operations-manager-activities.md).

## Set Custom Attribute Required Properties

| Element   | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| Message ID   | The ID of the message that contains the custom attribute.  | String   | No   |
| Attribute Name  | The name of the custom attribute to be created or updated. | String   | No   |
| Attribute Value | The value to assign to the custom attribute.   | String   | No   |

## Set Custom Attribute Published Data

| Element   | Description   | Value Type |
|:---|:---|:---|
| Message ID   | The ID of the message that contains the custom attribute.   | String   |
| Attribute Name  | The name of the custom attribute that was created or updated.   | String   |
| Attribute Value | The value that was assigned to the custom attribute.   | String   |
| HPOM Host   | The name or IP address of the HPOM management server.   | String   |
| HPOM Port   | The port used to connect to the HPOM management server.   | Integer   |
| HPOM Username   | The name of the HPOM used to connect to the HPOM management server. | String   |

## Other Activities

The Integration Pack for HP Operations Manager integration contains the following additional activities:

[Acknowledge Message](../../orchestrator/acknowledge-message.md)

[Add Annotation to Message](../../orchestrator/add-annotation-to-message.md)

[Create Message](../../orchestrator/create-message.md)

[Delete Annotation](../../orchestrator/delete-annotation.md)

[Delete Custom Attribute](../../orchestrator/delete-custom-attribute.md)

[Get Annotation](../../orchestrator/get-annotation.md)

[Get Message](get-message.md)

[Launch Tool](launch-tool.md)

[Monitor Message](monitor-message.md)

[Own/Disown Message](own-or-disown-message.md)

[Update Annotation](update-annotation.md)

[Update Message](update-message.md)
