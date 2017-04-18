---
title: Get Computer
description: You can use the Get Computer activity in a runbook to get the properties of a computer in Active Directory.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a2d782b3-10c2-453c-bb23-47ff4f7b0047
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Get Computer

Applies To: System Center 2016 - Orchestrator

You can use the Get Computer activity in a runbook to get the properties of a computer in Active Directory.

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

## Get Computer optional properties

| Element   | Description   | Valid Values |
|:---|:---|:---|
| ReturnDNOnly | If true, only the Distinguished Name property will be returned instead of all properties.   | Boolean   |
| Search Root  | The distinguished name of the node in the Active Directory Domain Services hierarchy where the search starts. | String   |
| Search Scope | The scope of the search that is observed by the server. The options are Base, OneLevel or SubTree.   | String   |

## Get Computer filter properties

| Element   | Description   | Filters   | Value Type |
|:---|:---|:---|:---|
| Disabled   | Specifies whether the account is currently disabled   | EqualTo, NotEqualTo   | Boolean   |
| Common Name   | Name to identify the computer   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Description   | Description for the computer   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Display Name   | Display name of the computer   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Indirect MemberOf   | Distinguished names of groups that this computer is an indirect member of | EqualTo   | String   |
| Computer Role   | Computer's role in the domain: Domain Controller, server, or workstation  | Equals, DoesNotEqual   | Int32   |
| Location   | Computer's location   | Equals, DoesNotEqual   | String   |
| Managed By   | Distinguished name of the user that is assigned to manage this object.   | EqualTo   | String   |
| MemberOf   | Distinguished names of groups that this computer is a member of   | EqualTo   | String   |
| Operating System   | Name of the computer's operating system   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Operating System Service Pack | Service pack level of the computer's operating system   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Operating System Version   | Version of the computer's operating system   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| DNS Host Name   | Name of the computer as registered in DNS   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Sam Account Name   | Account name to support earlier versions of the operating system   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Modification Date   | Date the computer account was last changed   | EqualTo, NotEqualTo, GreaterThan, GreaterThanOrEqualTo, LessThan, LessThanOrEqualTo | DateTime   |
| Creation Date   | Date and time that the account was created   | EqualTo, NotEqualTo, GreaterThan, GreaterThanOrEqualTo, LessThan, LessThanOrEqualTo | DateTime   |

## Get Computer published data

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Disabled   | Specifies whether the account is currently disabled.   | Boolean   |
| Common Name   | Name to identify the computer.   | String   |
| Count   | The number of groups returned by this activity.   | Integer   |
| Description   | Description of the computer.   | String   |
| Display Name   | Displays the name of the computer   | String   |
| Distinguished Name   | Distinguished name that uniquely identifies the computer account   | String   |
| DNS Host Name   | Name of the computer as registered in DNS   | String   |
| Location   | Computer's location   | String   |
| Computer Role   | Computer's role in the domain: Domain Controller, server, or workstation   | Int32   |
| Managed By   | Distinguished name of the user that is assigned to manage this object.   | String   |
| Operating System   | Name of the computer operating system   | String   |
| Operating System Service Pack | Service pack level of the computer operating system   | String   |
| Operating System Version   | Version of the computer operating system   | String   |
| Sam Account Name   | Account name to support earlier versions of the operating system   | String   |
| Modification Date   | The date when the computer account was last changed   | DateTime   |
| Creation Date   | The date and time when the account was created   | DateTime   |
| Search Root   | The distinguished name of the node in the Active Directory Domain Services hierarchy where the search starts. | String   |
| Search Scope   | The scope of the search that is observed by the server. The options are Base, OneLevel or SubTree.   | String   |
