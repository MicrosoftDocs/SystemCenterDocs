---
title: Create User
description: You can use the Create User activity in a runbook to create a user in the Microsoft Active Directory.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bc69c0d8-bcbb-4b59-b1b1-03a4b0a33d8d
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Create User

Applies To: System Center 2016 - Orchestrator

You can use the Create User activity in a runbook to create a user in the Microsoft Active Directory.

This activity publishes all of the data from the required and optional properties into published data except user password. Additional published data is generated based on the class that you select when you define the activity.

The following tables list the required and optional properties and published data for this activity.

## Required properties for Create User activity

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Common Name | Name to identify the user | String   |

## Optional properties for Create User activity

| Element   | Description   | Valid Values |
|:---|:---|:---|
| Account Expires   | The date when the account expires   | DateTime   |
| Account Never Expires   | Specifies that the account never expires   | Boolean   |
| City   | User's city   | String   |
| Company   | User's company name   | String   |
| Container Distinguished Name | Distinguished name of the container where the user is located   | String   |
| Department   | User's department name in their company   | String   |
| Description   | Description for the user   | String   |
| Display Name   | Displays the name of the user   | String   |
| Fax Number   | User's fax number   | String   |
| First Name   | User's first name   | String   |
| Home Directory   | Home directory for the user account   | String   |
| Home Drive   | Specifies the drive letter to which the UNC path specified by home Directory will be mapped   | String   |
| Home Phone   | User's home telephone number   | String   |
| Initials   | Initials of the user's name   | String   |
| Last Name   | User's last name   | String   |
| Email   | Email address for the user   | String   |
| Manager   | Distinguished name of the account for the user's manager   | String   |
| Mobile Phone   | User's mobile telephone number   | String   |
| Pager   | User's pager telephone number   | String   |
| Password   | Password for the user   | String   |
| Password Never Expires   | Specifies that the user's password never expires   | Boolean   |
| Notes   | General notes about the user's telephone   | String   |
| Office   | User's office location   | String   |
| Post Office Box   | User's post office box number   | String   |
| Postal Code   | User's postal code or zip code   | String   |
| Profile Path   | Path to the location for the user's profile   | String   |
| Logon Script   | Path and name of the logon script for the account   | String   |
| State or Province   | User's state or province   | String   |
| Street Address   | User's street address   | String   |
| Phone Number   | User's telephone number   | String   |
| RDS Allow Logon   | Specifies whether the user is allowed to log on to Remote Desktop Services   | Boolean   |
| RDS Broken Connection Action | Specifies the action to take when a Remote Desktop Services session limit is reached   | Boolean   |
| RDS Connect Client Drives   | Specifies whether to reconnect to mapped client drives when a user logs on to a Remote Desktop Services session   | Boolean   |
| RDS Connect Printer Drives   | Specifies whether to reconnect to mapped client printers when a user logs on to a Remote Desktop Services session   | Boolean   |
| RDS Default To Main Printer  | Specifies whether to print automatically to the client's default printer from a Remote Desktop Services session   | Boolean   |
| RDS Home Directory   | The Home directory for the user when they log on to Remote Desktop Services (RDS)   | String   |
| RDS Home Drive   | The Home drive for the user when they log on to Remote Desktop Services   | String   |
| RDS Initial Program   | The Path and file names of the application to start automatically when the user logs on to the Remote Desktop Services   | String   |
| RDS Max Connection Time   | The maximum duration, in minutes, of a Remote Desktop Session for the user   | Int32   |
| RDS Max Disconnection Time   | The maximum amount of time, in minutes, that a disconnected Remote Desktop Services session remains active for the user   | Int32   |
| RDS Max Idle Time   | The maximum amount of time, in minutes, that a Remote Desktop Services session can remain idle for the user   | Int32   |
| RDS Profile Path   | Roaming or mandatory profile path to use when the user logs on to Remote Desktop Services   | String   |
| RDS Reconnection Action   | Specifies whether the user is allowed to reconnect to a disconnected Remote Desktop Services session   | Boolean   |
| RDS Remote Control   | Specifies whether to allow remote observation or remote control of the user's Remote Desktop Services session   | Int32   |
| RDS Work Directory   | The working directory path for the user in a Remote Desktop Session   | String   |
| SAM Account Name   | The Security Accounts Manager (SAM) logon name used to support clients and servers running earlier versions of the operating system. | String   |
| Title   | User's job title   | String   |
| User Cannot Change Password  | Specifies that the user cannot change their password   | Boolean   |
| User Must Change Password   | Specifies that the user must change their password the next time they log on   | Boolean   |
| User Principal Name   | This attribute contains the UPN that is an Internet-style login name for a user based on the Internet standard RFC 822   | String   |
| Web Page   | User's primary web page   | String   |

## Published data for Create User activity

| Name   | Description   | Value Type |
|:---|:---|:---|
| Account Expires   | Date that the account expires   | DateTime   |
| Account Never Expires   | Specifies that account never expires   | Boolean   |
| City   | User's city   | String   |
| Common Name   | Name to identify the user   | String   |
| Company   | User's company name   | String   |
| Container Distinguished Name | Distinguished name of the container where the user is located   | String   |
| Container Path   | The parent container for the user   | String   |
| Department   | User's department name in their company   | String   |
| Description   | Description for the user   | String   |
| Display Name   | Displays the name of the user   | String   |
| Distinguished Name   | Displays the name for the user   | String   |
| Fax Number   | User's fax number   | String   |
| First Name   | User's first name   | String   |
| Home Directory   | The Home directory for the user account   | String   |
| Home Drive   | Specifies the drive letter to which the UNC path specified by homeDirectory will be mapped   | String   |
| Home Phone   | User's home telephone number   | String   |
| Initials   | Initials of the user's name   | String   |
| Last Name   | User's last name   | String   |
| Email   | Email address for the user   | String   |
| Manager   | Distinguished name of the account for the user's manager   | String   |
| Mobile Phone   | User's mobile telephone number   | String   |
| Pager   | User's pager telephone number   | String   |
| Password Never Expires   | Specifies that the user's password never expires   | Boolean   |
| Notes   | General notes about the user's telephone   | String   |
| Office   | User's office location   | String   |
| Post Office Box   | User's post office box number   | String   |
| Postal Code   | User's postal code or zip code   | String   |
| Profile Path   | The path to the location for the user's profile   | String   |
| Logon Script   | The path and name of the logon script for the account   | String   |
| State or Province   | User's state or province   | String   |
| Street Address   | User's street address   | String   |
| Phone Number   | User's telephone number   | String   |
| RDS Allow Logon   | Specifies whether the user is allowed to log on to Remote Desktop Services   | Boolean   |
| RDS Broken Connection Action | Specifies the action to take when a Remote Desktop Services session limit is reached   | Boolean   |
| RDS Connect Client Drives   | Specifies whether to reconnect to the mapped client drives when user logs on to a Remote Desktop Services session   | Boolean   |
| RDS Connect Printer Drives   | Specifies whether to reconnect to the mapped client printers when user logs on to a Remote Desktop Services session   | Boolean   |
| RDS Default To Main Printer  | Specifies whether to print automatically to the client's default printer from a Remote Desktop Services session   | Boolean   |
| RDS Home Directory   | The Home directory for the user when they log on to Remote Desktop Services   | String   |
| RDS Home Drive   | The Home drive for the user when they log on to Remote Desktop Services   | String   |
| RDS Initial Program   | Path and file names of the application to start automatically when the user logs on to the Remote Desktop Services   | String   |
| RDS Max Connection Time   | The maximum duration, in minutes, of a Remote Desktop Session for the user   | Int32   |
| RDS Max Disconnection Time   | The maximum amount of time, in minutes, that a disconnected Remote Desktop Services session remains active for the user   | Int32   |
| RDS Max Idle Time   | The maximum amount of time, in minutes, that a Remote Desktop Services session can remain idle for the user   | Int32   |
| RDS Profile Path   | Roaming or mandatory profile path to use when the user logs on to Remote Desktop Services   | String   |
| RDS Reconnection Action   | Specifies whether the user is allowed to reconnect to a disconnected Remote Desktop Services session   | Boolean   |
| RDS Remote Control   | Specifies whether to allow remote observation or remote control of the user's Remote Desktop Services session   | Int32   |
| RDS Work Directory   | The working directory path for the user in a Remote Desktop Session   | String   |
| SAM Account Name   | The Security Accounts Manager (SAM) logon name used to support clients and servers running earlier versions of the operating system. | String   |
| Title   | User's job title   | String   |
| User Cannot Change Password  | Specifies that the user cannot change their password   | Boolean   |
| User Must Change Password   | Specifies that the user must change their password the next time they log on.   | Boolean   |
| User Principal Name   | This attribute contains the UPN that is an Internet-style login name for a user based on the Internet standard RFC 822.   | String   |
| Web Page   | User's primary web page   | String   |
