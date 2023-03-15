---
title: Reset User Password
description: You can use the Reset User Password activity in a runbook to reset the user password in the Microsoft Active Directory.
ms.custom: UpdateFrequency3
ms.date: 12/02/2016
ms.prod: system-center
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 50b7bfd7-ecef-4c81-9172-854059cbc853
author: jyothisuri
ms.author: jsuri
manager: mkluck
robots: noindex
---
# Reset User Password

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

You can use the Reset User Password activity in a runbook to reset the user password in Microsoft Active Directory.

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

## Required properties for Reset User Password activity

| Element   | Description   | Valid Values  |
|:---|:---|:---|
| Distinguished Name   | Distinguished name of the user account   | String   |
| User Must Change Password | Whether the user must change the password when first using the reset password. | True<br>False |
| User Password   | New password for the user   | String   |

## Published data for Reset User Password activity

| Name   | Description   | Value Type   |
|:---|:---|:---|
| Distinguished Name   | Distinguished name of the user account   | String   |
| User Must Change Password | Whether the user must change the password when first using the reset password. | True<br>False |
