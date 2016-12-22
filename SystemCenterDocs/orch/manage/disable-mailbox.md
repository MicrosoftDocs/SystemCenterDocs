---
title: Disable Mailbox
description: For an on-premises environment, you can use the Disable Mailbox activity in a runbook to disable the mailbox of an existing user or InetOrgPerson object and remove that object's Exchange attributes from Active Directory.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8ddd7efe-2342-4a53-95f9-887cdcd2e67f
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
Disable Mailbox
===============

Applies To: System Center 2016 - Orchestrator

For an on-premises environment, you can use the Disable Mailbox activity in a runbook to disable the mailbox of an existing user or InetOrgPerson object and remove that object's Exchange attributes from Active Directory. The user account associated with the disabled mailbox remains in Active Directory, but it is no longer associated with any mailbox. The disabled mailbox is not deleted. It can be reconnected to a user at a later time.

For an online cloud-based environment, the Disable Mailbox activity can be used with the Archive parameter to disable an archive for an existing mailbox.

The following tables list the required properties, optional properties, and published data for this activity.

Required properties for the Disable Mailbox activity
----------------------------------------------------

| **Element** | **Description**   | **Valid values** |
|:---|:---|:---|
| Identity   | The identity of the mailbox to be disabled. This can be of the following value types:<br>GUID <br>Distinguished name (DN)<br>Display name<br>Domain\\Account <br>User principal name (UPN)<br>LegacyExchangeDN<br>SmtpAddress<br>Alias | String   |

Optional properties for the Disable Mailbox activity
----------------------------------------------------

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Arbitration   | Indicates that the mailbox to be deleted is an arbitration mailbox. Arbitration mailboxes are used for managing approval workflow. For example, an arbitration mailbox can handle moderated recipients and distribution group membership approval.<br>Default is True, when selected. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | True, False   |
| Archive   | Indicates whether to disconnect the archive mailbox from the associated mailbox user. This property cannot be used with the Remote Archive property.<br>Default is True, when selected. <br><br><strong>Note </strong><br> This property is not available in the Live@edu environment. <br><br>   | True, False   |
| Disable Last Arbitration Mailbox Allowed | Specifies whether to disable the specified mailbox if it is the only arbitration mailbox in the organization. You must have at least one arbitration mailbox in the organization to enable user-created distribution groups or moderated recipient functionality.<br>Default is True, when selected. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | True, False   |
| Domain Controller   | The fully qualified domain name (FQDN) of the domain controller that writes this configuration change to Active Directory. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | String   |
| Ignore Default Scope   | When set to True, this property instructs the command to ignore the default recipient scope setting for the Exchange Management Shell session and to use the entire forest as the scope. This allows the command to access Active Directory objects that are not currently in the default scope. <br>Default is True, when selected. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br> When you use the **Ignore Default Scope** property, the **Domain Controller** property cannot be used. The command automatically uses an appropriate global catalog server.<br>When you use the **Ignore Default Scope** property, only the DN can be used for the **Identity** property. Other forms of identification, such as alias or GUID, are not accepted. | True, False   |
| Ignore Legal Hold   | When set to True, this property instructs the command to ignore the legal hold status of the mail user and allows it to remove the mailbox that has been on legal hold. After the mailbox is removed, it cannot be included in a discovery search. Depending on the configured properties, removed mailboxes are purged either immediately or when the deleted mailbox retention period expires. Check with your organization's legal or Human Resources department before disabling a mailbox that is on legal hold.<br>Default is True, when selected. <br><br><strong>Note </strong><br> This property is not available in the Office 365 environment. <br><br>   | True, False   |
| Remote Archive   | Specifies whether to disconnect the remote archive for this mailbox. When you enable this property, the RemoteRecipientType property for the mailbox is reset to indicate that this mailbox does not have a remote archive. A remote archive exists in a cloud-based service. This property cannot be used with the Archive property. <br>Default is True, when selected. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | True, False   |

Published data for the Disable Mailbox activity
-----------------------------------------------

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Exchange Environment   | Indicates the type of Exchange environment where this activity will be executed. Default is On-Premises.   | String   |
| Exchange PowerShell Application | The application name segment of the connection URI.   | String   |
| Exchange Server Host   | The associated Exchange server host machine.   | String   |
| Exchange Server Port   | The associated Exchange Server port.   | String   |
| Exchange User Name   | The username to log on to the Exchange server.   | String   |
| Identity   | Mailbox identity.   | String   |
| Skip CA Check   | Indicates whether the client skips the validation that the server certificate is signed by a trusted certification authority (CA) when connecting over Hypertext Transfer Protocol (HTTP) over Secure Sockets Layer (SSL). | String   |
| Skip CN Check   | Indicates whether the client skips validation that the certificate common name (CN) of the server matches the hostname of the server.   | String   |
| Skip Revocation Check   | Indicates whether the connection skips validation of the revocation status of the server certificate.   | String   |
| Use SSL   | Indicates whether SSL encryption is used.   | String   |

#### Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)

