---
title: Update User Role Property
description: Updates User Role Property
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 6cb84e98-be26-4aa5-b0d4-d1400a8852db
author: jyothisuri
ms.author: jsuri
robots: noindex
---
# Update User Role Property

Updates User Role Property

## Update User Role Property Required Properties

| Element   | Description   | Valid Values   |
|:---|:---|:---|
| User Role Name | The name of the user role to update   | Alphanumeric text   |
| Action Type   | The type of update action   | Add, Remove   |
| Property   | The property to be updated   | Select from list of Properties |
| Value   | The new value assigned to the newly added property | Based on property value type   |

## Updates User Role Property Optional Properties

| Element   | Description   | Valid Values   |
|:---|:---|:---|
| Description | Text explanation of the user role | Alphanumeric text |

## Updates User Role Property Published Data

| Element   | Description   | Valid Values   |
|:---|:---|:---|
| User Role ID   | The ID of the user role   |   |
| User Role Name   | The name of the user role   | string   |
| Profile Type   | The profile type of the user role   | string   |
| Host Group Names in Scope  | Name or names of the host groups   | string   |
| Cloud Names in Scope   | Name or names of the cloud names   | string   |
| Run as Account Names   | Name or names of the run as accounts  | string   |
| Actions Permitted   | List of actions permitted   | string   |
| Member Names   | Members of the user role   | string   |
| Description   | Text description of the user role   | Alphanumeric text |
| User Role Data Path   | Location of User Role data.   | string   |
| Library Server Names   | The names of the VMM Library Servers. | string   |
| VM Template Resource Names | The names of the VM templates.   | string   |
