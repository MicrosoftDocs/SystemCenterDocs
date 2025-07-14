---
title: Delete User
description: You can use the Delete User activity in a runbook to delete a user in the Microsoft Active Directory.
ms.custom: UpdateFrequency2
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 7db21ed7-b166-44a5-a8f1-70ede936fbef
author: jyothisuri
ms.author: jsuri
robots: noindex
---
# Delete User

You can use the Delete User activity in a runbook to delete a user in the Microsoft Active Directory.

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

## Required properties for Delete User activity

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Distinguished Name | Distinguished name of the user account to delete | String   |

## Published data for Delete User activity

| Name   | Description   | Value Type |
|:---|:---|:---|
| Distinguished Name | Distinguished name of the user account to delete | String   |
