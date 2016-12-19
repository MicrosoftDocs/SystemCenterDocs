---
title: Get Group
description: You can use the Get Group activity in a runbook to get the properties of a group in the Microsoft Active Directory.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9ede00a5-b836-4c85-ae05-ab4db8f864ab
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
Get Group
=========

Applies To: System Center 2016 - Orchestrator

You can use the Get Group activity in a runbook to get the properties of a group in the Microsoft Active Directory.

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

Get Group optional properties
-----------------------------

| Element   | Description   | Valid Values |
|:---|:---|:---|
| ReturnDNOnly | If true, only the Distinguished Name property will be returned instead of all properties.   | Boolean   |
| Search Root  | The distinguished name of the node in the Active Directory Domain Services hierarchy where the search starts. | String   |
| Search Scope | The scope of the search that is observed by the server. The options are Base, OneLevel or SubTree.   | String   |

Get Group filter properties
---------------------------

| Element   | Description   | Filters   | Value Type |
|:---|:---|:---|:---|
| Common Name   | Name to identify the group   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Description   | Description for the group   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Display Name   | Display name of the group   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Group Scope   | Set of flags identifying the scope of the group   | EqualTo, NotEqualTo   | String   |
| Group Type   | Set of flags identifying the group's type   | EqualTo, NotEqualTo   | String   |
| Indirect Member   | Distinguished name of the indirect members of this group   | EqualTo   | String   |
| Indirect MemberOf | Distinguished names of groups that this group is an indirect member of | EqualTo   | String   |
| Managed By   | Distinguished name of the user that is assigned to manage this object. | EqualTo   | String   |
| Member   | Distinguished name of the members of this group   | EqualTo   | String   |
| MemberOf   | Distinguished names of groups that this group is a member of   | EqualTo   | String   |
| Sam Account Name  | Account name to support earlier versions of the operating system   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Modification Date | Date the computer account was last changed   | EqualTo, NotEqualTo, GreaterThan, GreaterThanOrEqualTo, LessThan, LessThanOrEqualTo | DateTime   |
| Creation Date   | Date and time that the account was created   | EqualTo, NotEqualTo, GreaterThan, GreaterThanOrEqualTo, LessThan, LessThanOrEqualTo | DateTime   |

Get Group published data
------------------------

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Count   | The number of groups returned by this activity.   | Integer   |
| Common Name   | Name to identify the group   | String   |
| Description   | Description for the group   | String   |
| Display Name   | Display name of the group   | String   |
| Distinguished Name | Distinguished name that uniquely identifies the group   | String   |
| Group Scope   | Set of flags that identify the scope of the group   | String   |
| Group Type   | Set of flags that identify the type of the group   | String   |
| Managed By   | Distinguished name of the user that is assigned to manage this object.   | String   |
| Sam Account Name   | Account name to support earlier versions of the operating system   | String   |
| Modification Date  | The date when the computer account was last changed   | DateTime   |
| Creation Date   | The date and time that the account was created   | DateTime   |
| Search Root   | The distinguished name of the node in the Active Directory Domain Services hierarchy where the search starts. | String   |
| Search Scope   | The scope of the search that is observed by the server. The options are Base, OneLevel or SubTree.   | String   |
