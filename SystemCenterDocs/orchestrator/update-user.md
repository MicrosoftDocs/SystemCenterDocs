---
title: Update User
description: You can use the Update User activity in a runbook to update the properties of a user in the Microsoft Active Directory.
ms.custom: UpdateFrequency2, engagement-fy24
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: na
ms.suite: na
ms.subservice: orchestrator
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 2f5a4d2c-5b1d-4073-bc9f-1bf59a0d6384
author: jyothisuri
ms.author: jsuri
robots: noindex
---
# Update User

You can use the Update User activity in a runbook to update the properties of a user in Microsoft Active Directory.

This activity publishes all of the data from the required and optional properties into published data. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

## Required properties for Update User activity

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Distinguished Name | Relative distinguished name that uniquely identifies the user account | String   |

## Optional properties for Update User activity

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Account Expires   | Date that the account expires   | DateTime   |
| Account Never Expires   | Specifies that the account never expires   | Boolean   |
| City   | User's city   | String   |
| Company   | User's company name   | String   |
| Department   | User's department name in their company   | String   |
| Description   | Description of the user   | String   |
| Display Name   | Displays the name for the user   | String   |
| Fax Number   | User's fax number   | String   |
| First Name   | User's first name   | String   |
| Home Directory   | The Home directory for the user account   | String   |
| Home Drive   | Specifies the drive letter to which the UNC path specified by homeDirectory will be mapped   | String   |
| Home Phone   | User's home telephone number   | String   |
| Initials   | Initials of the user's name   | String   |
| Last Name   | User's last name   | String   |
| Email   | Email addresses for the user   | String   |
| Manager   | Distinguished name of the account for the user's manager   | String   |
| Mobile Phone   | User's mobile telephone number   | String   |
| Pager   | User's pager telephone number   | String   |
| Password Never Expires   | Specifies that the user's password never expires   | Boolean   |
| Notes   | General notes about the user's telephone   | String   |
| Office   | User's office location   | String   |
| Post Office Box   | User's post office box number   | String   |
| Postal Code   | User's postal code or zip code   | String   |
| Profile Path   | Path to the location for the user's profile   | String   |
| Logon Script   | Path and name of the sign-in script for the account   | String   |
| State or Province   | User's state or province   | String   |
| Street Address   | User's street address   | String   |
| Phone Number   | User's telephone number   | String   |
| RDS Allow Logon   | Specifies whether the user is allowed to sign in to Remote Desktop Services   | Boolean   |
| RDS Broken Connection Action | Specifies the action to take when a Remote Desktop Services session limit is reached   | Boolean   |
| RDS Connect Client Drives   | Specifies whether to reconnect to mapped client drives when user signs in to a Remote Desktop Services session   | Boolean   |
| RDS Connect Printer Drives   | Specifies whether to reconnect to mapped client printers when the user signs in to a Remote Desktop Services session   | Boolean   |
| RDS Default To Main Printer  | Specifies whether to print automatically to the client's default printer from a Remote Desktop Services session   | Boolean   |
| RDS Home Directory   | The Home directory for the user when they sign in to Remote Desktop Services   | String   |
| RDS Home Drive   | The Home drive for the user when they sign in to Remote Desktop Services   | String   |
| RDS Initial Program   | Path and file names of the application to start automatically when the user signs in to the Remote Desktop Services   | String   |
| RDS Max Connection Time   | Maximum duration, in minutes, of a Remote Desktop Session for the user   | Int32   |
| RDS Max Disconnection Time   | Maximum amount of time, in minutes, that a disconnected Remote Desktop Services session remains active for the user   | Int32   |
| RDS Max Idle Time   | Maximum amount of time, in minutes, that a Remote Desktop Services session can remain idle for the user   | Int32   |
| RDS Profile Path   | Roaming or mandatory profile path to use when the user signs in to Remote Desktop Services   | String   |
| RDS Reconnection Action   | Specifies whether the user is allowed to reconnect to a disconnected Remote Desktop Services session   | Boolean   |
| RDS Remote Control   | Specifies whether to allow remote observation or remote control of the user's Remote Desktop Services session   | Int32   |
| RDS Work Directory   | The working directory path for the user in a Remote Desktop Session   | String   |
| Title   | User's job title   | String   |
| User Cannot Change Password  | Specifies that the user can't change their password   | Boolean   |
| User Must Change Password   | Specifies that the user must change their password the next time they sign in.   | Boolean   |
| User Principal Name   | This attribute contains the UPN that is an Internet-style sign-in name for a user based on the Internet standard RFC 822 | String   |
| Web Page   | User's primary web page   | String   |

## Published data for Update User activity

| Name   | Description   | Value Type |
|:---|:---|:---|
| Account Expires   | Date that the account expires   | DateTime   |
| Account Never Expires   | Specifies that account never expires   | Boolean   |
| City   | User's city   | String   |
| Company   | User's company name   | String   |
| Department   | User's department name in their company   | String   |
| Description   | Description of the user   | String   |
| Display Name   | Displays the name for the user   | String   |
| Distinguished Name   | Relative distinguished name that uniquely identifies the user account   | String   |
| Fax Number   | User's fax number   | String   |
| First Name   | User's first name   | String   |
| Home Directory   | The Home directory for the user account   | String   |
| Home Drive   | Specifies the drive letter to which to map the UNC path specified by homeDirectory   | String   |
| Home Phone   | User's home telephone number   | String   |
| Initials   | Initials of the user's name   | String   |
| Last Name   | User's last name   | String   |
| Email   | Email addresses for the user   | String   |
| Manager   | Distinguished name of the account for the user's manager   | String   |
| Mobile Phone   | User's mobile telephone number   | String   |
| Pager   | User's pager telephone number   | String   |
| Password Never Expires   | Specifies that the user's password never expires   | Boolean   |
| Notes   | General notes about the user's telephone   | String   |
| Office   | User's office location   | String   |
| Post Office Box   | User's post office box number   | String   |
| Postal Code   | User's postal code or zip code   | String   |
| Profile Path   | Path to the location for the user's profile   | String   |
| Logon Script   | Path and name of the sign-in script for the account   | String   |
| State or Province   | User's state or province   | String   |
| Street Address   | User's street address   | String   |
| Phone Number   | User's telephone number   | String   |
| RDS Allow Logon   | Specifies whether the user is allowed to sign in to Remote Desktop Services   | Boolean   |
| RDS Broken Connection Action | Specifies the action to take when a Remote Desktop Services session limit is reached   | Boolean   |
| RDS Connect Client Drives   | Specifies whether to reconnect to mapped client drives when user signs in to a Remote Desktop Services session   | Boolean   |
| RDS Connect Printer Drives   | Specifies whether to reconnect to mapped client printers when user signs in to a Remote Desktop Services session   | Boolean   |
| RDS Default To Main Printer  | Specifies whether to print automatically to the client's default printer from a Remote Desktop Services session   | Boolean   |
| RDS Home Directory   | The Home directory for the user when they sign in to Remote Desktop Services   | String   |
| RDS Home Drive   | The Home drive for the user when they sign in to Remote Desktop Services   | String   |
| RDS Initial Program   | Path and file names of the application to start automatically when the user signs in to the Remote Desktop Services   | String   |
| RDS Max Connection Time   | Maximum duration, in minutes, of a Remote Desktop Session for the user   | Int32   |
| RDS Max Disconnection Time   | Maximum amount of time, in minutes, that a disconnected Remote Desktop Services session remains active for the user   | Int32   |
| RDS Max Idle Time   | Maximum amount of time, in minutes, that a Remote Desktop Services session can remain idle for the user   | Int32   |
| RDS Profile Path   | Roaming or mandatory profile path to use when the user signs in to Remote Desktop Services   | String   |
| RDS Reconnection Action   | Specifies whether the user is allowed to reconnect to a disconnected Remote Desktop Services session   | Boolean   |
| RDS Remote Control   | Specifies whether to allow remote observation or remote control of the user's Remote Desktop Services session   | Int32   |
| RDS Work Directory   | The working directory path for the user in a Remote Desktop Session   | String   |
| Title   | User's job title   | String   |
| User Cannot Change Password  | Specifies that the user can't change their password   | Boolean   |
| User Must Change Password   | Specifies that the user must change their password the next time they sign in.   | Boolean   |
| User Principal Name   | This attribute contains the UPN that is an Internet-style sign-in name for a user based on the Internet standard RFC 822 | String   |
| Web Page   | User's primary web page   | String   |
