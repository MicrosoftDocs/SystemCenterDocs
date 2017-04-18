---
title: Update Message
description: The Update Message activity is used in a runbook to update an existing message.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ba06a70c-1b93-4588-9ef7-15ae6ba47dbd
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Update Message

Applies To: System Center 2016 - Orchestrator

The Update Message activity is used in a runbook to update an existing message.

The following tables list the required properties and published data for this activity. For more information on configuring activities, see [HP Operations Manager Activities](../../orchestrator/hp-operations-manager-activities.md).

## Update Message Required Properties

| Element   | Description   | Valid Values   | Look up |
|:---|:---|:---|:---|
| Message ID   | The ID of the message that contains the annotation to update. | String   | No   |
| Severity   | Severity of the event that the message relates to.   | Normal<br>Warning<br>Minor<br>Major<br>Critical | Yes   |
| Message Text | Brief description of the event that this message relates to.  | String   | No   |

## Update Message Published Data

| Element   | Description   | Value Type |
|:---|:---|:---|
| Message ID   | Unique identifier for a message.   | String   |
| Description   | Detailed description of the message.   | String   |
| Message Text   | Brief description of the event that the message relates to.   | String   |
| Severity   | Severity of the event that the message relates to.   | String   |
| Solution   | Description of the steps taken in response to the message.   | String   |
| Message Group   | String used for categorizing messages. Messages that have some logical connection have the same Message Group.   | String   |
| Subcategory   | String used for more detailed organization of messages that have the same Message Group.   | String   |
| Product Type   | String that may be used for integration with a service management product. The service management product defines the string's value and purpose. | String   |
| Problem Type   | String that may be used for integration with a service management product. The service management product defines the string's value and purpose. | String   |
| Collaboration Mode   | String that may be used for integration with a service management product. The service management product defines the string's value and purpose. | String   |
| Service Name   | The name of the service that the message relates to. The severity a message can affect the status of a service that it relates to.   | String   |
| Node   | Name of the node generating the message.   | String   |
| Owner   | Name of the HPOM user that is currently responsible for the message.   | String   |
| Message Type   | String used for organizing messages.   | String   |
| Application   | Name of the application to which the message relates.   | String   |
| Object   | Name of the object to which the message relates.   | String   |
| Time Owned or Acknowledged | The time at which the message was owned or acknowledged. The service maps whichever time is later.   | Datetime   |
| Time Created   | The time at which the agent created the message.   | Datetime   |
| Time Received   | The time at which the management server received the message.   | Datetime   |
| Number of Duplicates   | Number of duplicates that the management server had detected for the message.   | Integer   |
| Message Key   | String that enables other processes to identify messages that relate to each other.   | String   |
| Matched   | Indicates whether the message was sent to the server because of a matched condition in a policy or template.   | String   |
| Automatic Action Status   | Status of the automatic action, if one is associated with the message.   | String   |
| Operator Action Status   | Status of the operator-initiated action, if one is associated with the message.   | String   |
| Escalation   | Defines the escalation status of the message, if the message was escalated by this management server, or to a different management server.   | String   |
| Original Message   | Details of the event that is the cause of this message.   | String   |
| Custom Attributes   | An XML representation of the custom message attributes associated with the message.   | String   |
| Number of Annotations   | Number of annotations that have been added to the message.   | Integer   |
| Source   | Contains the name and version of the template that created the message.   | String   |
| HPOM Host   | The name or IP address of the HPOM management server.   | String   |
| HPOM Port   | The port used to connect to the HPOM management server.   | Integer   |
| HPOM Username   | The name of the HPOM used to connect to the HPOM management server.   | String   |

## Other Activities

The Integration Pack for HP Operations Manager integration contains the following additional activities:

[Acknowledge Message](../../orchestrator/acknowledge-message.md)

[Add Annotation to Message](../../orchestrator/add-annotation-to-message.md)

[Create Message](../../orchestrator/create-message.md)

[Delete Annotation](../../orchestrator/delete-annotation.md)

[Delete Custom Attribute](delete-custom-attribute.md)

[Get Annotation](get-annotation.md)

[Get Message](get-message.md)

[Launch Tool](launch-tool.md)

[Monitor Message](monitor-message.md)

[Own/Disown Message](own-or-disown-message.md)

[Set Custom Attribute](set-custom-attribute.md)

[Update Annotation](update-annotation.md)
