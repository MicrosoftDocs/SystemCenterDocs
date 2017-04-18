---
title: Update Annotation
description: The Update Annotation activity is used in a runbook to update an annotation to an existing message.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5966113a-fea5-46b9-a510-e57745f92737
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Update Annotation

Applies To: System Center 2016 - Orchestrator

The Update Annotation activity is used in a runbook to update an annotation to an existing message.

The following tables list the required properties and published data for this activity. For more information on configuring activities, see [HP Operations Manager Activities](../../orchestrator/hp-operations-manager-activities.md).

## Update Annotation Required Properties

| Element   | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| Message ID   | The ID of the message that contains the annotation to update. | String   | No   |
| Annotation ID   | The ID of the annotation to be updated.   | String   | No   |
| Annotation Text | The updated text for the annotation.   | String   | No   |

## Update Annotation Published Data

| Element   | Description   | Value Type |
|:---|:---|:---|
| Message ID   | The ID of the message that contains the annotation that was updated. | String   |
| Annotation ID   | The ID of the annotation that was updated.   | String   |
| Annotation Text | The updated text for the annotation.   | String   |
| HPOM Host   | The name or IP address of the HPOM management server.   | String   |
| HPOM Port   | The port used to connect to the HPOM management server.   | Integer   |
| HPOM Username   | The name of the HPOM used to connect to the HPOM management server.  | String   |

>[!TIP]
>The Update Annotation activity will succeed when provided with a **Message ID** that does not match a Message stored on the HP Operations Manager management server. 

## Other Activities

The Integration Pack for HP Operations Manager integration contains the following additional activities:

[Acknowledge Message](../../orchestrator/acknowledge-message.md)

[Add Annotation to Message](../../orchestrator/add-annotation-to-message.md)

[Create Message](../../orchestrator/create-message.md)

[Delete Annotation](../../orchestrator/delete-annotation.md)

[Delete Custom Attribute](../../orchestrator/delete-custom-attribute.md)

[Get Annotation](get-annotation.md)

[Get Message](get-message.md)

[Launch Tool](launch-tool.md)

[Monitor Message](monitor-message.md)

[Own/Disown Message](own-or-disown-message.md)

[Set Custom Attribute](set-custom-attribute.md)

[Update Message](update-message.md)
