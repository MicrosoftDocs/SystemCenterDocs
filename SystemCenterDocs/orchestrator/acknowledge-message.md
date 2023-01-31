---
title: Acknowledge Message
description: The Acknowledge Message activity is used in a runbook to acknowledge or unacknowledge a message.
author: jyothisuri
manager: mkluck
ms.date: 01/17/2018
ms.prod: system-center
ms.technology: orchestrator
ms.topic: reference
ms.author: jsuri
---


# Acknowledge Message

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end


The Acknowledge Message activity is used in a runbook to acknowledge or unacknowledge a message.

The following tables list the required properties and published data for this activity. For more information on configuring activities, see [HP Operations Manager Activities](operations-manager-activities.md).

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

- [Add Annotation to Message](add-annotation-to-message.md)

- [Create Message](create-message.md)

- [Delete Annotation](delete-annotation.md)

- [Delete Custom Attribute](delete-custom-attribute.md)

- [Get Annotation](get-annotation.md)

- [Get Message](get-message.md)

- [Launch Tool](launch-tool.md)

- [Monitor Message](monitor-message.md)

- [Own/Disown Message](own-or-disown-message.md)

- [Set Custom Attribute](set-custom-attribute.md)

- [Update Annotation](update-annotation.md)

- [Update Message](update-message.md)
