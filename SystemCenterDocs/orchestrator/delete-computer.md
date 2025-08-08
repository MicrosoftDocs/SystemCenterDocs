---
title: Delete Computer
description: You can use the Delete Computer activity in a runbook to delete a computer in the Microsoft Active Directory.
ms.custom: UpdateFrequency2
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 45b7c571-5ae6-46a9-8154-531927a1dfb3
author: jyothisuri
ms.author: jsuri
robots: noindex
---
# Delete Computer

You can use the Delete Computer activity in a runbook to delete a computer in the Microsoft Active Directory.

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

## Required properties for Delete Computer activity

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Distinguished Name | Distinguished name of the computer account to delete | String   |

## Published data for Delete Computer activity

| Name   | Description   | Value Type |
|:---|:---|:---|
| Distinguished Name | Distinguished name of the computer account to delete | String   |
