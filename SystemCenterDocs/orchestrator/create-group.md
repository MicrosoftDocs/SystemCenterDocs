---
title: Create Group
description: You can use the Create Group activity in a runbook to create a group in the Microsoft Active Directory.
ms.custom: UpdateFrequency2
ms.date: 12/04/2023
ms.prod: system-center
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 602441b9-6c17-42bf-8eef-1ab814d0adbc
author: jyothisuri
ms.author: jsuri
manager: mkluck
robots: noindex
---
# Create Group

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

You can use the Create Group activity in a runbook to create a group in the Microsoft Active Directory.

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

## Required properties for Create Group activity

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Common Name | Name to identify the group | String   |

## Optional properties for Create Group activity

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Container Distinguished Name | Distinguished name of the container where the group is located   | String   |
| Description   | Description for the group   | String   |
| Display Name   | Display the name of the group   | String   |
| Group Scope   | Set of flags identifying the scope of the group   | String   |
| Group Type   | Set of flags identifying the group's type   | String   |
| SAM Account Name   | The Security Accounts Manager (SAM) sign-in name used to support clients and servers running earlier versions of the operating system. | String   |

## Published data for Create Group activity

| Name   | Description   | Value Type |
|:---|:---|:---|
| Common Name   | Name to identify the group   | String   |
| Description   | Description for the group   | String   |
| Display Name   | Display the name of the group   | String   |
| Distinguished Name   | Distinguished name that uniquely identifies the group   | String   |
| Group Scope   | Set of flags identifying the scope of the group   | String   |
| Group Type   | Set of flags identifying the type of the group   | String   |
| Container Distinguished Name | Distinguished name of the container where the group is located   | String   |
| Container Path   | Path of the container where the group is located   | String   |
| SAM Account Name   | The Security Accounts Manager (SAM) sign-in name used to support clients and servers running earlier versions of the operating system. | String   |
