---
title: Remove User From Group
description: You can use the Remove User From Group activity in a runbook to remove a user from a group in the Microsoft Active Directory.
ms.custom: UpdateFrequency2
ms.date: 12/02/2016
ms.prod: system-center
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0df95529-c73f-4b20-941f-d7914707f7e7
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
robots: noindex
---
# Remove User From Group

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

You can use the Remove User From Group activity in a runbook to remove a user from a group in the Microsoft Active Directory.

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

## Required properties for the Remove User From Group activity

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Group Distinguished Name | Distinguished name of the group   | String   |
| User Distinguished Name  | Distinguished name of the user account | String   |

## Published data for Remove User From Group activity

| Name   | Description   | Value Type |
|:---|:---|:---|
| Group Distinguished Name | Distinguished name of the group   | String   |
| User Distinguished Name  | Distinguished name of the user account | String   |
