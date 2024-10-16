---
title: Update Computer
description: You can use the Update Computer activity in a runbook to update the properties of a computer in the Microsoft Active Directory.
ms.custom: UpdateFrequency2, engagement-fy24
ms.date: 01/23/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 339881aa-8c21-4037-b4de-af1cc534546e
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
robots: noindex
---
# Update Computer



You can use the Update Computer activity in a runbook to update the properties of a computer in Microsoft Active Directory.

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

## Required properties for Update Computer activity

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Distinguished Name | Distinguished name that uniquely identifies the computer account | String   |

## Optional properties for Update Computer activity

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Description   | Description for the computer   | String   |
| Display Name  | Display name of the computer   | String   |
| DNS Host Name | Name of the computer as registered in DNS | String   |
| Location   | Computer's location   | String   |

## Published data for Update Computer activity

| Name   | Description   | Value Type |
|:---|:---|:---|
| Description   | Description for the computer   | String   |
| Display Name   | Display name of the computer   | String   |
| Distinguished Name | Distinguished name that uniquely identifies the computer account | String   |
| DNS Host Name   | Name of the computer as registered in DNS   | String   |
| Location   | Computer's location   | String   |
