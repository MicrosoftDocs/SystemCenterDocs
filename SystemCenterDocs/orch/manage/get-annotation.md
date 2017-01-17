---
title: Get Annotation
description: The Get Annotation activity retrieves annotations for a specified message according to filter criteria that you specify.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 60be0ba1-5e71-4521-bfae-9c7721fdfa03
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Get Annotation

Applies To: System Center 2016 - Orchestrator

The Get Annotation activity retrieves annotations for a specified message according to filter criteria that you specify. The activity uses filters to determine which annotations retrieved from the management server should be published.

The following tables list the required properties and published data for this activity. For more information on configuring activities, see [HP Operations Manager Activities](hp-operations-manager-activities.md).

## Get Annotation Required Properties

| Element   | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| Message ID | The ID of the message to get annotations for. | String   | No   |

## Get Annotation Filters

| Element   | Description   | Filters   | Value Type |
|:---|:---|:---|:---|
| Annotation ID   | Unique identifier for an annotation.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts With<br>Ends With | String   |
| Annotation Text | The annotation text.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts With<br>Ends With | String   |
| Author   | Name of the HPOM user that is currently responsible for the annotation. | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts With<br>Ends With | String   |
| Time Created   | The time that the annotations was created.   | Less than<br>Greater than   | Datetime   |

## Get Annotation Published Data

| Element   | Description   | Value Type |
|:---|:---|:---|
| Message ID   | The ID of the message that contains the annotation.   | String   |
| Annotation ID   | Unique identifier for an annotation.   | String   |
| Annotation Text  | The annotation text.   | String   |
| Author   | Name of the HPOM user that is currently responsible for the annotation.   | String   |
| Time Created   | The time that the annotation was created.   | Datetime   |
| Annotation Count | The number of annotations that were retrieved that satisfy the specified filter criteria. | Integer   |
| HPOM Host   | The name or IP address of the HPOM management server.   | String   |
| HPOM Port   | The port used to connect to the HPOM management server.   | Integer   |
| HPOM Username   | The name of the HPOM used to connect to the HPOM management server.   | String   |

## Other Activities

The Integration Pack for HP Operations Manager integration contains the following additional activities:

[Acknowledge Message](acknowledge-message.md)

[Add Annotation to Message](add-annotation-to-message.md)

[Create Message](create-message.md)

[Delete Annotation](delete-annotation.md)

[Delete Custom Attribute](delete-custom-attribute.md)

[Get Message](get-message.md)

[Launch Tool](launch-tool.md)

[Monitor Message](monitor-message.md)

[Own/Disown Message](own-or-disown-message.md)

[Set Custom Attribute](set-custom-attribute.md)

[Update Annotation](update-annotation.md)

[Update Message](update-message.md)
