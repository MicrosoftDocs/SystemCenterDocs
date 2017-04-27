---
title: Remove Remote Mailbox (Hybrid)
description: You can use the Remove Remote Mailbox activity to delete an existing remote mailbox.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: e13e25d3-2dc1-472d-807d-5a05daa062d7
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Remove Remote Mailbox (Hybrid)

> Applies To: System Center 2016 - Orchestrator

You can use the Remove Remote Mailbox activity to delete an existing remote mailbox.

The following tables list the required properties, optional properties, and published data for this activity.

## Required properties for Remove Remote Mailbox (Hybrid) activity

| **Element** | **Description**   | **Valid values** |
|:---|:---|:---|
| Identity   | Specifies the identity of the mailbox or mail user. It can be one of the following value types:<br>GUID<br>Distinguished name (DN)<br>Domain\\Account <br>User principal name (UPN)<br>LegacyExchangeDN<br>SMTP address<br>Alias | String   |

## Optional properties for Remove Remote Mailbox (Hybrid) activity

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Domain Controller   | Specifies the fully qualified domain name (FQDN) of the domain controller that writes this configuration change to Active Directory.   | String   |
| Ignore Default Scope | Instructs the command to ignore the default recipient scope setting for the Exchange Management Shell session and to use the entire forest as the scope. This allows the command to access Active Directory objects that are not currently in the default scope. <br>If you use the Ignore Default Scope property, you should be aware of the following restrictions:<br>Domain Controller property cannot be used. The command uses an appropriate global catalog server automatically.<br>Only the DN for the Identity property can be used. Other forms of identification, such as alias or GUID, are not accepted.<br>Default value is True, when selected. | True or<br>False |
| Ignore Legal Hold   | Ignores the legal hold status of the mail user and allows you to remove the mailbox that's on legal hold. After a mailbox is removed, it cannot be included in a discovery search. Depending on the configured properties, removed mailboxes are either purged immediately or when the deleted mailbox retention period expires. Check with your organization's policy or Human Resources department before you disable a mailbox that's on legal hold.<br>Default value is True, when selected.   | True or<br>False |

## Published data for Remove Remote Mailbox (Hybrid) activity

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Exchange Environment   | Indicates the type of Exchange environment where this activity will be executed.   | String   |
| Exchange PowerShell Application | Specifies the application name segment of the connection URI.   | String   |
| Exchange Server Host   | Specifies the connected Exchange Server.   | String   |
| Exchange Server Port   | Specifies the connected Exchange Server port.   | String   |
| Exchange User Name   | Username used to connect to Exchange Server.   | String   |
| Identity   | Identity of the mailbox or mail user.   | String   |
| Skip CA Check   | Indicates whether the client validates that the server certificate is signed by a trusted certification authority (CA) when connecting over Hypertext Transfer Protocol, over Secure Socket Layer. | String   |
| Skip CN Check   | Indicates whether the client validates that the certificate common name (CN) of the server matches the hostname of the server.   | String   |
| Skip Revocation Check   | Indicates whether the connection does not validate the revocation status of the server certificate.   | String   |
| Use SSL   | Indicates whether SSL encryption is used.   | String   |
