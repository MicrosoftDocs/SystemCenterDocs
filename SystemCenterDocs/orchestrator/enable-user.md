---
title: Enable User
description: You can use the Enable User activity in a runbook to enable a user in the Microsoft Active Directory.
ms.custom: UpdateFrequency2
ms.date: 4/25/2017
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a6a86852-db93-487a-8e9f-2e36c920980e
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
---

# Enable User

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

You can use the Enable User activity in a runbook to enable a user in the Microsoft Active Directory.

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

## Required properties for Enable User activity

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Distinguished Name | Distinguished name of the user account | String   |

## Published data for Enable User activity

| Name   | Description   | Value Type |
|:---|:---|:---|
| Distinguished Name | Distinguished name of the user account | String   |
