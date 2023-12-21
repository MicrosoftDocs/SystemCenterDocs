---
title: Create User Role
description: This activity creates a user role within a designated cloud.
ms.custom: UpdateFrequency3, engagement-fy24
ms.date: 10/10/2023
ms.prod: system-center
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: be8f686e-782e-424e-b804-b8945aa3ef8d
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
robots: noindex
---
# Create User Role

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

This activity creates a user role within a designated cloud.

## Create User Role Activity Required Properties

| Element   | Description   | Valid Values   |
|:---|:---|:---|
| User Role Name | The name of the user roles to be created | Alphanumeric text   |
| Profile Type   | The profile for this user role   | Delegated Admin, Read-Only Admin, Self Service User |

## Create User Role Activity Optional Properties

| Element   | Description   | Valid Values   |
|:---|:---|:---|
| Description | A text description for the user role to be created | Alphanumeric text |

## Create User Role Activity Published Data

| Element   | Description   | Valid Values   |
|:---|:---|:---|
| User Role ID   | The ID of the user role   |   |
| User Role Name   | The name of the user role   | Alphanumeric text |
| Profile Type   | The profile type of the user role |   |
| Host Group Names in Scope   |   |   |
| Cloud Names in Scope   |   |   |
| Run as Account Names   |   |   |
| Actions Permitted   | List of actions permitted   |   |
| Member Names   | Members of the user role   |   |
| Description   | Text description of the user role |   |
| User Role Data Path   | The data path   |   |
| Library Server Names   |   |   |
| VM Template Resource Names   |   |   |
| Service Template Resource Names   |   |   |
| Service Instance Resource Names   |   |   |
| VM Instance Resource Names   |   |   |
| Hardware Profile Resource Names   |   |   |
| Application Profile Resource Names   |   |   |
| Guest OS Profile Resource Names   |   |   |
| SQL Profile Resource Names   |   |   |
| Service Configuration Resource Names |   |   |
