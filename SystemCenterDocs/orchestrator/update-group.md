---
title: Update Group
description: You can use the Update Group activity in a runbook to update properties of a group in the Microsoft Active Directory.
ms.custom: UpdateFrequency2, engagement-fy24
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 9ddbe80a-4efb-4679-b880-bda7228c167e
author: jyothisuri
ms.author: jsuri
---
# Update Group

You can use the Update Group activity in a runbook to update properties of a group in Microsoft Active Directory.

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

## Required properties for Update Group activity

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Distinguished Name | Distinguished name that uniquely identifies the group | String   |

## Optional properties for Update Group activity

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Description  | Description for the group   | String   |
| Display Name | Display name of the group   | String   |
| Group Scope  | Set of flags identifying the scope of the group | String   |
| Group Type   | Set of flags identifying the type of the group  | String   |

## Published data for Update Group activity

| Name   | Description   | Value Type |
|:---|:---|:---|
| Description   | Description for the group   | String   |
| Display Name   | Display name of the group   | String   |
| Distinguished Name | Distinguished name that uniquely identifies the group | String   |
| Group Scope   | Set of flags identifying the scope of the group   | String   |
| Group Type   | Set of flags identifying the type of the group   | String   |
