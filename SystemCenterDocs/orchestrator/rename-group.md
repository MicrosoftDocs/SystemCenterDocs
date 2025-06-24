---
title: Rename Group
description: You can use the Rename Group activity in a runbook to rename a group in the Microsoft Active Directory.
ms.custom: UpdateFrequency2, engagement-fy24
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fe6cca94-3419-4008-8bb8-8d6ad02599a7
author: jyothisuri
ms.author: jsuri
robots: noindex
---
# Rename Group

You can use the Rename Group activity in a runbook to rename a group in Microsoft Active Directory.

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

## Required properties for Rename Group activity

| Element   | Description   | Valid Values |
|:---|:---|:---|
| New Common Name   | New common name for the group   | String   |
| Distinguished Name | Distinguished name of the group | String   |

## Optional properties for Rename Group activity

| Element   | Description   | Valid Values |
|:---|:---|:---|
| New Sam Account Name | New sign-in name to support earlier versions of the operating system | String   |

## Published data for Rename Group activity

| Name   | Description   | Value Type |
|:---|:---|:---|
| New Common Name   | New common name for the group   | String   |
| Distinguished Name   | Distinguished name of the group   | String   |
| New Sam Account Name | New sign-in name to support earlier versions of the operating system | String   |
