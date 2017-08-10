---
title: Monitor Message
description: The Monitor Message activity invokes a runbook when certain HP Operations Manager messages are created, updated, acknowledged or unacknowledged according to filter criteria that you specify.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: f8343797-0f78-43ab-a5a5-742233cefa46
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Monitor Message

> Applies To: System Center 2016 - Orchestrator

The Monitor Message activity invokes a runbook when certain HP Operations Manager messages are created, updated, acknowledged or unacknowledged according to filter criteria that you specify. The activity uses filters to determine which messages should invoke the runbook.

The following tables list the required properties and published data for this activity. For more information on configuring activities, see [HP Operations Manager Activities](operations-manager-activities.md).

## Monitor Message required properties

| Element   | Description   | Value Type   |
|:---|:---|:---|
| Monitor New Messages   | The runbook will be invoked if the monitor detects a new message   | True<br>False |
| Monitor Modified Messages   | The runbook will be invoked if the monitor detects a modified message.   | True<br>False |
| Monitor Acknowledged Messages   | The runbook will be invoked if the monitor detects a message that was acknowledged   | True<br>False |
| Monitor UnAcknowledged Messages | The runbook will be invoked if the monitor detects a message that was unacknowledged | True<br>False |

## Monitor Message filters

| Element   | Description   | Filters   | Value Type   |
|:---|:---|:---|:---|
| Message ID   | Unique identifier for a message.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with | String   |
| Description   | Detailed description of the message.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with | String   |
| Message Text   | Brief description of the event that the message relates to.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with | String   |
| Severity   | Severity of the event that the message relates to.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with | Normal<br>Warning<br>Minor<br>Major<br>Critical |
| Solution   | Description of the steps taken in response to the message.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with | String   |
| Message Group   | String used for categorizing messages. Messages that have some logical connection have the same Message Group.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with | String   |
| Subcategory   | String used for more detailed organization of messages that have the same Message Group.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with | String   |
| Product Type   | String that may be used for integration with a service management product. The service management product defines the string's value and purpose. | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with | String   |
| Problem Type   | String that may be used for integration with a service management product. The service management product defines the string's value and purpose. | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with | String   |
| Collaboration Mode   | String that may be used for integration with a service management product. The service management product defines the string's value and purpose. | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with | String   |
| Service Name   | The name of the service that the message relates to. The severity a message can affect the status of a service that it relates to.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with | String   |
| Node   | Name of the node generating the message.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with | String   |
| Owner   | Name of the HPOM user that is currently responsible for the message.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with | String   |
| Message Type   | String used for organizing messages.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with | String   |
| Application   | Name of the application to which the message relates.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with | String   |
| Object   | Name of the object to which the message relates.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with | String   |
| Time Owned or Acknowledged | The time at which the message was owned or acknowledged. The service maps whichever time is later.   | Is less than<br>Is greater than   | Datetime   |
| Time Created   | The time at which the agent created the message.   | Is less than<br>Is greater than   | Datetime   |
| Time Received   | The time at which the management server received the message.   | Is less than<br>Is greater than   | Datetime   |
| Number of Duplicates   | Number of duplicates that the management server had detected for the message.   | Equals<br>Does not equal<br>Is less than<br>Is less than or equal to<br>Is greater than<br>Is greater than or equal to   | Integer   |
| Message Key   | String that enables other processes to identify messages that relate to each other.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with | String   |
| Matched   | Indicates whether the message was sent to the server because of a matched condition in a policy or template.   | Equals<br>Does not equal   | Boolean   |
| Automatic Action Status   | Status of the automatic action, if one is associated with the message.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with | String   |
| Operator Action Status   | Status of the operator-initiated action, if one is associated with the message.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with | String   |
| Escalation   | Defines the escalation status of the message, if the message was escalated by this management server, or to a different management server.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with | String   |
| Original Message   | Details of the event that is the cause of this message.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with | String   |
| Custom Attributes   | An XML representation of the custom message attributes associated with the message.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with | String   |
| Number of Annotations   | Number of annotations that have been added to the message.   | Equals<br>Does not equal<br>Is less than<br>Is less than or equal to<br>Is greater than<br>Is greater than or equal to   | Integer   |
| Source   | Contains the name and version of the template that created the message.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with | String   |

## Monitor Message published data

| Element   | Description   | Value Type |
|:---|:---|:---|
| Application   | Name of the application to which the message relates.   | String   |
| Automatic Action Status   | Status of the automatic action, if one is associated with the message.   | String   |
| Collaboration Mode   | String that may be used for integration with a service management product. The service management product defines the string's value and purpose. | String   |
| Custom Attributes   | An XML representation of the custom message attributes associated with the message.   | String   |
| Description   | Detailed description of the message.   | String   |
| Escalation   | Defines the escalation status of the message, if the message was escalated by this management server, or to a different management server.   | String   |
| HPOM Host   | The name or IP address of the HPOM management server.   | String   |
| HPOM Port   | The port used to connect to the HPOM management server.   | Integer   |
| HPOM Username   | The name of the HPOM used to connect to the HPOM management server.   | String   |
| Matched   | Indicates whether the message was sent to the server because of a matched condition in a policy or template.   | String   |
| Message Count   | The number of messages that triggered the runbook.   | Integer   |
| Message Group   | String used for categorizing messages. Messages that have some logical connection have the same Message Group.   | String   |
| Message ID   | Unique identifier for a message.   | String   |
| Message Key   | String that enables other processes to identify messages that relate to each other.   | String   |
| Message Text   | Brief description of the event that the message relates to.   | String   |
| Message Type   | String used for organizing messages.   | String   |
| Monitor Acknowledged Messages   | The runbook will be invoked if the monitor detects a message than that was acknowledged.   | Boolean   |
| Monitor Modified Messages   | The runbook will be invoked if the monitor detects a modified message.   | Boolean   |
| Monitor New Messages   | The runbook will be invoked if the monitor detects a new message.   | Boolean   |
| Monitor UnAcknowledged Messages | The runbook will be invoked if the monitor detects a message that was unacknowledged.   | Boolean   |
| Node   | Name of the node generating the message.   | String   |
| Number of Annotations   | Number of annotations that have been added to the message.   | Integer   |
| Number of Duplicates   | Number of duplicates that the management server had detected for the message.   | Integer   |
| Object   | Name of the object to which the message relates.   | String   |
| Operator Action Status   | Status of the operator-initiated action, if one is associated with the message.   | String   |
| Original Message   | Details of the event that is the cause of this message.   | String   |
| Owner   | Name of the HPOM user that is currently responsible for the message.   | String   |
| Problem Type   | String that may be used for integration with a service management product. The service management product defines the string's value and purpose. | String   |
| Product Type   | String that may be used for integration with a service management product. The service management product defines the string's value and purpose. | String   |
| Service Name   | The name of the service that the message relates to. The severity a message can affect the status of a service that it relates to.   | String   |
| Severity   | Severity of the event that the message relates to.   | String   |
| Solution   | Description of the steps taken in response to the message.   | String   |
| Source   | The name and version of the template that created the message.   | String   |
| Subcategory   | String used for more detailed organization of messages that have the same Message Group.   | String   |
| Time Created   | The time at which the agent created the message.   | Datetime   |
| Time Owned or Acknowledged   | The time at which the message was owned or acknowledged. The service maps whichever time is later.   | Datetime   |
| Time Received   | The time at which the management server received the message.   | Datetime   |

>[!TIP]
>When editing filters for numeric fields, the **Filter Settings** dialog may change the **Is less than** and **Is greater than** relations to **Is less than or equal to** and **Is greater than or equal to**. To avoid inadvertently modifying the filter, click **Cancel** to dismiss the Filter Settings dialog without committing the change.

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
- [Own/Disown Message](own-or-disown-message.md)
- [Set Custom Attribute](set-custom-attribute.md)
- [Update Annotation](update-annotation.md)
- [Update Message](update-message.md)
