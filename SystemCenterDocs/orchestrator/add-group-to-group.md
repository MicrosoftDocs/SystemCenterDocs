---
title: Add Group To Group
description: You can use the Add Group To Group activity in a runbook to add a group to a group in the Microsoft Active Directory.
ms.custom: UpdateFrequency2, engagement-fy24
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 3017b8c2-be10-44cf-a806-e7ec13d4e8c7
author: jyothisuri
ms.author: jsuri
---
# Add Group To Group

You can use the Add Group To Group activity in a runbook to add a group to a group in the Microsoft Active Directory.

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

## Required properties for Add Group To activity

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Parent Group Distinguished Name | Distinguished name of the parent group | String   |
| Group Distinguished Name   | Distinguished name of the group   | String   |

## Published data for Add Group To Group activity

| Name   | Description   | Value Type |
|:---|:---|:---|
| Parent Group Distinguished Name | Distinguished name of the parent group | String   |
| Group Distinguished Name   | Distinguished name of the group   | String   |
