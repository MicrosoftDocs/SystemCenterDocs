---
title: Add Annotation to Message
description: The Add Annotation to Message activity is used in a runbook to add an annotation to an existing message.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 81d9905b-685d-4fc8-9da2-9b742bded6ef
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Add Annotation to Message

Applies To: System Center 2016 - Orchestrator

The Add Annotation to Message activity is used in a runbook to add an annotation to an existing message.

The following tables list the required properties and published data for this activity. For more information on configuring activities, see [HP Operations Manager Activities](operations-manager-activities.md).

## Add Annotation to Message Required Properties

| Element   | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| Message ID   | The ID of the message to add the annotation to. | String   | No   |
| Annotation Text | The text of the annotation to add.   | String   | No   |

## Add Annotation to Message Published Data

| Element   | Description   | Value Type |
|:---|:---|:---|
| Message ID   | The ID of the message that the annotation was added to.   | String   |
| Annotation ID   | The ID that HPOM generated for the annotation.   | String   |
| Annotation Text | The text of the annotation.   | String   |
| HPOM Host   | The name or IP address of the HPOM management server.   | String   |
| HPOM Port   | The port used to connect to the HPOM management server.   | Integer   |
| HPOM Username   | The name of the HPOM used to connect to the HPOM management server. | String   |

>[!TIP]
>When used in conjunction with the Create Message activity care must be taken to ensure that the Message ID is associated with an original message. Using the Message ID of a duplicate message that has been correlated by HP Operations Manager will cause the Add Annotation to Message activity to fail.

## Other Activities

The Integration Pack for HP Operations Manager integration contains the following additional activities:

[Acknowledge Message](acknowledge-message.md)

[Create Message](create-message.md)

[Delete Annotation](delete-annotation.md)

[Delete Custom Attribute](delete-custom-attribute.md)

[Get Annotation](get-annotation.md)

[Get Message](get-message.md)

[Launch Tool](launch-tool.md)

[Monitor Message](monitor-message.md)

[Own/Disown Message](own-or-disown-message.md)

[Set Custom Attribute](set-custom-attribute.md)

[Update Annotation](update-annotation.md)

[Update Message](update-message.md)
