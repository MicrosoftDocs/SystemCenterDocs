---
title: Delete Annotation
description: The Delete Annotation activity is used in a runbook to delete an annotation from an existing message.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3517e6a7-9b62-4b72-854a-ec39e4969f47
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
Delete Annotation
=================

Applies To: System Center 2016 - Orchestrator

The Delete Annotation activity is used in a runbook to delete an annotation from an existing message.

The following tables list the required properties and published data for this activity. For more information on configuring activities, see [HP Operations Manager Activities](hp-operations-manager-activities.md).

Delete Annotation Required Properties
-------------------------------------

| Element   | Description   | Valid Values | Look up |
|:---|:---|:---|:---|
| Message ID   | The ID of the message that contains the annotation to delete. | String   | No   |
| Annotation ID | The ID of the annotation to delete.   | String   | No   |

Delete Annotation Published Data
--------------------------------

| Element   | Description   | Value Type |
|:---|:---|:---|
| Message ID   | The ID of the message that contains the annotation that was deleted. | String   |
| Annotation ID | The ID of the annotation that was deleted.   | String   |
| HPOM Host   | The name or IP address of the HPOM management server.   | String   |
| HPOM Port   | The port used to connect to the HPOM management server.   | Integer   |
| HPOM Username | The name of the HPOM used to connect to the HPOM management server.  | String   |

Other Activities
----------------

The Integration Pack for HP Operations Manager integration contains the following additional activities:

[Acknowledge Message](acknowledge-message.md)

[Add Annotation to Message](add-annotation-to-message.md)

[Create Message](create-message.md)

[Delete Custom Attribute](delete-custom-attribute.md)

[Get Annotation](get-annotation.md)

[Get Message](get-message.md)

[Launch Tool](launch-tool.md)

[Monitor Message](monitor-message.md)

[Own/Disown Message](own/disown-message.md)

[Set Custom Attribute](set-custom-attribute.md)

[Update Annotation](update-annotation.md)

[Update Message](update-message.md)
