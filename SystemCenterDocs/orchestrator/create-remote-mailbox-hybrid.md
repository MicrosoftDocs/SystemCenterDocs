---
title: Create Remote Mailbox (Hybrid)
description: You can use the Create Remote Mailbox (Hybrid) activity to create a mail-enabled user in on-premises Active Directory and Exchange.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 3ac940c2-52e1-41a1-90f3-532edb575fbe
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Create Remote Mailbox (Hybrid)

You can use the Create Remote Mailbox (Hybrid) activity to create a mail-enabled user in on-premises Active Directory and Exchange. An associated mailbox is also created in the cloud-based service (hybrid environment).

The following tables list the required properties, optional properties, and published data for this activity.

## Required properties for Create Remote Mailbox (Hybrid)

| **Element**   | **Description**   | **Valid Values** |
|:---|:---|:---|
| Alias   | The email alias of the user and its associated mailbox in the service to be created with this activity. <br>The alias can be a combination of characters separated by a period with no intervening spaces. Do not use special characters in the alias. | String   |
| Name   | Specifies the common name (CN) of the on-premises mail-enabled user and its associated mailbox in the service.   | String   |
| User Principal Name | Specifies a system user name in an email address format (for example, ed@contoso.com).   | String   |

## Optional properties for Create Remote Mailbox (Hybrid)

| **Element**   | **Description**   | **Valid Values**   |
|:---|:---|:---|
| Account Disabled   | Indicates whether to create the mail-enabled user in a disabled state. <br>Default is True, when selected.   | True, False   |
| Archive   | Indicates whether to create an archive mailbox in the service in addition to the mailbox that is created in the service by this activity.<br>Default is True, when selected.   | True, False   |
| Display Name   | Specifies the name that will be displayed in Microsoft Outlook for the mail user and its associated mailbox in the service.   | String   |
| Domain Controller   | Specifies the fully qualified domain name (FQDN) of the domain controller that writes this configuration change to Active Directory.   | String   |
| Equipment   | Indicates whether the mailbox in the service should be created as an equipment resource mailbox. This property cannot be set to True when Room property is also set to True.<br>Default is True, when selected.   | True, False   |
| First Name   | Specifies the first name of the new user.   | String   |
| Immutable ID   | This property is used by GAL Synchronization (GALSync). It specifies a unique and immutable identifier in the form of an SMTP address for an Exchange mailbox that is used for federated delegation when requesting Security Assertion Markup Language (SAML) tokens. <br>If federation is configured for this mailbox and this property is not configured when creating the mailbox, Exchange will create the value for the immutable identifier based upon the mailbox's ExchangeGUID and the federated account namespace. For example: 7a78e7c8-620e-4d85-99d3-c90d90f29699@mail.contoso.com. <br>The Immutable ID property must be configured if Active Directory Federation Services (AD FS) is deployed to allow single sign-on into an off-premises mailbox and AD FS is configured to use a different attribute than ExchangeGUID for sign-on token requests. Exchange and AD FS must both request the same token for the same user to ensure proper functionality for a cross-premise Exchange deployment scenario. | String   |
| Initials   | The initials of the user that you create.   | String   |
| Last Name   | The last name of the user that you create.   | String   |
| Moderated By   | This property identifies the users who are responsible for moderating the messages sent to this mail user and its associated mailbox in the service. To designate more than one moderating user, separate the users with commas.<br>This property is required when the Moderation Enabled property is True. If this property is not configured and a user is already specified as the manager of this mail user, the Moderated By property is automatically set by use of the Managed By property of the mail user. Otherwise, an error is returned.   | String   |
| Moderation Enabled   | Specifies whether to enable moderation for the mail user. <br>Default is True, when selected.   | True, False   |
| On-Premises Organizational Unit | Specifies the organizational unit (OU) in the on-premises organization in which the new mailbox is added. This property has no effect on the mailbox in the service.   | String   |
| Password   | Specifies the password used by the mail user to secure his or her account and the associated mailbox in the service.   | String   |
| Password Confirm   | This property is used to confirm the password.   | String   |
| Primary SMTP Address   | Specifies the primary SMTP address for the mail user. By default, the primary SMTP address is generated based on the default email address policy. If you specify a primary SMTP address by using this property, the command sets the EmailAddressPolicyEnabled attribute of the mail user to False, and the email addresses of this mail user will not be automatically updated per email address policies.   | String   |
| Remote Power Shell Enabled   | Specifies whether the new mailbox user can use Remote PowerShell. Remote PowerShell is required to open the Exchange Management Shell or the Exchange Management Console on Mailbox, Hub Transport, Unified Messaging, and Client Access servers. Access to Remote PowerShell is required even to open the Shell or the console on the local server. <br>Default is True, when selected.   | True, False   |
| Remote Routing Address   | Specifies the SMTP address of the user's associated mailbox in the service.<br>If you have configured mail flow between the on-premises organization and the service, you do not need to specify this property. The remote routing address is calculated automatically.   | String   |
| Reset Password On Next Logon   | Specifies whether the password in the Password property must be reset the next time the user logs on.<br>Default is True, when selected.   | True, False   |
| Room   | Indicates whether the mailbox in the service should be created as a room resource mailbox. <br>This property cannot be set to True when the Equipment property is also set to True.<br>Default is True, when selected.   | True, False   |
| SAM Account Name   | This is the logon name for clients and servers running older versions of the operating system. This attribute must contain fewer than 20 characters. An account name can contain letters, numbers, and the following punctuation marks and symbols: <br>! \# $ % ^ & - . \_ { } | ~   | String   |
| Send Moderation Notifications   | Specifies how status notifications are sent to users when someone sends a message to the moderated distribution group. <br>Set this property to Always if you want notifications to be sent to all senders.<br>Set this property to Internal if you want notifications to be sent only to the senders who are internal to your organization.<br>Set this property to Never to disable all status notifications.<br>The default value is blank.<br>The sender is always notified if the message is rejected by the moderators, regardless of the value of this property.   | Always <br>Internal <br>Never |

## Published data for Create Remote Mailbox (Hybrid)

| **Element**   | **Description**   | **Valid Values** |
|:---|:---|:---|
| Accept Messages Only From   | Specifies mailbox users and mail-enabled contacts that can send email messages to this distribution group.   | String   |
| Accept Messages Only From DL Members   | Specifies distribution lists that are allowed to send email messages to this mailbox.   | String   |
| Accept Messages Only From Senders Or Members | Specifies senders or members that are allowed to send email messages to this distribution group.   | String   |
| Address List Membership   | Specifies address lists of which this mailbox is a member.   | String   |
| Alias   | Mail nickname of the user.   | String   |
| Arbitration Mailbox   | Specifies the mailbox that is used to manage the moderation process.   | String   |
| Archive Database   | Archive mailbox database.   |   |
| Archive GUID   | Archive mailbox identifier.   | String   |
| Archive Name   | Archive mailbox name.   | String   |
| Archive Quota   | Archive mailbox Quota parameter.   | String   |
| Archive Status   | Indicates archive status (Active or None).   | String   |
| Archive Warning Quota   | Mailbox size at which a size quota warning message is sent.   | String   |
| Bypass Moderation From Senders Or Members   | Lists Senders or Members whose messages are not subject to approval.   | String   |
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
| Disabled Archive Database   | The identity of the disabled archive database.   | String   |
| Disabled Archive GUID   | GUID of the disabled archive.   | String   |
| Display Name   | Content of the Simple Display Name field.   | String   |
| Distinguished Name   | Exchange's legacy distinguished name.   | String   |
| Email Address Policy Enabled   | Indicates whether the use of Address Policies is enabled.   | String   |
| Email Addresses   | Collection of email addresses for the mailbox.   | String   |
| End Date For Retention Hold   | End date of the Retention Hold period.   | String   |
| Exchange Environment   | Indicates the type of Exchange environment where this activity will be executed. The default for this property is On-Premises.   | String   |
| Exchange GUID   | Globally unique identifier of the Microsoft Exchange installation.   | String   |
| Exchange PowerShell Application   | Specifies the application name segment of the connection URI.   | String   |
| Exchange Server Host   | The connected host Exchange server.   | String   |
| Exchange Server Port   | The connected port on the Exchange server.   | String   |
| Exchange User Account Control   | This property is a mask that can be used to retrieve the user account control flags associated with this mailbox. This can be one of the following values:<br>AccountDisabled <br>CannotChangePassword <br>DoNotExpirePassword <br>DoNotRequirePreauthentication <br>EncryptedTextPasswordAllowed <br>HomeDirectoryRequired <br>InterDomainTrustAccount <br>Lockout <br>MnsLogonAccount <br>None <br>NormalAccount <br>NotDelegated <br>PasswordExpired <br>PasswordNotRequired <br>Script <br>ServerTrustAccount <br>SmartCardRequired <br>TemporaryDuplicateAccount <br>TrustedForDelegation <br>TrustedToAuthenticateForDelegation <br>UseDesKeyOnly <br>WorkstationTrustAccount | String   |
| Exchange User Name   | Username used to log on to Exchange server.   | String   |
| Exchange Version   | Version of the Exchange server.   | String   |
| Extension Custom Attribute 1   | Extension Custom Attribute 1.   | String   |
| Extension Custom Attribute 2   | Extension Custom Attribute 2.   | String   |
| Extension Custom Attribute 3   | Extension Custom Attribute 3.   | String   |
| Extension Custom Attribute 4   | Extension Custom Attribute 4.   | String   |
| Extension Custom Attribute 5   | Extension Custom Attribute 5.   | String   |
| Extensions   | Extension List.   | String   |
| External Directory Object Id   | The ID of the mailbox in the external directory.   | String   |
| Forwarding Address   | The Forwarding Address that is defined for the mailbox.   | String   |
| GUID   | Mailbox GUID.   | String   |
| Grant Send On Behalf To   | A list of users who are allowed to send messages on the owners behalf.   | String   |
| Has Picture   | Indicates whether a picture is associated with the mailbox.   | String   |
| Has Spoken Name   | Indicates whether a spoken name is associated with the mailbox.   | String   |
| Hidden From Address Lists Enabled   | Indicates whether mailbox information is hidden from address book.   | String   |
| Identity   | Mailbox identity.   | String   |
| Immutable ID   | Identifier for the mailbox that will never change.   | String   |
| Is Valid   | Indicates whether the object is configured correctly.   | String   |
| Last Exchange Changed Time   | Last Exchange changed time.   | Datetime   |
| Legacy Exchange DN   | Legacy Exchange DN.   | String   |
| Litigation Hold Date   | Date and time when litigation hold was enabled.   | Datetime   |
| Litigation Hold Enabled   | Indicates whether the mailbox is under a litigation hold.   | String   |
| Litigation Hold Owner   | User who enabled the litigation hold.   | String   |
| Mail Tip   | Mail tip.   | String   |
| Mail Tip Translations   | Mail tip translation list.   | String   |
| Mailbox Move Batch Name   | Name of the move batch that contains this mailbox.   | String   |
| Mailbox Move Flags   | Flags for a mailbox move. <br>This can be one of the following values: <br>CrossOrg<br>IntraOrg<br>MoveOnlyArchiveMailbox<br>MoveOnlyPrimaryMailbox<br>None<br>Offline<br>Protected<br>Pull<br>Push<br>RemoteLegacy<br>Suspend<br>SuspendWhenReadyToComplete   | String   |
| Mailbox Move Remote Host Name   | Name of the remote host that is participating in the move.   | String   |
| Mailbox Move Source MDB   | Active Directory identifier of the source database.   | String   |
| Mailbox Move Status   | Indicates the status of a mailbox move. This can be one of the following values:<br>AutoSuspended <br>Completed <br>CompletedWithWarning <br>CompletionInProgress <br>Failed <br>InProgress <br>None <br>Queued <br>Suspended   | String   |
| Mailbox Move Target MDB   | Active Directory identifier of the database to which the mailbox is being copied.   | String   |
| Max Receive Size   | Received message size limit.   | String   |
| Max Send Size   | Sent message size limit.   | String   |
| Moderated By   | List of users responsible for moderating this mailbox.   | String   |
| Moderation Enabled   | Indicates whether moderation is enabled for this mailbox.   | String   |
| Name   | Name associated with this object.   | String   |
| Object Category   | Active Directory object category for this mailbox.   | String   |
| Object Class   | List of Active Directory object classes which apply to this mailbox.   | String   |
| On-Premises Organizational Unit   | Organizational unit for this mailbox.   | String   |
| Organization ID   | Organization for this mailbox.   | String   |
| Originating Server   | Originating server.   | String   |
| Partner Object ID   | GUID for partner object.   | String   |
| Persisted Capabilities   | Persisted capability list.   | String   |
| Policies Excluded   | List of policies excluded.   | String   |
| Policies Included   | List of policies included.   | String   |
| Primary SMTP Address   | Primary SMTP address for the mailbox.   | String   |
| Protocol Settings   | Protocol settings used by the mailbox.   | String   |
| Recipient Limits   | Maximum number of recipients per message that this mailbox can send to.   | String   |
| Recipient Type   | Recipient type.   | String   |
| Recipient Type Details   | Recipient type details.   | String   |
| Reject Messages From   | Rejected sender IDs list.   | String   |
| Reject Messages From DL Members   | Rejected DL sender IDs list.   | String   |
| Reject Messages From Senders Or Members   | Rejected sender IDs list.   | String   |
| Remote Recipient Type   | Remote recipient type.   | String   |
| Remote Routing Address   | Specifies the SMTP address of the mailbox in the service that's associated with this mail-enabled user.   | String   |
| Require Sender Authentication Enabled   | Indicates whether sender authentication is required.   | String   |
| Retain Deleted Items For   | Length of time to keep deleted items.   | String   |
| Retention Comment   | Comment displayed regarding the user's retention hold status.   | String   |
| Retention Hold Enabled   | Indicates whether the contents of the mailbox are subject to retention.   | String   |
| Retention URL   | Retention policy that is applied to the mailbox.   | String   |
| SAM Account Name   | URL for a Web page with details about the organization's message retention policies.   | String   |
| Send Moderation Notifications   | Moderation notifications for this mailbox.   | String   |
| Simple Display Name   | Simple display name.   | String   |
| Single Item Recovery Enabled   | Indicates whether the Recovery Items folder can be purged.   | String   |
| Skip CA Check   | Indicates whether the client validates that the server certificate is signed by a trusted certification authority (CA) to connect over Hypertext Transfer Protocol over Secure Socket Layer.   | String   |
| Skip CN Check   | Indicates whether the client skips validation of whether the certificate common name (CN) of the server matches the hostname of the server.   | String   |
| Skip Revocation Check   | indicates whether the connection skips validation of the server certificate's revocation status.   | String   |
| Start Date For Retention Hold   | Date and time to begin a retention hold on messages in this mailbox.   | Datetime   |
| UM DTMF Map   | UM DTMF Map.   | String   |
| Use SSL   | Indicates whether SSL encryption is used.   | String   |
| User Principal Name   | Principal name for the mailbox user.   | String   |
| When Changed   | Date and time when the mailbox was changed.   | Datetime   |
| When Changed UTC   | UTC date and time when the mailbox was changed.   | Datetime   |
| When Created   | Date and time when the mailbox was created.   | Datetime   |
| When Created UTC   | UTC date and time when the mailbox was created   | Datetime   |
| When Mailbox Created   | Date and time when the mailbox was created   | Datetime   |
| Windows Email Address   | Email address.   | String   |

#### Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)
