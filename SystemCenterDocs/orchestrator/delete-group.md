---
title: Delete Group
description: You can use the Delete Group activity in a runbook to delete a group in the Microsoft Active Directory.
ms.custom: UpdateFrequency2
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: a9e39268-b3aa-493c-b6f1-7b4862164f5d
author: Jeronika-MS
ms.author: v-gajeronika
---
# Delete Group

You can use the Delete Group activity in a runbook to delete a group in the Microsoft Active Directory.

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

## Required properties for Delete Group activities

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Distinguished Name | Distinguished name of the group to delete | String |

## Published data for Delete Group activity

| Name   | Description   | Value Type |
|:---|:---|:---|
| Distinguished Name | Distinguished name of the group to delete | String |
