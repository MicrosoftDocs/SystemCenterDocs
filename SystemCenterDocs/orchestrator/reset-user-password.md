---
title: Reset User Password
description: You can use the Reset User Password activity in a runbook to reset the user password in the Microsoft Active Directory.
ms.custom: UpdateFrequency2, engagement-fy24
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 50b7bfd7-ecef-4c81-9172-854059cbc853
author: jyothisuri
ms.author: jsuri
---
# Reset User Password

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
