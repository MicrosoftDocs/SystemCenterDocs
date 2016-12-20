---
title: Disable Remote Mailbox (Hybrid)
description: You can use the Disable Remote Mailbox (Hybrid) activity to remove a mailbox from the cloud-based service (hybrid environment).
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d21a4d11-f5ef-4948-a7bf-e4f58cc87b7f
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
Disable Remote Mailbox (Hybrid)
===============================

Applies To: System Center 2016 - Orchestrator

You can use the Disable Remote Mailbox (Hybrid) activity to remove a mailbox from the cloud-based service (hybrid environment). When you remove a mailbox with this activity, the associated user object in the on-premises Active Directory is not removed.

The following tables list the required properties, optional properties, and published data for this activity.

Required properties for Disable Remote Mailbox (Hybrid)
-------------------------------------------------------

| **Element** | **Description**   | **Valid values** |
|:---|:---|:---|
| Identity   | The identity of the Active Directory user whose remote mailbox will be disabled. This can be one of the following value types:<br>ADObjectID <br>GUID <br>Distinguished name (DN)<br>Domain\\SamAccountName<br>User principal name (UPN)<br>LegacyExchangeDN<br>Email Address<br>User alias | String   |

Optional properties for Disable Remote Mailbox (Hybrid)
-------------------------------------------------------

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Archive   | Indicates whether to disconnect the archive mailbox in the service from the associated mailbox in the service. <br>If you use this property, the on-premises mail-enabled user and its associated mailbox in the service are not removed.<br>Default is True, when selected.   | True, False   |
| Domain Controller   | Specifies the fully qualified domain name (FQDN) of the domain controller that writes this configuration change to Active Directory.   | String   |
| Ignore Default Scope | When configured and set to True, this property instructs the command to ignore the default recipient scope setting for the Exchange Management Shell session and to use the entire forest as the scope. This allows the command to access Active Directory objects that are not currently in the default scope. <br>If you use this property, you cannot use the Domain Controller property. The command automatically uses an appropriate global catalog server.<br>If you use this property, you can only use the DN for the Identity property. Other forms of identification, such as alias or GUID, are not accepted.<br>Default is True, when selected. | True, False   |
| Ignore Legal Hold   | If this element is configured and set to True, the command ignores the legal hold status of the mailbox user and allows you to disable the cloud mailbox that has been on legal hold.<br>When you disable a mailbox, the mailbox is disconnected from the user account. After you disable a mailbox, you cannot include it in a discovery search. Disconnected mailboxes are permanently deleted from the mailbox database after the deleted mailbox retention period expires. Check with your organization's legal or Human Resources department before you disable a mailbox that is on legal hold. <br>Default is True, when selected.   | True, False   |

Published data for Disable Remote Mailbox (Hybrid)
--------------------------------------------------

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Exchange Environment   | Indicates the type of Exchange environment where this activity will be executed. Default is On-Premise.   | String   |
| Exchange PowerShell Application | Specifies the application name segment of the connection URI.   | String   |
| Exchange Server Host   | The associated Exchange server host machine.   | String   |
| Exchange Server Port   | The associated Exchange server port.   | String   |
| Exchange User Name   | The username to log on to the Exchange server.   | String   |
| Identity   | The identity of the remote mailbox to be disabled.   | String   |
| Skip CA Check   | Indicates whether the client must validate that the server certificate is signed by a trusted certification authority (CA) when connecting over Hypertext Transfer Protocol over Secure Socket Layer. | String   |
| Skip CN Check   | Indicates whether the client must validate that the certificate common name (CN) of the server matches the hostname of the server.   | String   |
| Skip Revocation Check   | Indicates whether the connection does not check the revocation status of the server certificate.   | String   |
| Use SSL   | Indicates whether SSL encryption is used.   | String   |

#### Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)

