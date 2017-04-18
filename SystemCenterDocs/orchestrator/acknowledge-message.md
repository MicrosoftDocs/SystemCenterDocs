---
title: Acknowledge Message
description: The Acknowledge Message activity is used in a runbook to acknowledge or un-acknowledge a message.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c8d06fea-db19-494a-9f40-0b480d2af7c5
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Acknowledge Message

Applies To: System Center 2016 - Orchestrator

The Acknowledge Message activity is used in a runbook to acknowledge or un-acknowledge a message.

The following tables list the required properties and published data for this activity. For more information on configuring activities, see [HP Operations Manager Activities](hp-operations-manager-activities.md).

## Acknowledge Message Required Properties

| Element   | Description   | Valid Values   | Look up |
|:---|:---|:---|:---|
| Message ID   | The ID of the message to be acknowledged or unacknowledged.   | String   | No   |
| Acknowledge Status | Specifies whether the message should be acknowledged or unacknowledged. | Acknowledge<br>UnAcknowledge | Yes   |

## Acknowledge Message Published Data

| Element   | Description   | Value Type |
|:---|:---|:---|
| Message ID   | The ID of the message that was acknowledged or unacknowledged   | String   |
| Acknowledge Status | Specifies whether the message was acknowledged or unacknowledged   | String   |
| HPOM Host   | The name or IP address of the HPOM management server.   | String   |
| HPOM Port   | The port used to connect to the HPOM management server.   | Integer   |
| HPOM Username   | The name of the HPOM used to connect to the HPOM management server. | String   |

## Other Activities

The Integration Pack for HP Operations Manager integration contains the following additional activities:

[Add Annotation to Message](add-annotation-to-message.md)

[Create Message](create-message.md)

[Delete Annotation](../orch/manage/delete-annotation.md)

[Delete Custom Attribute](../orch/manage/delete-custom-attribute.md)

[Get Annotation](../orch/manage/get-annotation.md)

[Get Message](../orch/manage/get-message.md)

[Launch Tool](../orch/manage/launch-tool.md)

[Monitor Message](../orch/manage/monitor-message.md)

[Own/Disown Message](../orch/manage/own-or-disown-message.md)

[Set Custom Attribute](../orch/manage/set-custom-attribute.md)

[Update Annotation](../orch/manage/update-annotation.md)

[Update Message](../orch/manage/update-message.md)
