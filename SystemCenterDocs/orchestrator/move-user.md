---
title: Move User
description: You can use the Move User activity in a runbook to move a user under a new parent path in the Microsoft Active Directory.
ms.custom: UpdateFrequency3
ms.date: 12/02/2016
ms.prod: system-center
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 17575faf-3a92-453f-882f-e00f79b6f44e
author: jyothisuri
ms.author: jsuri
manager: mkluck
robots: noindex
---
# Move User

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

You can use the Move User activity in a runbook to move a user under a new parent path in the Microsoft Active Directory.

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

## Move User required properties

| Element   | Description   | Valid Values |
|:---|:---|:---|
| User Distinguished Name | Distinguished name of the user account | String   |

## Move User optional properties

| Element   | Description   | Valid Values |
|:---|:---|:---|
| New Container Distinguished Name | Distinguished name of new container path of the user account | String   |

## Move User published data

| Name   | Description   | Value Type |
|:---|:---|:---|
| User Distinguished Name   | Distinguished name of the user account   | String   |
| New Parent Distinguished Name | Distinguished name of new parent path of the user account | String   |
| New Parent Path   | Path of new parent of the user account   | String   |
