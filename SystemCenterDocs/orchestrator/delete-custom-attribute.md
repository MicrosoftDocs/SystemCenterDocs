---
title: Delete Custom Attribute
description: The Delete Custom Attribute activity is used in a runbook to delete a custom attribute from an existing message.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a33075ab-042d-4efa-81b6-1efa8f8fa578
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Delete Custom Attribute

Applies To: System Center 2016 - Orchestrator

The Delete Custom Attribute activity is used in a runbook to delete a custom attribute from an existing message.

The following tables list the required properties and published data for this activity. For more information on configuring activities, see [HP Operations Manager Activities](operations-manager-activities.md).

## Delete Custom Attribute Required Properties

| Element   | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| Message ID   | The ID of the message that contains the custom attribute. | String   | No   |
| Attribute Name | The name of the custom attribute to be deleted   | String   | No   |

## Delete Custom Attribute Published Data

| Element   | Description   | Value Type |
|:---|:---|:---|
| Message ID   | The ID of the message that contains the custom attribute.   | String   |
| Attribute Name | The name of the custom attribute that was deleted.   | String   |
| HPOM Host   | The name or IP address of the HPOM management server.   | String   |
| HPOM Port   | The port used to connect to the HPOM management server.   | Integer   |
| HPOM Username  | The name of the HPOM used to connect to the HPOM management server. | String   |

## Other Activities

The Integration Pack for HP Operations Manager integration contains the following additional activities:

[Acknowledge Message](acknowledge-message.md)

[Add Annotation to Message](add-annotation-to-message.md)

[Create Message](create-message.md)

[Delete Annotation](delete-annotation.md)

[Get Annotation](get-annotation.md)

[Get Message](get-message.md)

[Launch Tool](launch-tool.md)

[Monitor Message](monitor-message.md)

[Own/Disown Message](own-or-disown-message.md)

[Set Custom Attribute](set-custom-attribute.md)

[Update Annotation](update-annotation.md)

[Update Message](update-message.md)
