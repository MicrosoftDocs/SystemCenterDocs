---
title: Remove Computer From Group
description: You can use the Remove Computer From Group activity in a runbook to remove a computer from a group in the Microsoft Active Directory.
ms.custom: UpdateFrequency2, engagement-fy24
ms.date: 01/23/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c5f2a00-b4bf-4315-b976-dd0a7005e47b
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
robots: noindex
---
# Remove Computer From Group

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

You can use the Remove Computer From Group activity in a runbook to remove a computer from a group in the Microsoft Active Directory.

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

## Required properties for Remove Computer From Group activity

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Group Distinguished Name   | Distinguished name of the group   | String   |
| Computer Distinguished Name | Distinguished name of the user account | String   |

## Published data for Remove Computer From Group activity

| Name   | Description   | Value Type |
|:---|:---|:---|
| Group Distinguished Name   | Distinguished name of the group   | String   |
| Computer Distinguished Name | Distinguished name of the user account | String   |
