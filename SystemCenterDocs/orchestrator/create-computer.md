---
title: Create Computer
description: You can use the Create Computer activity in a runbook to create an entry for a computer in the Microsoft Active Directory.
ms.custom: UpdateFrequency2
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 509fb603-b567-4497-85c7-4fbf4a1cec0f
author: Jeronika-MS
ms.author: v-gajeronika
ms.update-cycle: 1095-days
---
# Create Computer

You can use the Create Computer activity in a runbook to create an entry for a computer in the Microsoft Active Directory. Typically, you would do this if you would like to pre-assign the Organizational Unit (OU) in which certain computers should go once they join the domain.

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

## Required properties for Create Computer activity

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Common Name | Name to identify the computer | String   |

## Optional properties for Create Computer activity

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Container Distinguished Name | Distinguished name of the container where the computer is located   | String   |
| Description   | Description for the computer   | String   |
| Display Name   | Display name of the computer   | String   |
| DNS Host Name   | Name of the computer as registered in DNS   | String   |
| Location   | Computer's location   | String   |
| SAM Account Name   | The Security Accounts Manager (SAM) sign-in name used to support clients and servers running earlier versions of the operating system. | String   |

## Published data for Create Computer activity

| Name   | Description   | Value Type |
|:---|:---|:---|
| Common Name   | Name to identify the computer   | String   |
| Container Distinguished Name | Distinguished name of the container where the computer is located | String   |
| Container Path   | Path of the container where the computer is located   | String   |
| Description   | Description for the computer   | String   |
| Display Name   | Display name of the computer   | String   |
| Distinguished Name   | Distinguished name that uniquely identifies the computer account  | String   |
| DNS Host Name   | Name of the computer as registered in DNS   | String   |
| Location   | Computer's location   | String   |
