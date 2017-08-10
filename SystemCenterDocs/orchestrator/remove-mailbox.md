---
title: Remove Mailbox
description: You can use the Remove Mailbox activity to delete an existing mailbox and the Active Directory user that is associated with that mailbox, in an on-premise or online Exchange environment.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 57ac9277-f810-4efe-a8a4-dd01829113e7
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Remove Mailbox

> Applies To: System Center 2016 - Orchestrator

You can use the Remove Mailbox activity to delete an existing mailbox and the Active Directory user that is associated with that mailbox, in an on-premise or online Exchange environment. For an environment such as Microsoft Office 365 online, the Remove Mailbox activity can be used to delete a mailbox.

The following tables list the required properties, optional properties, and published data for this activity.

## Required properties for Remove Mailbox activity

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Mailbox ID   | Identifies the mailbox that is to be removed.<br>When Mailbox ID Type equals Identity, then<br>the Mailbox ID property accepts the following value types:<br>Alias. For example, JPhilips<br>Canonical DN. For example, Atlanta.Corp.Contoso.Com/Users/JPhilips<br>Display Name. For example, Jeff Philips<br>Distinguished Name (DN). For example, N=JPhilips,CN=Users,DC=Atlanta,DC=Corp,DC=contoso,DC=com<br>Domain\\Account. For example, Atlanta\\JPhilips<br>GUID. For example, fb456636-fe7d-4d58-9d15-5af57d0354c2<br>Immutable ID. For example, fb456636-fe7d-4d58-9d15-5af57d0354c2@contoso.com<br>Legacy Exchange DN. For example, /o=Contoso/ou=AdministrativeGroup/cn=Recipients/cn=JPhilips<br>SMTP Address. For example, Jeff.Philips@contoso.com<br>User Principal Name. For example, JPhilips@contoso.com<br>Use only the Mailbox ID property to disconnect the mailbox from the user and to remove the user object from Active Directory. The mailbox object still exists. By default, this mailbox remains in the Exchange database for 30 days, and then is deleted.<br>Use the Mailbox ID property in conjunction with the Permanent optional property to disconnect the mailbox from the user, remove the user object from Active Directory, and remove the mailbox object from the Exchange database. The mailbox object does not remain in the Exchange database as a disconnected mailbox.<br>When Mailbox ID Type equals StoreMailboxIdentity, then <br>the Mailbox ID property accepts the following value types:<br>Mailbox display name<br>GUID of the mailbox<br>LegacyExchangeDN<br>Use the Mailbox ID property in conjunction with the Database optional property when you have disconnected a mailbox from its associated user and want to remove the mailbox object from the Exchange database store. | String   |
| Mailbox ID Type | Specifies the type for the ID property.<br> <br><br><strong>Note </strong><br> The StoreMailboxIdentity value is available only in an on-premises environment. <br><br>   | Identity<br>StoreMailboxIdentity |

## Optional properties for Remove Mailbox activity

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Arbitration   | Specifies that the mailbox for which the command is executed is an arbitration mailbox. Arbitration mailboxes are used for managing approval workflow. For example, an arbitration mailbox is used for handling moderated recipients and distribution group membership approval.<br>Default is value True, when selected. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | True, False   |
| Database   | Specifies the database that contains the mailbox object to be removed.<br>This property accepts the following value types:<br>GUID<br>Database name<br>Use in conjunction with the StoreMailboxIdentity type when you have disconnected a mailbox from its associated user and want to remove the mailbox object from the Exchange store. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | String   |
| Domain Controller   | Specifies the fully qualified domain name (FQDN) of the domain controller that writes this configuration change to Active Directory. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | String   |
| Ignore Default Scope   | Instructs the command to ignore the default recipient scope setting for the Exchange Management Shell session and use the entire forest as the scope. This allows the command to access Active Directory objects that aren't currently in the default scope. <br>The Ignore Default Scope property introduces the following restrictions:<br>Domain Controller property cannot be used. The command uses an appropriate global catalog server automatically.<br>Only the DN for the Identity property can be used. Other forms of identification, such as alias or GUID, are not accepted.<br>Default value is True, when selected. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br> | True, False   |
| Ignore Legal Hold   | Ignores the legal hold status of the mail user and allows you to remove the mailbox that's on legal hold. After a mailbox is removed, it cannot be included in a discovery search. Depending on the configured properties, removed mailboxes are either purged immediately or when the deleted mailbox retention period expires. Check with your organization's policy or Human Resources department before you disable a mailbox that's on legal hold.<br>Default value is True, when selected. <br><br><strong>Note </strong><br> This property is not available in the Live@edu environment. <br><br>   | True, False   |
| Keep Windows Live ID (Live@edu only)   | Preserves the Windows Live ID that's associated with the deleted mailbox. This property applies to objects in the cloud-based service. It is not available for on-premises deployments.<br>Default value is True, when selected. <br><br><strong>Note </strong><br> This property is available only in the Live@edu environment. <br><br>   | True, False   |
| Permanent   | Use this in conjunction with the Identity type to specify whether to disconnect the mailbox from the user, to remove the associated user object from Active Directory, and to remove the mailbox object from the Exchange database. Default value is True, when selected. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | True, False   |
| Remove Last Arbitration Mailbox Allowed | Indicates whether it is allowed to remove the last Arbitration Mailbox.<br>Default value is True, when selected. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | True or<br>False |

## Published data for Remove Mailbox activity

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Exchange Environment   | Indicates the type of Exchange environment where this activity will be executed.   | String   |
| Exchange PowerShell Application | Specifies the application name segment of the connection URI.   | String   |
| Exchange Server Host   | Connected Exchange Server.   | String   |
| Exchange Server Port   | Connected Exchange Server port.   | String   |
| Exchange User Name   | Username that is used to connect to Exchange Server.   | String   |
| Mailbox ID   | Identity of the mailbox or mail user.   | String   |
| Skip CA Check   | Indicates whether the client validates that the server certificate is signed by a trusted certification authority (CA) when connecting over Hypertext Transfer Protocol over Secure Socket Layer. | String   |
| Skip CN Check   | Indicates whether the client validates that the certificate common name (CN) of the server matches the hostname of the server.   | String   |
| Skip Revocation Check   | Indicates whether the connection does not validate the revocation status of the server certificate.   | String   |
| Use SSL   | Indicates whether SSL encryption is used.   | String   |
