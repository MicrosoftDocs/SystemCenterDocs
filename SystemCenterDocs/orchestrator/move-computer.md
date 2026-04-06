---
title: Move Computer
description: You can use the Move Computer activity in a runbook to move a computer under a new parent path in the Active Directory.
ms.custom: UpdateFrequency2
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: f2e7bbaf-24b3-4aeb-ad55-2078dd21befa
ms.update-cycle: 1095-days
author: Jeronika-MS
ms.author: v-gajeronika
---
# Move Computer

You can use the Move Computer activity in a runbook to move a computer under a new parent path in the Active Directory.

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

## Move Computer required properties

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Computer Distinguished Name | Distinguished name of the computer account | String   |

## Move Computer optional properties

| Element   | Description   | Valid Values |
|:---|:---|:---|
| New Container Distinguished Name | Distinguished name of new parent path of the computer account | String   |

## Move Computer published data

| Name   | Description   | Value Type |
|:---|:---|:---|
| Computer Distinguished Name   | Distinguished name of the computer account   | String   |
| New Parent Distinguished Name | Distinguished name of new parent path of the computer account | String   |
| New Parent Path   | Path of new parent of the computer account   | String   |
