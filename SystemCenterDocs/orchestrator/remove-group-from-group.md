---
title: Remove Group From Group
description: You can use the Remove Group From Group activity in a runbook to remove a group from a group in the Microsoft Active Directory.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: fc22dcd6-bd35-4e41-9ee6-f6060e6c014b
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Remove Group From Group

> Applies To: System Center 2016 - Orchestrator

You can use the Remove Group From Group activity in a runbook to remove a group from a group in the Microsoft Active Directory.

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

## Required properties for Remove Group From Group activity

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Group Distinguished Name   | Distinguished name of the child group  | String   |
| Parent Group Distinguished Name | Distinguished name of the parent group | String   |

## Published data for Remove Group From Group activity

| Name   | Description   | Value Type |
|:---|:---|:---|
| Parent Group Distinguished Name | Distinguished name of the parent group | String   |
| Group Distinguished Name   | Distinguished name of the child group  | String   |
