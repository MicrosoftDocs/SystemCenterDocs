---
title: Move Group
description: You can use the Move Group activity in a runbook to move a group under a new parent path in the Microsoft Active Directory.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 1673dd33-f7e3-43e7-af9d-daecccd71558
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Move Group

> Applies To: System Center 2016 - Orchestrator

You can use the Move Group activity in a runbook to move a group under a new parent path in the Microsoft Active Directory.

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

## Move Group required properties

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Group Distinguished Name | Distinguished name of the group | String   |

## Move Group optional properties

| Element   | Description   | Valid Values |
|:---|:---|:---|
| New Container Distinguished Name | Distinguished name of new container path of the group | String   |

## Move Group published data

| Name   | Description   | Value Type |
|:---|:---|:---|
| Group Distinguished Name   | Distinguished name of the group   | String   |
| New Parent Distinguished Name | Distinguished name of new parent path of the group | String   |
| New Parent Path   | Path of new parent of the group   | String   |
