---
title: Rename Group
description: You can use the Rename Group activity in a runbook to rename a group in the Microsoft Active Directory.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: fe6cca94-3419-4008-8bb8-8d6ad02599a7
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Rename Group

> Applies To: System Center 2016 - Orchestrator

You can use the Rename Group activity in a runbook to rename a group in the Microsoft Active Directory.

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
| New Sam Account Name | New logon name to support earlier versions of the operating system | String   |

## Published data for Rename Group activity

| Name   | Description   | Value Type |
|:---|:---|:---|
| New Common Name   | New common name for the group   | String   |
| Distinguished Name   | Distinguished name of the group   | String   |
| New Sam Account Name | New logon name to support earlier versions of the operating system | String   |
