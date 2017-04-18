---
title: Unlock User
description: You can use the Unlock User activity in a runbook to reset the user password in Active Directory.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 541e7081-1c6c-4b25-82b0-4369d48f14eb
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Unlock User

Applies To: System Center 2016 - Orchestrator

You can use the Unlock User activity in a runbook to reset the user password in Active Directory.

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

## Required properties for the Unlock User activity

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Distinguished Name | Distinguished name of the user account | String   |

## Published data for the Unlock User activity

| Name   | Description   | Value Type |
|:---|:---|:---|
| Distinguished Name | Distinguished name of the user account | String   |
