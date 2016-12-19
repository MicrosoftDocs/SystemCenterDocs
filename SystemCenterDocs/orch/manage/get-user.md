---
title: Get User
description: You can use the Get User activity in a runbook to get the properties of a user in the Microsoft Active Directory.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c058aab3-9e89-4c52-93d6-d66666d4ba2f
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
Get User
========

Applies To: System Center 2016 - Orchestrator

You can use the Get User activity in a runbook to get the properties of a user in the Microsoft Active Directory.

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

Get User optional properties
----------------------------

| Element   | Description   | Valid Values |
|:---|:---|:---|
| ReturnDNOnly | If true, only the Distinguished Name property will be returned instead of all properties   | Boolean   |
| Search Root  | The distinguished name of the node in the Active Directory Domain Services hierarchy where the search starts | String   |
| Search Scope | The scope of the search that is observed by the server. The options are Base, OneLevel or SubTree.   | String   |

Get User filter properties
--------------------------

| Element   | Description   | Filters   | Value Type |
|:---|:---|:---|:---|
| Account Expires   | Date that the account expires   | EqualTo, NotEqualTo, GreaterThan, GreaterThanOrEqualTo, LessThan, LessThanOrEqualTo. | DateTime   |
| Disabled   | Specifies whether the account is currently disabled   | EqualTo, NotEqualTo.   | Boolean   |
| Expired   | Specifies whether the account is currently expired   | EqualTo, NotEqualTo.   | Boolean   |
| Locked   | Specifies whether the account is currently locked   | EqualTo, NotEqualTo.   | Boolean   |
| Account Never Expires   | Specifies that account never expires   | EqualTo, NotEqualTo.   | Boolean   |
| City   | User's city   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith.   | String   |
| Common Name   | Name to identify the user   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith.   | String   |
| Company   | User's company name   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith.   | String   |
| Department   | User's department name in their company   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith.   | String   |
| Description   | Description of the user   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith.   | String   |
| Display Name   | Display name for the user   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith.   | String   |
| Fax Number   | User's fax number   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith.   | String   |
| First Name   | User's first name   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith.   | String   |
| Home Directory   | Home directory for the user account   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith.   | String   |
| Home Drive   | Specifies the drive letter to which to map the UNC path specified by homeDirectory   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith.   | String   |
| Home Phone   | User's home telephone number   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith.   | String   |
| Indirect MemberOf   | Distinguished names of groups that this user is an indirect member of   | EqualTo   | String   |
| Initials   | Initials of the user's name   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith.   | String   |
| Last Name   | User's last name   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith.   | String   |
| Lockout Time   | Date and time that the account was locked out   | EqualTo, NotEqualTo, GreaterThan, GreaterThanOrEqualTo, LessThan, LessThanOrEqualTo. | DateTime   |
| Email   | Email addresses for the user   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith.   | String   |
| Manager   | Distinguished name of the account for the user's manager   | EqualTo   | String   |
| MemberOf   | Distinguished names of groups that this user is a member of   | EqualTo   | String   |
| Mobile Phone   | User's mobile telephone number   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith.   | String   |
| Pager   | User's pager telephone number   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith.   | String   |
| Password Never Expires   | Specifies that the user's password never expires   | EqualTo, NotEqualTo.   | Boolean   |
| Notes   | General notes about the user   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith.   | String   |
| Office   | User's office location   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith.   | String   |
| Post Office Box   | User's post office box number   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith.   | String   |
| Postal Code   | User's postal code or zip code   | EqualTo,No tEqualTo, Contains, DoesNotContain, EndsWith, StartsWith.   | String   |
| Profile Path   | Path to the location for the user's profile   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith.   | String   |
| Sam Account Name   | Logon name to support earlier versions of the operating system   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith.   | String   |
| Logon Script   | Path and name of the logon script for the account   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith.   | String   |
| State or Province   | User's state or province   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith.   | String   |
| Street Address   | User's street address   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith.   | String   |
| Phone Number   | User's telephone number   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| RDS Allow Logon   | Specifies whether the user is allowed to log on to Remote Desktop Services   | EqualTo, NotEqualTo.   | Boolean   |
| RDS Broken Connection Action | Specifies the action to take when a Remote Desktop Services session limit is reached   | EqualTo, NotEqualTo.   | Boolean   |
| RDS Connect Client Drives   | Specifies whether to reconnect to mapped client drives when user logs on to a Remote Desktop Services session   | EqualTo, NotEqualTo.   | Boolean   |
| RDS Connect Printer Drives   | Specifies whether to reconnect to mapped client printers when user logs on to a Remote Desktop Services session   | EqualTo, NotEqualTo.   | Boolean   |
| RDS Default To Main Printer  | Specifies whether to print automatically to the client's default printer from a Remote Desktop Services session   | EqualTo, NotEqualTo.   | Boolean   |
| RDS Home Directory   | Home directory for the user when they log on to Remote Desktop Services   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith.   | String   |
| RDS Home Drive   | Home drive for the user when they log on to Remote Desktop Services   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith.   | String   |
| RDS Initial Program   | Path and file name of the application to start automatically when the user logs on to the Remote Desktop Services   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith.   | String   |
| RDS Max Connection Time   | Maximum duration, in minutes, of a Remote Desktop Session for the user   | EqualTo, NotEqualTo, GreaterThan, GreaterThanOrEqualTo, LessThan, LessThanOrEqualTo. | Int32   |
| RDS Max Disconnection Time   | Maximum amount of time, in minutes, that a disconnected Remote Desktop Services session remains active for the user   | EqualTo, NotEqualTo, GreaterThan, GreaterThanOrEqualTo, LessThan, LessThanOrEqualTo. | Int32   |
| RDS Max Idle Time   | Maximum amount of time, in minutes, that a Remote Desktop Services session can remain idle for the user   | EqualTo, NotEqualTo, GreaterThan, GreaterThanOrEqualTo, LessThan, LessThanOrEqualTo. | Int32   |
| RDS Profile Path   | Roaming or mandatory profile path to use when the user logs on to Remote Desktop Services   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith.   | String   |
| RDS Reconnection Action   | Specifies whether the user is allowed to reconnect to a disconnected Remote Desktop Services session   | EqualTo, NotEqualTo.   | Boolean   |
| RDS Remote Control   | Specifies whether to allow remote observation or remote control of the user's Remote Desktop Services session   | EqualTo, NotEqualTo, GreaterThan, GreaterThanOrEqualTo, LessThan, LessThanOrEqualTo. | Int32   |
| RDS Work Directory   | Working directory path for the user in a Remote Desktop Session   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith.   | String   |
| Title   | User's job title   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith.   | String   |
| User Principal Name   | This attribute contains the UPN that is an Internet-style login name for a user based on the Internet standard RFC 822. | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith.   | String   |
| Modification Date   | Date the user account was last changed   | EqualTo, NotEqualTo, GreaterThan, GreaterThanOrEqualTo, LessThan, LessThanOrEqualTo. | DateTime   |
| Creation Date   | Date and time that the account was created   | EqualTo, NotEqualTo, GreaterThan, GreaterThanOrEqualTo, LessThan, LessThanOrEqualTo   | DateTime   |
| Web Page   | User's primary web page   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith.   | String   |

Get User published data
-----------------------

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Account Expires   | Date that the account expires   | DateTime   |
| Count   | The number of groups returned by this activity.   | Integer   |
| Disabled   | Specifies whether the account is currently disabled   | Boolean   |
| Expired   | Specifies whether the account is currently expired   | Boolean   |
| Locked   | Specifies whether the account is currently locked   | Boolean   |
| Account Never Expires   | Specifies that account never expires   | Boolean   |
| City   | User's city   | String   |
| Common Name   | Name to identify the user   | String   |
| Company   | User's company name   | String   |
| Department   | User's department name in their company   | String   |
| Description   | Description of the user   | String   |
| Display Name   | Display name for the user   | String   |
| Distinguished Name   | Distinguished name that uniquely identifies the user account   | String   |
| Fax Number   | User's fax number   | String   |
| First Name   | User's first name   | String   |
| Home Directory   | The Home directory for the user account   | String   |
| Home Drive   | Specifies the drive letter to which to map the UNC path specified by homeDirectory   | String   |
| Home Phone   | User's home telephone number   | String   |
| Initials   | Initials of the user's name   | String   |
| Last Name   | User's last name   | String   |
| Lockout Time   | Date and time that the account was locked out   | DateTime   |
| Email   | Email addresses for the user   | String   |
| Manager   | Distinguished name of the account for the user's manager   | String   |
| Mobile Phone   | User's mobile telephone number   | String   |
| Pager   | User's pager telephone number   | String   |
| Password Expired   | Specifies whether the password is expired   | Boolean   |
| Password Last Set   | Date and time that the password was last set   | DateTime   |
| Password Never Expires   | Specifies that the user's password never expires   | Boolean   |
| Notes   | General notes about the user   | String   |
| Office   | User's office location   | String   |
| Post Office Box   | User's post office box number   | String   |
| Postal Code   | User's postal code or zip code   | String   |
| Profile Path   | Path to the location for the user's profile   | String   |
| Sam Account Name   | Logon name to support earlier versions of the operating system   | String   |
| Logon Script   | Path and name of the logon script for the account   | String   |
| State or Province   | User's state or province   | String   |
| Street Address   | User's street address   | String   |
| Phone Number   | User's telephone number   | String   |
| RDS Allow Logon   | Specifies whether the user is allowed to log on to Remote Desktop Services   | Boolean   |
| RDS Broken Connection Action | Specifies the action to take when a Remote Desktop Services session limit is reached   | Boolean   |
| RDS Connect Client Drives   | Specifies whether to reconnect to mapped client drives when user logs on to a Remote Desktop Services session   | Boolean   |
| RDS Connect Printer Drives   | Specifies whether to reconnect to mapped client printers when user logs on to a Remote Desktop Services session   | Boolean   |
| RDS Default To Main Printer  | Specifies whether to print automatically to the client's default printer from a Remote Desktop Services session   | Boolean   |
| RDS Home Directory   | The Home directory for the user when they log on to Remote Desktop Services   | String   |
| RDS Home Drive   | The Home drive for the user when they log on to Remote Desktop Services   | String   |
| RDS Initial Program   | Path and file names of the application to start automatically when the user logs on to the Remote Desktop Services   | String   |
| RDS Max Connection Time   | The maximum duration, in minutes, of a Remote Desktop Session for the user   | Int32   |
| RDS Max Disconnection Time   | The maximum amount of time, in minutes, that a disconnected Remote Desktop Services session remains active for the user | Int32   |
| RDS Max Idle Time   | The maximum amount of time, in minutes, that a Remote Desktop Services session can remain idle for the user   | Int32   |
| RDS Profile Path   | Roaming or mandatory profile path to use when the user logs on to Remote Desktop Services   | String   |
| RDS Reconnection Action   | Specifies whether the user is allowed to reconnect to a disconnected Remote Desktop Services session   | Boolean   |
| RDS Remote Control   | Specifies whether to allow remote observation or remote control of the user's Remote Desktop Services session   | Int32   |
| RDS Work Directory   | The working directory path for the user in a Remote Desktop Session   | String   |
| Runbook Server Name   | The name the runbook server that is running the search.   | String   |
| Search Root   | The distinguished name of the node in the Active Directory Domain Services hierarchy where the search starts.   | String   |
| Search Scope   | The scope of the search that is observed by the server. The options are Base, OneLevel or SubTree.   | String   |
| Title   | User's job title   | String   |
| User Cannot Change Password  | Specifies that the user cannot change their password   | Boolean   |
| User Principal Name   | This attribute contains the UPN that is an Internet-style login name for a user based on the Internet standard RFC 822  | String   |
| Modification Date   | The date when the user account was last changed   | DateTime   |
| Creation Date   | The date and time when the account was created   | DateTime   |
| Web Page   | User's primary web page   | String   |

