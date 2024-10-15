---
title: Enable Computer
description: You can use the Enable Computer activity in a runbook to enable a computer in the Microsoft Active Directory.
ms.custom: UpdateFrequency2
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d187fb68-3036-42e6-958b-92060bf4e545
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
---

# Enable Computer

You can use the Enable Computer activity in a runbook to enable a computer in the Microsoft Active Directory.

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

## Required properties for Enable Computer activity

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Distinguished Name | Distinguished name of the computer account | String   |

## Published data for Enable Computer activity

| Name   | Description   | Value Type |
|:---|:---|:---|
| Distinguished Name | Distinguished name of the computer account | String   |
