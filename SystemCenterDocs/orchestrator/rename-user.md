---
title: Rename User
description: You can use the Rename User activity in a runbook to rename a computer in the Microsoft Active Directory.
ms.custom: UpdateFrequency2, engagement-fy24
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 2fa89f30-9b7d-4f15-a885-d07a94c4ce37
ms.update-cycle: 1095-days
author: Jeronika-MS
ms.author: v-gajeronika
---
# Rename User

You can use the Rename User activity in a runbook to rename a computer in Microsoft Active Directory.

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

## Required properties for Rename User activity

| Element   | Description   | Valid Values |
|:---|:---|:---|
| New Common Name   | New common name for the user account   | String   |
| Distinguished Name   | Distinguished name of the user account   | String   |
| New Sam Account Name | New sign-in name to support earlier versions of the operating system | String   |

## Published data for Rename User activity

| Name   | Description   | Value Type |
|:---|:---|:---|
| New Common Name   | New common name for the user account   | String   |
| Distinguished Name   | Distinguished name of the user account   | String   |
| New Sam Account Name | New sign-in name to support earlier versions of the operating system | String   |
