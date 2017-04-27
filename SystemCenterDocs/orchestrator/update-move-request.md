---
title: Update Move Request
description: You can use the Update Move Request activity in a runbook to change the attributes of an existing Move request, for an on-premise environment.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 835c5d91-79b8-4d0e-9cdf-89e472328608
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Update Move Request

Applies To: System Center 2016 - Orchestrator

You can use the Update Move Request activity in a runbook to change the attributes of an existing Move request, for an on-premise environment.

The following tables list the required properties, optional properties, and published data for this activity.

## Required properties for Update Move Request activity

| **Element** | **Description**   | **Valid values** |
|:---|:---|:---|
| Identity   | Specifies the identity of the mailbox or mail user. It can be one of the following values:<br>GUID<br>Distinguished name (DN)<br>Domain\\Account <br>User principal name (UPN)<br>LegacyExchangeDN<br>SMTP address<br>Alias | String   |

## Optional properties for Update Move Request activity

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Accept Large Data Loss   | Specifies that a large amount of data loss is acceptable if the Bad Item Limit is set to 51 or higher. Items are considered corrupted if the item cannot be read from the source database or cannot be written to the target database. Corrupted items will not be available in the destination mailbox or in the .pst file.   | True, False   |
| Bad Item Limit   | Specifies the number of bad items to skip if the request encounters corruption in the mailbox. Use 0 (zero) to not skip bad items. The valid input range for this property is from 0 (zero) through 2147483647. The default value is 0 (zero). We suggest that you keep the default value 0 and only change the Bad Item Limit property value if the request fails.<br>If you set the Bad Item Limit property to more than 50, the command fails, and you receive a warning that states: "Please confirm your intention to accept a large amount of data loss by specifying Accept Large Data Loss." If you receive this warning, you need to run the command again. This time, run command by using the Accept Large Data Loss property. No further warnings appear, and any corrupted items are not available after the process is complete. | String   |
| Batch Name   | Specifies a descriptive name for moving a batch of mailboxes. The name can then be used in the Batch Name property as a search string for the Get Move Request mode.   | String   |
| Domain Controller   | Specifies the fully qualified domain name (FQDN) of the domain controller that writes this configuration change to Active Directory.   | String   |
| Ignore Rule Limit Errors   | Specifies that the command does not move the user's rules to the target server that runs Exchange.<br>Default value is True, when selected.   | True, False   |
| Remote Credential User Name   | Specifies the user name for an administrator who has permission to perform the mailbox move.   | String   |
| Remote Credential Password   | Specifies the password for an administrator who has permission to perform the mailbox move.   | String   |
| Remote Global Catalog   | Specifies the fully qualified domain name (FQDN) of the global catalog server for the remote forest.   | String   |
| Remote Host Name   | Specifies the FQDN of the cross-forest organization from which you're moving the mailbox.   | String   |
| Suspend When Ready To Complete | Specifies whether to suspend the move request before it reaches the status of CompletionInProgress. After the move is suspended, it has a status of AutoSuspended. The move can then be manually completed by using the Resume-MoveRequest command.<br>You can only use the Suspend When Ready To Complete property to move online mailboxes and to move mailboxes from Exchange Server 2007 or Exchange 2010 mailbox databases. You can't use this property to move offline mailboxes or to move mailboxes from Exchange Server 2003 mailbox databases. <br>Default value is True, when selected.   | True, False   |

## Published data for Update Move Request activity

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Exchange Environment   | Indicates the type of Exchange environment where this activity will be executed.   | String   |
| Exchange PowerShell Application | Specifies the application name segment of the connection URI.   | String   |
| Exchange Server Host   | Specifies the connected Exchange server.   | String   |
| Exchange Server Port   | Specifies the connected Exchange server port.   | String   |
| Exchange User Name   | Specifies the username used to connect to Exchange server.   | String   |
| Identity   | Specifies the identity of the mailbox or mail user.   | String   |
| Skip CA Check   | Indicates whether the client validates that the server certificate is signed by a trusted certification authority (CA) when connecting over Hypertext Transfer Protocol, over Secure Socket Layer. | String   |
| Skip CN Check   | Indicates whether the client validates that the certificate common name (CN) of the server matches the hostname of the server.   | String   |
| Skip Revocation Check   | Indicates whether the connection does not validate the revocation status of the server certificate.   | String   |
| Use SSL   | Indicates whether the SSL encryption is used.   | String   |

## Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)

