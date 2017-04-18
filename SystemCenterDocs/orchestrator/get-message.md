---
title: Get Message
description: The Get Message activity retrieves message from a management server according to filter criteria that you specify.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cd78c430-e320-44f8-b6ae-2b55c4e42ff6
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Get Message

Applies To: System Center 2016 - Orchestrator

The Get Message activity retrieves message from a management server according to filter criteria that you specify. The activity uses filters to determine which messages retrieved from the management server should be published.

The following tables list the required properties and published data for this activity. For more information on configuring activities, see [HP Operations Manager Activities](hp-operations-manager-activities.md).

## Get Message Filters

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
| Collaboration Mode   | String that may be used for integration with a service management product. The service management product defines the string's value and purpose. | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with | fyi<br>peer<br>incident\_exchange   |
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
| Source   | Contains the name and version of the template that created the message.   | Equals<br>Does not equa<br>lContains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with | String   |

## Get Message Published Data

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
| Message Count   | The number of messages that were retrieved from the HPOM management server that satisfy the specified filter criteria.   | Integer   |
| HPOM Host   | The name or IP address of the HPOM management server.   | String   |
| HPOM Port   | The port used to connect to the HPOM management server.   | Integer   |
| HPOM Username   | The name of the HPOM used to connect to the HPOM management server.   | String   |

>[!TIP]
>The **Get Message** activity can only retrieve Active messages from the HP Operations Manager management server.

>[!TIP]
>The maximum number of Messages that can be returned by the Get Message activity is determined by the HP Operations Manager Web Service **MaxItemsMaximum** configuration parameter. The **MaxItemsMaximum** configuration parameter has a default value of 500, however this can be increased up to 5,000 as directed in the HP Operations Manager Web Services Integration Manager documentation.

>[!TIP]
>When editing filters for numeric fields, the **Filter Settings** dialog may change the **Is less than** and **Is greater than** relations to **Is less than or equal to** and **Is greater than or equal to**. To avoid inadvertently modifying the filter, click **Cancel** to dismiss the Filter Settings dialog without committing the change.

## Other Activities

The Integration Pack for HP Operations Manager integration contains the following additional activities:

[Acknowledge Message](acknowledge-message.md)

[Add Annotation to Message](add-annotation-to-message.md)

[Create Message](create-message.md)

[Delete Annotation](delete-annotation.md)

[Delete Custom Attribute](delete-custom-attribute.md)

[Get Annotation](get-annotation.md)

[Launch Tool](../orch/manage/launch-tool.md)

[Monitor Message](../orch/manage/monitor-message.md)

[Own/Disown Message](../orch/manage/own-or-disown-message.md)

[Set Custom Attribute](../orch/manage/set-custom-attribute.md)

[Update Annotation](../orch/manage/update-annotation.md)

[Update Message](../orch/manage/update-message.md)
