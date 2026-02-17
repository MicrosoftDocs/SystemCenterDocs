---
title: Get Organizational Unit
description: You can use the Get Organizational Unit activity in a runbook to get the properties of an organizational unit in Active Directory Domain Services (AD DS).
ms.custom: UpdateFrequency2
ms.date: 04/02/2025
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: c233113a-c20d-4196-8985-8529c9e73d02
ms.update-cycle: 1095-days
author: Jeronika-MS
ms.author: v-gajeronika
---

# Get Organizational Unit

You can use the Get Organizational Unit activity in a runbook to get the properties of an organizational unit in Active Directory Domain Services (AD DS).

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

## Get Organizational Unit optional properties

The following table lists the optional properties for Get Organizational Unit activity:

| Element   | Description   | Valid Values |
|:---|:---|:---|
| ReturnDNOnly | If true, only the Distinguished Name property will be returned instead of all the properties   | Boolean   |
| Search Root  | The distinguished name of the node in the Active Directory Domain Services hierarchy where the search starts | String   |
| Search Scope | The scope of the search that is observed by the server; the options are Base, OneLevel, or SubTree   | String   |

## Get Organizational Unit filter properties

The following table lists the filter properties for Get Organizational Unit activity:

| Element   | Description   | Filters   | Value Type |
|:---|:---|:---|:---|
| Description   | Description for the organizational unit   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Display Name   | Display name of the organizational unit   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Managed By   | Distinguished name of the user that is assigned to manage this object | EqualTo   | String   |
| Organizational Unit | Unique name to identify the organizational unit   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Modification Date   | Date the organizational unit account was last changed   | EqualTo, NotEqualTo, GreaterThan, GreaterThanOrEqualTo, LessThan, LessThanOrEqualTo | DateTime   |
| Creation Date   | Date and time that the organizational unit was created   | EqualTo, NotEqualTo, GreaterThan, GreaterThanOrEqualTo, LessThan, LessThanOrEqualTo | DateTime   |

## Get Organizational Unit published data

The following table lists the published data for Get Organizational Unit activity:

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Description   | Description for the organizational unit   | String   |
| Count   | The number of organizational units returned by this activity   | Integer   |
| Display Name   | Display name of the organizational unit   | String   |
| Distinguished Name  | Distinguished name that uniquely identifies the organizational unit   | String   |
| Managed By   | Distinguished name of the user that is assigned to manage this object   | String   |
| Organizational Unit | Unique name to identify the organizational unit   | String   |
| Modification Date   | Date the organizational unit account was last changed   | DateTime   |
| Creation Date   | Date and time that the organizational unit was created   | DateTime   |
| Search Root   | The distinguished name of the node in the Active Directory Domain Services hierarchy where the search starts | String   |
| Search Scope   | The scope of the search that is observed by the server; the options are Base, OneLevel, or SubTree | String   |
