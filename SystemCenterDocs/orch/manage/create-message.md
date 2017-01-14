---
title: Create Message
description: The Create Message activity is used in a runbook to store a new message on the management server.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2d32a3a-f9ee-4ff4-8a4b-6a32b1f01f4a
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Create Message

Applies To: System Center 2016 - Orchestrator

The Create Message activity is used in a runbook to store a new message on the management server.

The following tables list the required and optional properties and published data for this activity. For more information on configuring activities, see [HP Operations Manager Activities](hp-operations-manager-activities.md).

## Create Message Required Properties

| Element   | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| Message Text | Brief description of the event that the message relates to. | String   | No   |
| Node   | Name of the node generating the message.   | String   | No   |

## Create Message Optional Properties

| Element   | Description   | Valid Values   | Look up |
|:---|:---|:---|:---|
| Description   | Detailed description of the message.   | String   | No   |
| Severity   | Severity of the event that the message relates to.   | Normal<br>Warning<br>Minor<br>Major<br>Critical | Yes   |
| Solution   | Description of the steps taken in response to the message.   | String   | No   |
| Message Group   | String used for categorizing messages. Messages that have some logical connection have the same Message Group.   | String   | No   |
| Subcategory   | String used for more detailed organization of messages that have the same Message Group.   | String   | No   |
| Product Type   | String that may be used for integration with a service management product. The service management product defines the string's value and purpose. | String   | No   |
| Problem Type   | String that may be used for integration with a service management product. The service management product defines the string's value and purpose. | String   | No   |
| Collaboration Mode | String that may be used for integration with a service management product. The service management product defines the string's value and purpose. | fyi<br>peer<br>incident\_exchange   | Yes   |
| Service Name   | The name of the service that the message relates to. The severity a message can affect the status of a service that it relates to.   | String   | No   |
| Message Type   | String used for organizing messages.   | String   | No   |
| Application   | Name of the application to which the message relates.   | String   | No   |
| Object   | Name of the object to which the message relates.   | String   | No   |
| Time Created   | The time at which the agent created the message.   | Datetime   | Yes   |
| Message Key   | String that enables other processes to identify messages that relate to each other.   | String   | No   |

## Create Message Published Data

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
| Collaboration Mode | String that may be used for integration with a service management product. The service management product defines the string's value and purpose. | String   |
| Service Name   | The name of the service that the message relates to. The severity a message can affect the status of a service that it relates to.   | String   |
| Node   | Name of the node generating the message.   | String   |
| Message Type   | String used for organizing messages.   | String   |
| Application   | Name of the application to which the message relates.   | String   |
| Object   | Name of the object to which the message relates.   | String   |
| Time Created   | The time at which the agent created the message.   | Datetime   |
| Message Key   | String that enables other processes to identify messages that relate to each other.   | String   |
| HPOM Host   | The name or IP address of the HPOM management server.   | String   |
| HPOM Port   | The port used to connect to the HPOM management server.   | Integer   |
| HPOM Username   | The name of the HPOM used to connect to the HPOM management server.   | String   |

>[!WARNING]
>The **Message ID** that is published by the **Create Message** activity might not be valid in those cases where HP Operations Manager performs correlation. Therefore, caution must be taken to ensure that the **Message ID** published from the **Create Message** activity is only used in Runbooks where you are confident that the new message is not a duplicate of an existing message.

>[!WARNING]
>The **Create Message** activity will succeed and publish an invalid Message ID when provided with an invalid **Node**.

## Other Activities

The Integration Pack for HP Operations Manager integration contains the following additional activities:

[Acknowledge Message](acknowledge-message.md)

[Add Annotation to Message](add-annotation-to-message.md)

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
