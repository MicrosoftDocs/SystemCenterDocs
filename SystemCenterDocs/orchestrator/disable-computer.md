---
title: Disable Computer
description: You can use the Disable Computer activity in a runbook to disable a computer in the Microsoft Active Directory.
ms.custom: UpdateFrequency2
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 84b51ab5-b50e-4953-b0ac-7e5f2b915f83
author: jyothisuri
ms.author: jsuri
---

# Disable Computer

You can use the Disable Computer activity in a runbook to disable a computer in the Microsoft Active Directory.

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

## Required properties for Disable Computer activity

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Distinguished Name | Distinguished name of the computer account | String   |

## Published data for Disable Computer activity

| Name   | Description   | Value Type |
|:---|:---|:---|
| Distinguished Name | Distinguished name of the computer account | String   |