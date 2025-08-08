---
title: Remove Group From Group
description: You can use the Remove Group From Group activity in a runbook to remove a group from a group in the Microsoft Active Directory.
ms.custom: UpdateFrequency2, engagement-fy24
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: fc22dcd6-bd35-4e41-9ee6-f6060e6c014b
author: jyothisuri
ms.author: jsuri
---
# Remove Group From Group

You can use the Remove Group From Group activity in a runbook to remove a group from a group in Microsoft Active Directory.

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

## Required properties for Remove Group From Group activity

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Group Distinguished Name   | Distinguished name of the child group  | String   |
| Parent Group Distinguished Name | Distinguished name of the parent group | String   |

## Published data for Remove Group From Group activity

| Name   | Description   | Value Type |
|:---|:---|:---|
| Parent Group Distinguished Name | Distinguished name of the parent group | String   |
| Group Distinguished Name   | Distinguished name of the child group  | String   |
