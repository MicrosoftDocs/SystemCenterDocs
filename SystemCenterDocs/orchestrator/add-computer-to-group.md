---
title: Add Computer To Group
description: You can use the Add Computer To Group activity in a runbook to add a computer to a group in the Microsoft Active Directory.
ms.custom: UpdateFrequency2, engagement-fy24
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 37312c77-54fc-488b-b710-053ad0a78ba9
author: Jeronika-MS
ms.author: v-gajeronika
---
# Add Computer To Group

You can use the Add Computer To Group activity in a runbook to add a computer to a group in the Microsoft Active Directory.

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

## Required properties for Add Computer to Group activity

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Group Distinguished Name   | Distinguished name of the group   | String   |
| Computer Distinguished Name | Distinguished name of the computer account | String   |

## Published data for Add Computer to Group activity

| Name   | Description   | Value Type |
|:---|:---|:---|
| Group Distinguished Name   | Distinguished name of the group   | String   |
| Computer Distinguished Name | Distinguished name of the computer account | String   |
