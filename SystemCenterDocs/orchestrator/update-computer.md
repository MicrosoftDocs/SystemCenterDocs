---
title: Update Computer
description: You can use the Update Computer activity in a runbook to update the properties of a computer in the Microsoft Active Directory.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 339881aa-8c21-4037-b4de-af1cc534546e
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Update Computer

Applies To: System Center 2016 - Orchestrator

You can use the Update Computer activity in a runbook to update the properties of a computer in the Microsoft Active Directory.

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
