---
title: Enable Remote Mailbox (Hybrid)
description: You can use the Enable Remote Mailbox (Hybrid) activity to create a mailbox in the cloud-based service for an existing user in the on-premises Active Directory (hybrid environment).
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cb690bb4-e07e-4a9f-9f19-2886c9a8fec4
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Enable Remote Mailbox (Hybrid)

Applies To: System Center 2016 - Orchestrator

You can use the Enable Remote Mailbox (Hybrid) activity to create a mailbox in the cloud-based service for an existing user in the on-premises Active Directory (hybrid environment).

The following tables list the required properties, optional properties, and published data for this activity.

## Required properties for Enable Remote Mailbox (Hybrid)

| **Element** | **Description**   | **Valid values** |
|:---|:---|:---|
| Identity   | The identity of the Active Directory user. This element can be one of the following value types:<br>ADObjectID <br>GUID <br>Distinguished name (DN)<br>Domain\\SamAccountName <br>User principal name (UPN)<br>LegacyExchangeDN<br>User alias | String   |

## Optional properties for Enable Remote Mailbox (Hybrid)

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Alias   | Specifies the alias of the user and the associated mailbox in the service. An alias can contain letters, numbers, and the following punctuation marks and symbols: <br>! \# $ % ^ & \* + - . / = ? \_ { } | ~   | String   |
| Archive   | Specifies whether to create an archive mailbox for the specified user. Default is True, when selected.   | True, False   |
| Archive Name   | Specifies the name of the archive mailbox. Use this property to change the name of the archive.   | String   |
| Display Name   | Specifies the display name for the mailbox that is created in the service.   | String   |
| Domain Controller   | Specifies the fully qualified domain name (FQDN) of the domain controller that writes this configuration change to Active Directory.   | String   |
| Equipment   | Specifies the new mailbox as equipment if this mailbox is a resource mailbox.<br>Default is True, when selected.   | True, False   |
| Primary SMTP Address   | Primary SMTP address for the mailbox.   | String   |
| Room   | Specifies the new mailbox as a room, if this mailbox is a resource mailbox. Default is True, when selected.   | True, False   |
| Remote Routing Address | Specifies the SMTP address of the mailbox in the service that this user is associated with.<br>If you have configured mail flow between the on-premises organization and the service, you do not need to specify this property. The remote routing address is calculated automatically. | String   |

## Published data for Enable Remote Mailbox (Hybrid)

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Accept Messages Only From   | Mailbox users and mail-enabled contacts from whom this mailbox will accept messages.   | String   |
| Accept Messages Only From DL Members   | Distribution lists from whom this mailbox will accept messages.   | String   |
| Accept Messages Only From Senders Or Members | Senders or members from whom this mailbox will accept messages.   | String   |
| Address List Membership   | The address lists of which this mailbox is a member.   | String   |
| Alias   | Mail nickname of the user.   | String   |
| Arbitration Mailbox   | The mailbox that is used to manage the moderation process.   | String   |
| Archive Database   | Archive mailbox database.   |   |
| Archive GUID   | The archive mailbox identifier.   | String   |
| Archive Name   | The archive mailbox name.   | String   |
| Archive Quota   | The archive mailbox Quota parameter.   | String   |
| Archive Status   | The archive status (Active or None).   | String   |
| Archive Warning Quota   | Mailbox size at which a warning message is sent.   | String   |
| Bypass Moderation From Senders Or Members   | Senders or list members whose messages are not subject to approval.   | String   |
| Calendar Version Store Disabled   | Indicates whether changes to calendar items are logged.   | String   |
| Custom Attribute 1   | Custom attribute 1.   | String   |
| Custom Attribute 10   | Custom attribute 10.   | String   |
| Custom Attribute 11   | Custom attribute 11.   | String   |
| Custom Attribute 12   | Custom attribute 12.   | String   |
| Custom Attribute 13   | Custom attribute 13.   | String   |
| Custom Attribute 14   | Custom attribute 14.   | String   |
| Custom Attribute 15   | Custom attribute 15.   | String   |
| Custom Attribute 2   | Custom attribute 2.   | String   |
| Custom Attribute 3   | Custom attribute 3.   | String   |
| Custom Attribute 4   | Custom attribute 4.   | String   |
| Custom Attribute 5   | Custom attribute 5.   | String   |
| Custom Attribute 6   | Custom attribute 6.   | String   |
| Custom Attribute 7   | Custom attribute 7.   | String   |
| Custom Attribute 8   | Custom attribute 8.   | String   |
| Custom Attribute 9   | Custom attribute 9.   | String   |
| Deliver to Mailbox And Forward   | The forwarding address of the mailbox.   | String   |
| Disabled Archive Database   | ID of disabled archive database.   | String   |
| Disabled Archive GUID   | GUID of disabled archive.   | String   |
| Display Name   | The contents of the Simple Display Name field.   | String   |
| Distinguished Name   | Exchange's legacy distinguished name.   | String   |
| Email Address Policy Enabled   | Indicates whether the use of Address Policies is enabled.   | String   |
| Email Addresses   | Collection of email addresses for the mailbox.   | String   |
| End Date For Retention Hold   | End date of the Retention Hold period.   | Datetime   |
| Exchange Environment   | Indicates the type of Exchange Server environment where this activity will be executed. Default is On-Premises.   | String   |
| Exchange GUID   | Unique identifier of the Microsoft Exchange installation.   | String   |
| Exchange PowerShell Application   | The application name segment of the connection URI.   | String   |
| Exchange Server Host   | The connected host Exchange Server.   | String   |
| Exchange Server Port   | The connected Exchange Server port.   | String   |
| Exchange User Account Control   | Specifies a mask that is used to retrieve the user account control flags associated with this mailbox. This can be one of the following values:<br>AccountDisabled <br>CannotChangePassword <br>DoNotExpirePassword <br>DoNotRequirePreauthentication <br>EncryptedTextPasswordAllowed <br>HomeDirectoryRequired <br>InterDomainTrustAccount <br>Lockout <br>MnsLogonAccount <br>None <br>NormalAccount <br>NotDelegated <br>PasswordExpired <br>PasswordNotRequired <br>Script <br>ServerTrustAccount <br>SmartCardRequired <br>TemporaryDuplicateAccount <br>TrustedForDelegation <br>TrustedToAuthenticateForDelegation <br>UseDesKeyOnly <br>WorkstationTrustAccount | String   |
| Exchange User Name   | The username used to log on to the Exchange server.   | String   |
| Exchange Version   | Version of the Exchange Server.   | String   |
| Extension Custom Attribute 1   | Extension Custom Attribute 1.   | String   |
| Extension Custom Attribute 2   | Extension Custom Attribute 2.   | String   |
| Extension Custom Attribute 3   | Extension Custom Attribute 3.   | String   |
| Extension Custom Attribute 4   | Extension Custom Attribute 4.   | String   |
| Extension Custom Attribute 5   | Extension Custom Attribute 5.   | String   |
| Extensions   | Extension List.   | String   |
| External Directory Object Id   | ID of the mailbox in the external directory.   | String   |
| Forwarding Address   | Forwarding Address defined for the mailbox.   | String   |
| GUID   | Mailbox GUID.   | String   |
| Grant Send On Behalf to   | List of users who are allowed to send messages on the owner's behalf.   | String   |
| Has Picture   | Indicates whether a picture is associated with the mailbox.   | String   |
| Has Spoken Name   | Indicates whether a spoken name is associated with the mailbox.   | String   |
| Hidden from Address Lists Enabled   | Indicates whether mailbox information is hidden from address book.   | String   |
| Identity   | Mailbox identity.   | String   |
| Immutable ID   | Mailbox identifier that will never change.   | String   |
| Is Valid   | Indicates whether the object is configured correctly.   | String   |
| Last Exchange Changed Time   | Last Exchange changed time.   | String   |
| Legacy Exchange DN   | Legacy Exchange DN.   | String   |
| Litigation Hold Date   | Date and time when litigation hold was enabled.   | Datetime   |
| Litigation Hold Enabled   | Indicates whether the mailbox is under a litigation hold.   | String   |
| Litigation Hold Owner   | User who enabled the litigation hold.   | String   |
| Mail Tip   | Mail tip.   | String   |
| Mail Tip Translations   | List of mail tip translations.   | String   |
| Mailbox Move Batch Name   | Name of the move batch that contains this mailbox.   | String   |
| Mailbox Move Flags   | Flags for a mailbox move. This can be one of the following values: <br>CrossOrg<br>IntraOrg<br>MoveOnlyArchiveMailbox<br>MoveOnlyPrimaryMailbox<br>None<br>Offline<br>Protected<br>Pull<br>Push<br>RemoteLegacy<br>Suspend<br>SuspendWhenReadyToComplete   | String   |
| Mailbox Move Remote Host Name   | Name of the remote host that is participating in the move.   | String   |
| Mailbox Move Source MDB   | Active Directory identifier of the source database.   | String   |
| Mailbox Move Status   | Indicates the status of a mailbox move. This can be one of the following values:<br>AutoSuspended <br>Completed <br>CompletedWithWarning <br>CompletionInProgress <br>Failed <br>InProgress <br>None <br>Queued <br>Suspended   | String   |
| Mailbox Move Target MDB   | Active Directory identifier of the database that the mailbox is being copied to.   | String   |
| Max Receive Size   | Received message size limit.   | String   |
| Max Send Size   | Sent message size limit.   | String   |
| Moderated By   | List of users responsible for moderating this mailbox.   | String   |
| Moderation Enabled   | Indicates whether moderation is enabled for this mailbox.   | String   |
| Name   | Name associated with this object.   | String   |
| Object Category   | Active Directory object category for this mailbox.   | String   |
| Object Class   | List of Active Directory object classes that apply to this mailbox.   | String   |
| On Premises Organizational Unit   | Organizational unit for this mailbox.   | String   |
| Organization ID   | Organization for this mailbox.   | String   |
| Originating Server   | Originating server.   | String   |
| Partner Object ID   | GUID for partner object ID.   | String   |
| Persisted Capabilities   | Persisted capability list.   | String   |
| Policies Excluded   | List of policies that are excluded.   | String   |
| Policies Included   | List of policies that are included.   | String   |
| Primary SMTP Address   | Primary SMTP address for the mailbox.   | String   |
| Protocol Settings   | Protocols used by the mailbox.   | String   |
| Recipient Limits   | Maximum number of recipients per message that this mailbox can send to.   | String   |
| Recipient Type   | Recipient type.   | String   |
| Recipient Type Details   | Recipient type details.   | String   |
| Reject Messages From   | Rejected sender IDs list.   | String   |
| Reject Messages From DL Members   | Rejected sender IDs list.   | String   |
| Reject Messages From Senders or Members   | Rejected sender IDs list.   | String   |
| Remote Recipient Type   | Remote recipient type.   | String   |
| Remote Routing Address   | The SMTP address of the mailbox in the service that is associated with this mail-enabled user.   | String   |
| Require Sender Authentication Enabled   | Indicates whether sender authentication is required.   | String   |
| Retain Deleted Items For   | Length of time to keep deleted items.   | String   |
| Retention Comment   | The comment that is displayed regarding the user's retention hold status.   | String   |
| Retention Hold Enabled   | Indicates whether the contents of the mailbox are subject to retention.   | String   |
| Retention URL   | Retention policy that is applied to the mailbox.   | String   |
| SAM Account Name   | URL for a webpage with details about the organization's message retention policies.   | String   |
| Send Moderation Notifications   | Enable moderation notifications for this mailbox.   | String   |
| Simple Display Name   | Simple display name.   | String   |
| Single Item Recovery Enabled   | Indicates whether the Recovery Items folder can be purged.   | String   |
| Skip CA Check   | Indicates whether the client will skip validation that the server certificate is signed by a trusted certification authority (CA) when connecting over Hypertext Transfer Protocol (HTTP) over Secure Sockets Layer (SSL).   | String   |
| Skip CN Check   | Indicates whether the client will skip validation that the certificate common name (CN) of the server matches the hostname of the server.   | String   |
| Skip Revocation Check   | Indicates whether the connection will skip validation of the revocation status of the server certificate.   | String   |
| Start Date For Retention Hold   | Date and time that a retention hold on messages in this mailbox begins.   | Datetime   |
| UM DTMF Map   | UM DTMF Map.   | String   |
| Use SSL   | Indicates whether SSL encryption is used.   | String   |
| User Principal Name   | Principal name for the mailbox user.   | String   |
| When Changed   | Date and time when mailbox was changed.   | Datetime   |
| When Changed UTC   | UTC date and time when mailbox was changed.   | Datetime   |
| When Created   | Date and time when the mailbox was created.   | Datetime   |
| When Created UTC   | UTC date and time when the mailbox was created.   | Datetime   |
| When Mailbox Created   | Date and time when mailbox was created.   | Datetime   |
| Windows Email Address   | Email address.   | String   |

#### Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)

