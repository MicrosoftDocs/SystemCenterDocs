---
title: Own or Disown Message
description: The Own/Disown Message activity is used in a runbook to take ownership or remove ownership of a message.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e07b864-9bb3-4808-947a-1f05a1673dac
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Own or Disown Message

Applies To: System Center 2016 - Orchestrator

The Own/Disown Message activity is used in a runbook to take ownership or remove ownership of a message.

The following tables list the required properties and published data for this activity. For more information on configuring activities, see [HP Operations Manager Activities](../../orchestrator/hp-operations-manager-activities.md).

## Own/Disown Message Required Properties

| Element   | Description   | Valid Values  | Look up |
|:---|:---|:---|:---|
| Message ID   | The ID of the message to be owned or disowned.   | String   | No   |
| Ownership Status | Specifies whether the message should be owned or disowned. | Own<br>Disown | Yes   |

## Own/Disown Message Published Data

| Element   | Description   | Value Type |
|:---|:---|:---|
| Message ID   | The ID of the message that was owned or disowned.   | String   |
| Ownership Status | Specifies whether the message was owned or disowned.   | String   |
| HPOM Host   | The name or IP address of the HPOM management server.   | String   |
| HPOM Port   | The port used to connect to the HPOM management server.   | Integer   |
| HPOM Username   | The name of the HPOM used to connect to the HPOM management server. | String   |

>[!TIP]
>The Own/Disown Message activity will succeed when provided with a Message ID that does not match a Message stored in HP Operations Manager management server. 

## Other Activities

The Integration Pack for HP Operations Manager integration contains the following additional activities:

[Acknowledge Message](acknowledge-message.md)

[Add Annotation to Message](add-annotation-to-message.md)

[Create Message](create-message.md)

[Delete Annotation](delete-annotation.md)

[Delete Custom Attribute](delete-custom-attribute.md)

[Get Annotation](get-annotation.md)

[Get Message](get-message.md)

[Launch Tool](launch-tool.md)

[Monitor Message](monitor-message.md)

[Set Custom Attribute](set-custom-attribute.md)

[Update Annotation](update-annotation.md)

[Update Message](update-message.md)
