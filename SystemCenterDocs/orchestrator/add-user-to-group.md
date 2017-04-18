---
title: Add User To Group
description: You can use the Add User To Group activity in a runbook to add a user to a group in the Microsoft Active Directory.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 38b183fe-a0ef-45f2-a6f6-615b33c072fc
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Add User To Group

Applies To: System Center 2016 - Orchestrator

You can use the Add User To Group activity in a runbook to add a user to a group in the Microsoft Active Directory.

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

## Required properties for Add User To Group activity

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Group Distinguished Name | Distinguished name of the group   | String   |
| User Distinguished Name  | Distinguished name of the user account | String   |

## Published data for Add User To Group activity

| Name   | Description   | Value Type |
|:---|:---|:---|
| Group Distinguished Name | Distinguished name of the group   | String   |
| User Distinguished Name  | Distinguished name of the user account | String   |
