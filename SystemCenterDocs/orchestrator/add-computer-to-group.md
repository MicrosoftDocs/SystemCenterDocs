---
title: Add Computer To Group
description: You can use the Add Computer To Group activity in a runbook to add a computer to a group in the Microsoft Active Directory.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 37312c77-54fc-488b-b710-053ad0a78ba9
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Add Computer To Group

Applies To: System Center 2016 - Orchestrator

You can use the Add Computer To Group activity in a runbook to add a computer to a group in the Microsoft Active Directory.

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

## Required properties for Add Computer to Group activity

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Group Distinguished Name   | Distinguished name of the group   | String   |
| Computer Distinguished Name | Distinguished name of the computer account | String   |

## Published data for Add Computer to Group activity

| Name   | Description   | Value Type |
|:---|:---|:---|
| Group Distinguished Name   | Distinguished name of the group   | String   |
| Computer Distinguished Name | Distinguished name of the computer account | String   |
