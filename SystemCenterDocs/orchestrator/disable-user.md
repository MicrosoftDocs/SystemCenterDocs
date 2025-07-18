---
title: Disable User
description: You can use the Disable User activity in a runbook to disable a user in the Microsoft Active Directory.
ms.custom: UpdateFrequency2
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: e8ddbe63-4f10-4907-838f-e76173295162
author: jyothisuri
ms.author: jsuri
---

# Disable User

You can use the Disable User activity in a runbook to disable a user in the Microsoft Active Directory.

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

## Required properties for Disable User activity

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Distinguished Name | Distinguished name of the user account | String   |

## Published data for Disable User activity

| Name   | Description   | Value Type |
|:---|:---|:---|
| Distinguished Name | Distinguished name of the user account | String   |
