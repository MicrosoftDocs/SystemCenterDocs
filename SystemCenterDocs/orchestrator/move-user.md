---
title: Move User
description: You can use the Move User activity in a runbook to move a user under a new parent path in the Microsoft Active Directory.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 17575faf-3a92-453f-882f-e00f79b6f44e
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Move User

You can use the Move User activity in a runbook to move a user under a new parent path in the Microsoft Active Directory.

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

## Move User required properties

| Element   | Description   | Valid Values |
|:---|:---|:---|
| User Distinguished Name | Distinguished name of the user account | String   |

## Move User optional properties

| Element   | Description   | Valid Values |
|:---|:---|:---|
| New Container Distinguished Name | Distinguished name of new container path of the user account | String   |

## Move User published data

| Name   | Description   | Value Type |
|:---|:---|:---|
| User Distinguished Name   | Distinguished name of the user account   | String   |
| New Parent Distinguished Name | Distinguished name of new parent path of the user account | String   |
| New Parent Path   | Path of new parent of the user account   | String   |
