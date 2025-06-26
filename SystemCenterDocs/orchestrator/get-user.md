---
title: Get User
description: You can use the Get User activity in a runbook to get the properties of a user in the Microsoft Active Directory.
ms.custom: UpdateFrequency2
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: c058aab3-9e89-4c52-93d6-d66666d4ba2f
author: jyothisuri
ms.author: jsuri
manager: jsuri
---

# Get User

You can use the Get User activity in a runbook to get the properties of a user in Microsoft Active Directory.

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

## [Get User Optional properties](#tab/get-user-optional-properties)

| Element   | Description   | Valid values |
|:---|:---|:---|
| ReturnDNOnly | If true, only the Distinguished Name property will be returned instead of all properties   | Boolean   |
| Search Root  | Distinguished name of the node in the Active Directory Domain Services (AD DS) hierarchy where the search starts | String   |
| Search Scope | Scope of the search that is observed by the server; the options are Base, OneLevel, or SubTree   | String   |

## [Get User Filter properties](#tab/get-user-filter-properties)

| Element   | Description   | Filters   | Value type |
|:---|:---|:---|:---|
| Account Expires   | Date that the account expires   | EqualTo, NotEqualTo, GreaterThan, GreaterThanOrEqualTo, LessThan, LessThanOrEqualTo | DateTime   |
| Disabled   | Whether the account is currently disabled   | EqualTo, NotEqualTo   | Boolean   |
| Expired   | Whether the account is currently expired   | EqualTo, NotEqualTo   | Boolean   |
| Locked   | Whether the account is currently locked   | EqualTo, NotEqualTo   | Boolean   |
| Account Never Expires   | Account never expires   | EqualTo, NotEqualTo   | Boolean   |
| City   | User's city   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Common Name   | Name to identify the user   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Company   | User's company name   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Department   | User's department name in their company   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Description   |Description of the user   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Display Name   | Display name for the user   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Fax Number   | User's fax number   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| First Name   | User's first name   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Home Directory   | Home directory for the user account   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Home Drive   | Drive letter to which to map the UNC path specified by homeDirectory   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Home Phone   | User's home telephone number   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Indirect MemberOf   | Distinguished names of groups that this user is an indirect member of   | EqualTo   | String   |
| Initials   | Initials of the user's name   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Last Name   | User's last name   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Lockout Time   | Date and time that the account was locked out   | EqualTo, NotEqualTo, GreaterThan, GreaterThanOrEqualTo, LessThan, LessThanOrEqualTo | DateTime   |
| Email   | Email addresses for the user   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Manager   | Distinguished name of the account for the user's manager   | EqualTo   | String   |
| MemberOf   | Distinguished names of groups that this user is a member of   | EqualTo   | String   |
| Mobile Phone   | User's mobile telephone number   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Pager   | User's pager telephone number   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith  | String   |
| Password Never Expires   | User's password never expires   | EqualTo, NotEqualTo  | Boolean   |
| Notes   | General notes about the user   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Office   | User's office location   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith  | String   |
| Post Office Box   | User's post office box number   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Postal Code   | User's postal code or zip code   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Profile Path   | Path to the location for the user's profile   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Sam Account Name   | Logon name to support earlier versions of the operating system   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Logon Script   | Path and name of the sign-in script for the account   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| State or Province   | User's state or province   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Street Address   | User's street address   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Phone Number   | User's telephone number   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| RDS Allow Logon   | Whether the user is allowed to sign in to Remote Desktop Services   | EqualTo, NotEqualTo   | Boolean   |
| RDS Broken Connection Action | Action to take when a Remote Desktop Services session limit is reached   | EqualTo, NotEqualTo   | Boolean   |
| RDS Connect Client Drives   | Whether to reconnect to mapped client drives when user signs in to a Remote Desktop Services session   | EqualTo, NotEqualTo   | Boolean   |
| RDS Connect Printer Drives   | Whether to reconnect to mapped client printers when user signs in to a Remote Desktop Services session   | EqualTo, NotEqualTo   | Boolean   |
| RDS Default To Main Printer  | Whether to print automatically to the client's default printer from a Remote Desktop Services session   | EqualTo, NotEqualTo   | Boolean   |
| RDS Home Directory   | Home directory for the user when they sign in to Remote Desktop Services   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| RDS Home Drive   | Home drive for the user when they sign in to Remote Desktop Services   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| RDS Initial Program   | Path and file name of the application to start automatically when the user signs in to the Remote Desktop Services   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| RDS Max Connection Time   | Maximum duration, in minutes, of a Remote Desktop Session for the user   | EqualTo, NotEqualTo, GreaterThan, GreaterThanOrEqualTo, LessThan, LessThanOrEqualTo | Int32   |
| RDS Max Disconnection Time   | Maximum amount of time, in minutes, that a disconnected Remote Desktop Services session remains active for the user   | EqualTo, NotEqualTo, GreaterThan, GreaterThanOrEqualTo, LessThan, LessThanOrEqualTo | Int32   |
| RDS Max Idle Time   | Maximum amount of time, in minutes, that a Remote Desktop Services session can remain idle for the user   | EqualTo, NotEqualTo, GreaterThan, GreaterThanOrEqualTo, LessThan, LessThanOrEqualTo | Int32   |
| RDS Profile Path   | Roaming or mandatory profile path to use when the user signs in to Remote Desktop Services   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| RDS Reconnection Action   | Whether the user is allowed to reconnect to a disconnected Remote Desktop Services session   | EqualTo, NotEqualTo   | Boolean   |
| RDS Remote Control   | Whether to allow remote observation or remote control of the user's Remote Desktop Services session   | EqualTo, NotEqualTo, GreaterThan, GreaterThanOrEqualTo, LessThan, LessThanOrEqualTo | Int32   |
| RDS Work Directory   | Working directory path for the user in a Remote Desktop Session   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Title   | User's job title   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| User Principal Name   | UPN that is an Internet-style sign-in name for a user based on the Internet standard RFC 822 | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |
| Modification Date   | Date the user account was last changed   | EqualTo, NotEqualTo, GreaterThan, GreaterThanOrEqualTo, LessThan, LessThanOrEqualTo | DateTime   |
| Creation Date   | Date and time that the account was created   | EqualTo, NotEqualTo, GreaterThan, GreaterThanOrEqualTo, LessThan, LessThanOrEqualTo   | DateTime   |
| Web Page   | User's primary web page   | EqualTo, NotEqualTo, Contains, DoesNotContain, EndsWith, StartsWith   | String   |

## [Get User published data](#tab/get-user-published-data)

| Element   | Description   | Valid values |
|:---|:---|:---|
| Account Expires   | Date that the account expires   | DateTime   |
| Count   | Number of groups returned by this activity   | Integer   |
| Disabled   | Whether the account is currently disabled   | Boolean   |
| Expired   | Whether the account is currently expired   | Boolean   |
| Locked   | Whether the account is currently locked   | Boolean   |
| Account Never Expires   | Whether the account never expires   | Boolean   |
| City   | User's city   | String   |
| Common Name   | Name to identify the user   | String   |
| Company   | User's company name   | String   |
| Department   | User's department name in their company   | String   |
| Description   | Description of the user   | String   |
| Display Name   | Display name for the user   | String   |
| Distinguished Name   | Distinguished name that uniquely identifies the user account   | String   |
| Fax Number   | User's fax number   | String   |
| First Name   | User's first name   | String   |
| Home Directory   | Home directory for the user account   | String   |
| Home Drive   | Drive letter to which to map the UNC path specified by homeDirectory   | String   |
| Home Phone   | User's home telephone number   | String   |
| Initials   | Initials of the user's name   | String   |
| Last Name   | User's last name   | String   |
| Lockout Time   | Date and time that the account was locked out   | DateTime   |
| Email   | Email addresses for the user   | String   |
| Manager   | Distinguished name of the account for the user's manager   | String   |
| Mobile Phone   | User's mobile telephone number   | String   |
| Pager   | User's pager telephone number   | String   |
| Password Expired   | Whether the password is expired   | Boolean   |
| Password Last Set   | Date and time that the password was last set   | DateTime   |
| Password Never Expires   | User's password never expires   | Boolean   |
| Notes   | General notes about the user   | String   |
| Office   | User's office location   | String   |
| Post Office Box   | User's post office box number   | String   |
| Postal Code   | User's postal code or zip code   | String   |
| Profile Path   | Path to the location for the user's profile   | String   |
| Sam Account Name   | Sign-in name to support earlier versions of the operating system   | String   |
| Logon Script   | Path and name of the sign-in script for the account   | String   |
| State or Province   | User's state or province   | String   |
| Street Address   | User's street address   | String   |
| Phone Number   | User's telephone number   | String   |
| RDS Allow Logon   | User is allowed to sign in on to Remote Desktop Services   | Boolean   |
| RDS Broken Connection Action | Action to take when a Remote Desktop Services session limit is reached   | Boolean   |
| RDS Connect Client Drives   | Whether to reconnect to mapped client drives when user signs in to a Remote Desktop Services session   | Boolean   |
| RDS Connect Printer Drives   | Whether to reconnect to mapped client printers when user signs in to a Remote Desktop Services session   | Boolean   |
| RDS Default To Main Printer  | Whether to print automatically to the client's default printer from a Remote Desktop Services session   | Boolean   |
| RDS Home Directory   | Home directory for the user when they sign in to Remote Desktop Services   | String   |
| RDS Home Drive   | Home drive for the user when they sign in to Remote Desktop Services   | String   |
| RDS Initial Program   | Path and file names of the application to start automatically when the user signs in to the Remote Desktop Services   | String   |
| RDS Max Connection Time   | Maximum duration, in minutes, of a Remote Desktop Session for the user   | Int32   |
| RDS Max Disconnection Time   | Maximum amount of time, in minutes, that a disconnected Remote Desktop Services session remains active for the user | Int32   |
| RDS Max Idle Time   | Maximum amount of time, in minutes, that a Remote Desktop Services session can remain idle for the user   | Int32   |
| RDS Profile Path   | Roaming or mandatory profile path to use when the user signs in to Remote Desktop Services   | String   |
| RDS Reconnection Action   | Whether the user is allowed to reconnect to a disconnected Remote Desktop Services session   | Boolean   |
| RDS Remote Control   | Whether to allow remote observation or remote control of the user's Remote Desktop Services session   | Int32   |
| RDS Work Directory   | Working directory path for the user in a Remote Desktop Session   | String   |
| Runbook Server Name   | Name the runbook server that is running the search   | String   |
| Search Root   | Distinguished name of the node in the Active Directory Domain Services hierarchy where the search starts   | String   |
| Search Scope   | Scope of the search that is observed by the server; the options are Base, OneLevel, or SubTree   | String   |
| Title   | User's job title   | String   |
| User Cannot Change Password  | User can't change their password   | Boolean   |
| User Principal Name   | UPN that is an Internet-style sign-in name for a user based on the Internet standard RFC 822  | String   |
| Modification Date   | Date when the user account was last changed   | DateTime   |
| Creation Date   | Date and time when the account was created   | DateTime   |
| Web Page   | User's primary web page   | String   |


---
