---
title: Get Mailbox
description: You can use the Get Mailbox activity to retrieve the attributes and objects for a mailbox in an on-premises or online environment.
ms.custom: na
ms.date: 4/25/2017
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 1e5f6075-259b-426b-97c9-a934d155f665
author: cfreemanwa
ms.author: raynew
manager: carmonm
---

# Get Mailbox

You can use the Get Mailbox activity to retrieve the attributes and objects for a mailbox in an on-premises or online environment. The Get Mailbox activity lets you filter against various mailbox attributes.

The following tables list the required properties, filters, optional properties, and published data for this activity.

## Required properties for the Get Mailbox activity

This activity has no required properties.

## Filters for the Get Mailbox activity

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Accept Messages Only From   | Mailbox users and mail-enabled contacts that can send email messages to this distribution group.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Accept Messages Only From DL Members   | Distribution lists that are allowed to send email messages to this mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Accept Messages Only From Senders Or Members | Senders or members that are allowed to send email messages to this distribution group.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Address Book Policy   | Address book policy for the mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain <br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Address List Membership   | Address list IDs.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Alias   | Mail nickname of the user.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Admin Display Version   | The version of the administrator's display.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Antispam Bypass Enabled   | Indicates whether anti-spam processing is used on the mailbox.   | Equals<br>Does not equal   |
| Arbitration Mailbox   | ID of the arbitration mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Archive Database   | ID of the archive database.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Archive Domain   | Archive domain name.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Archive GUID   | Unique archive identifier for the mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Archive Name   | Name of the archive mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Archive Quota   | Maximum size of the archive mailbox. <br>Can This property value can be either "unlimited" or a string with <br>format &lt;integer&gt; &lt;unit&gt; where unit can be KB, MB, GB, or TB. Defaults to Byte when unit is not specified.<br>Examples: 55 GB, unlimited, 77, 14 KB   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| Archive Release   | Archive release.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Archive Status   | Indicates archive status (Active or None).   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Archive State   | Indicates the state of the mailbox archive. This can be one of the following values:<br>HostedPending <br>HostedProvisioned <br>Local<br>None <br>OnPremise   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Archive Warning Quota   | Mailbox size at which a warning message is sent. <br>This property can be either "unlimited" or a string with <br>format &lt;integer&gt; &lt;unit&gt; where unit can be KB, MB, GB, or TB. Defaults to Byte when unit is not specified.<br>Examples: 55 GB, unlimited, 77, 14 KB   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| Audit Admin   | List of admin operations that are logged. This can be one of the following values: <br>Copy<br>Create<br>FolderBind<br>HardDelete<br>MessageBind<br>Move<br>MoveToDeletedItems<br>None<br>SendAs<br>SendOnBehalf<br>SoftDelete<br>Update   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Audit Delegate   | List of delegate options that are logged. This can be one of the following values: <br>Copy<br>Create<br>FolderBind<br>HardDelete<br>MessageBind<br>Move<br>MoveToDeletedItems<br>None<br>SendAs<br>SendOnBehalf<br>SoftDelete<br>Update   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Audit Enabled   | Indicates whether audit logging is enabled or disabled for the mailbox.   | Equals<br>Does not equal   |
| Audit Log Age Limit   | Amount of time the audit log entries are retained in the mailbox.<br>Format: d.hh:mm:ss where d = days, h = hours, m = minutes, and s = seconds.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| Audit Owner   | List of owner operations that are logged. This can be one of the following values: <br>Copy<br>Create<br>FolderBind<br>HardDelete<br>MessageBind<br>Move<br>MoveToDeletedItems<br>None<br>SendAs<br>SendOnBehalf<br>SoftDelete<br>Update   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Bypass Moderation From Senders Or Members   | List of senders for whom moderation is to be bypassed.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Calendar Repair Disabled   | Indicates whether calendar items in this mailbox will be repaired by the Calendar Repair Assistant.   | Equals<br>Does not equal   |
| Calendar Version Store Disabled   | Indicates whether changes to calendar items are logged.   | Equals<br>Does not equal   |
| Custom Attribute 1 - 15   | Custom attribute values.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Database   | Active Directory ID of the database that contains this mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Default Public Folder Mailbox   | Default public folder mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Deliver To Mailbox And Forward   | Indicates whether messages sent to this mailbox are forwarded to another mailbox.   | Equals<br>Does not equal   |
| Disabled Archive Database   | ID of disabled archive database.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Disabled Archive GUID   | GUID of disabled archive.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Display Name   | Display name for the mailbox user.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Distinguished Name   | Distinguished name for the object.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Downgrade High Priority Messages Enabled   | Indicates whether high-priority messages that have been sent to an X.400 mail system are changed to normal priority.   | Equals<br>Does not equal   |
| Email Addresses   | The collection of email addresses for the mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Email Address Policy Enabled   | Indicates whether Email Address Policy is enabled.   | Equals<br>Does not equal   |
| End Date For Retention Hold   | Date and time that a retention hold on messages in this mailbox expires.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| Exchange GUID   | Unique identifier of the Microsoft Exchange installation.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Exchange User Account Control   | A mask that is used to retrieve the user account control flags associated with this mailbox. This can be one of the following values:<br>AccountDisabled <br>CannotChangePassowrd <br>DoNotExpirePassword <br>DoNotRequirePreauthentication <br>EncryptedTextPasswordAllowed <br>HomeDirectoryRequired <br>InterDomainTrustAccount <br>Lockout <br>MnsLogonAccount <br>None <br>NormalAccount <br>NotDelegated <br>PasswordExpired <br>PasswordNotRequired <br>Script <br>ServerTrustAccount <br>SmartCardRequired <br>TemporaryDuplicateAccount <br>TrustedForDelegation <br>TrustedToAuthenticateForDelegation <br>UseDesKeyOnly <br>WorkstationTrustAccount   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Exchange Version   | Version of Microsoft Exchange that this object is associated with.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Extensions   | Extensions list.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| ExtensionCustomAttribute1- 5   | Extension custom attribute.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| External Directory Object ID   | External directory object ID.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| External OOF Options   | Options for sending Out of Office (OOF) messages to external senders. This can be one of the following values:<br>InternalOnly<br>External   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Forwarding Address   | Forwarding address for the mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Forwarding SMTP Address   | Forwarding SMTP address for the mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Grant Send On Behalf To   | List of users with "send on behalf" rights for this mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| GUID   | The globally unique identifier for this object.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Has Picture   | Indicates whether a picture has been associated with this mailbox.   | Equals<br>Does not equal   |
| Has Spoken Name   | Indicates whether a spoken name has been associated with this mailbox.   | Equals<br>Does not equal   |
| Hidden From Address Lists Enabled   | Indicates whether mailbox information is hidden from address book display.   | Equals<br>Does not equal   |
| Identity   | Mailbox identity.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Immutable ID   | Mailbox identifier that will never change.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Include In Garbage Collection   | Include In Garbage Collection.   | Equals<br>Does not equal   |
| Is Linked   | Indicates whether the mailbox is linked.   | Equals<br>Does not equal   |
| Is Machine To Person Text Messaging Enabled  | Indicates whether the server can send text messages to this user.   | Equals<br>Does not equal   |
| Is Mailbox Enabled   | Indicates whether the mailbox is enabled to process messages.   | Equals<br>Does not equal   |
| Is Person To Person Text Messaging Enabled   | Indicates whether another mailbox user can send a text message to the owner of this mailbox.   | Equals<br>Does not equal   |
| Is Resource   | Indicates whether this mailbox represents a resource, such as a conference room.   | Equals<br>Does not equal   |
| Is Shared   | Indicates whether this mailbox is shared by more than one user.   | Equals<br>Does not equal   |
| Is Soft Deleted By Disable   | Indicates whether the mailbox has been soft deleted as a result of a disable operation.   | Equals<br>Does not equal   |
| Is Soft Deleted By Remove   | Indicates whether the mailbox has been soft deleted as a result of a remove operation.   | Equals<br>Does not equal   |
| Issue Warning Quota   | Mailbox size at which a warning message is sent to the user.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| Is Valid   | Indicates whether the object is configured correctly.   | Equals<br>Does not equal   |
| Languages   | Preferred languages for this mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Last Exchange Changed Time   | Last Exchange changed time.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| Legacy Exchange DN   | Legacy Exchange DN.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Linked Master Account   | Master account for the linked mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Litigation Hold Date   | Date and time when litigation hold was enabled.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| Litigation Hold Enabled   | Indicates whether the mailbox is under a litigation hold.   | Equals<br>Does not equal   |
| Litigation Hold Owner   | User who enabled the litigation hold.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Mailbox Move Batch Name   | Name of the move batch that contains this mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Mailbox Move Flags   | Flags for a mailbox move. <br>This can be one of the following values: <br>CrossOrg<br>IntraOrg<br>MoveOnlyArchiveMailbox<br>MoveOnlyPrimaryMailbox<br>None<br>Offline<br>Protected<br>Pull<br>Push<br>RemoteLegacy<br>Suspend<br>SuspendWhenReadyToComplete<br>HighPriority   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Mailbox Move Remote Host Name   | Name of the remote host that is participating in the move.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Mailbox Move Source MDB   | Active Directory identifier of the source database.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Mailbox Move Status   | Indicates the status of a mailbox move. This can be one of the following values:<br>AutoSuspended <br>Completed <br>CompletedWithWarning <br>CompletionInProgress <br>Failed <br>InProgress <br>None <br>Queued <br>Suspended   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Mailbox Move Target MDB   | Active Directory identifier of the database that the mailbox is being copied to.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Mailbox Plan   | Mailbox plan for the mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Mailbox Release   | Mailbox release.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Mail Tip   | Mail tip.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Mail Tip Translations   | Mail tip translation list.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Managed Folder Mailbox Policy   | Messaging Records Management (MRM) policy for the mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Max Blocked Senders   | Maximum number of senders that can be included in a blocked senders list.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| Max Receive Size   | Received message size limit. <br>Can be either "unlimited" or a string with <br>format &lt;integer&gt; &lt;unit&gt; where unit can be KB, MB, GB, or TB. Defaults to Byte when unit is not specified.<br>Examples: 55 GB, unlimited, 77, 14 KB   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| Max Safe Senders   | Maximum number of senders that can be included in a safe senders list.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| Max Send Size   | Sent message size limit. <br>Can be either "unlimited" or a string with <br>format &lt;integer&gt; &lt;unit&gt; where unit can be KB, MB, GB, or TB. Defaults to Byte when unit is not specified.<br>Examples: 55 GB, unlimited, 77, 14 KB   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| Message Tracking Read Status Enabled   | Indicates whether detailed message tracking is enabled for the mailbox.   | Equals<br>Does not equal   |
| Microsoft Online Services ID   | Microsoft Online Services ID   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Moderated By   | List of users responsible for moderating this mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Moderation Enabled   | Indicates whether moderation is enabled or not for this mailbox.   | Equals<br>Does not equal   |
| Name   | Name associated with this object.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Object Category   | Active Directory object category for this mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Object Class   | List of Active Directory object classes that apply to this mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Office   | Microsoft Office attribute for the mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Offline Address Book   | Offline address book associated with the mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Organizational Unit   | Organizational unit for this mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Organization ID   | Organization for this mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Originating Server   | Originating server.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Partner Object ID   | GUID for partner object ID.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Persisted Capabilities   | Persisted capability list.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Policies Excluded   | List of policies that are excluded.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Policies Included   | List of policies that are included.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Primary SMTP Address   | Primary SMTP address for the mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Prohibit Send Quota   | Mailbox size at which the user is prohibited from sending email.<br>Can be either "unlimited" or a string with <br>format &lt;integer&gt; &lt;unit&gt; where unit can be KB, MB, GB, or TB. Defaults to Byte when unit is not specified.<br>Examples: 55 GB, unlimited, 77, 14 KB   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| Prohibit Send Receive Quota   | Mailbox size at which the user is prohibited from sending or receiving email.<br>Can be either "unlimited" or a string with <br>format &lt;integer&gt; &lt;unit&gt; where unit can be KB, MB, GB, or TB. Defaults to Byte when unit is not specified.<br>Examples: 55 GB, unlimited, 77, 14 KB   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| Protocol Settings   | Protocols used by the mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Query Base DN   | This property is used to control which address list a user has access to through Outlook Web App.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Query Base DN Restriction Enabled   | Indicates whether the user can search and view other mailboxes in their organization.   | Equals<br>Does not equal   |
| Recipient Limits   | Maximum number of recipients per message that this mailbox can send to.<br>Can be either "unlimited" or an integer.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| Recipient Type   | Recipient type. This can be one of the following values:<br>Computer <br>Contact <br>DynamicDistributionGroup <br>Group <br>Invalid <br>MailContact <br>MailNonUniversalGroup <br>MailUniversalDistributionGroup <br>MailUniversalSecurityGroup <br>MailUser <br>MicrosoftExchange <br>PublicDatabase <br>PublicFolder <br>SystemAttendantMailbox <br>SystemMailbox <br>User <br>UserMailbox   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Recipient Type Details   | Recipient type details. This can be one of the following values:<br>AllUniqueRecipientTypes <br>ArbitrationMailbox <br>Computer <br>Contact <br>DisabledUser <br>DiscoveryMailbox <br>DynamicDistributionGroup <br>EquipmentMailbox <br>LegacyMailbox <br>LinkedMailbox <br>LinkedUser <br>MailboxPlan <br>MailContact <br>MailForestContact <br>MailNonUniversalGroup <br>MailUniversalDistributionGroup <br>MailUniversalSecurityGroup <br>MailUser <br>MicrosoftExchange <br>None <br>NonUniversalGroup <br>PublicFolder <br>RemoteEquipmentMailbox <br>RemoteRoomMailbox <br>RemoteSharedMailbox <br>RemoteUserMailbox <br>RoleGroup <br>RoomList <br>RoomMailbox <br>SharedMailbox <br>SystemAttendantMailbox <br>SystemMailbox <br>UniversalDistributionGroup <br>UniversalSecurityGroup <br>User <br>UserMailbox | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Reconciliation Id   | Reconciliation ID.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Recoverable Items Quota   | Size limit for the Recovery Items folder.<br>Can be either "unlimited" or a string with <br>format &lt;integer&gt; &lt;unit&gt; where unit can be KB, MB, GB, or TB. Defaults to Byte when unit is not specified.<br>Examples: 55 GB, unlimited, 77, 14 KB   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| Recoverable Items Warning Quota   | Size at which a warning is sent that the Recovery Items folder is reaching its limit.<br>Can be either "unlimited" or a string with <br>format &lt;integer&gt; &lt;unit&gt; where unit can be KB, MB, GB, or TB. Defaults to Byte when unit is not specified.<br>Examples: 55 GB, unlimited, 77, 14 KB   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| Reject Messages From   | Rejected sender IDs list.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Reject Messages From DL Members   | Rejected sender IDs list.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Reject Messages From Senders Or Members   | Rejected sender IDs list.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Remote Account Policy   | Remote account policy ID.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Remote Recipient Type   | Remote recipient type. This can be one of the following values:<br>DeprovisionArchive <br>DeprovisionMailbox <br>EquipmentMailbox <br>Migrated <br>None <br>ProvisionArchive <br>ProvisionMailbox <br>RoomMailbox <br>SharedMailbox   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Require Sender Authentication Enabled   | Indicates whether sender authentication is required.   | Equals<br>Does not equal   |
| Resource Capacity   | Capacity of a resource mailbox.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| Resource Custom   | List containing additional information about a resource.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Resource Type   | Type of a resource.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Retain Deleted Items For   | Length of time to keep deleted items.<br>Format: d.hh:mm:ss where d = days, h = hours, m = minutes, and s = seconds.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| Retain Deleted Items Until Backup   | Indicates whether deleted items should be kept until the database is backed up.   | Equals<br>Does not equal   |
| Retention Comment   | The comment that is displayed regarding the user's retention hold status.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Retention Hold Enabled   | Indicates whether the contents of the mailbox are subject to retention.   | Equals<br>Does not equal   |
| Retention Policy   | Retention policy that is applied to the mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Retention URL   | URL for a webpage with details about the organization's message retention policies.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Role Assignment Policy   | Management role that was assigned to the mailbox when it was created or enabled.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Rules Quota   | Size limit for rules.<br>Can be either "unlimited" or a string with <br>format &lt;integer&gt; &lt;unit&gt; where unit can be KB, MB, GB, or TB. Defaults to Byte when unit is not specified.<br>Examples: 55 GB, unlimited, 77, 14 KB   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| Sam Account Name   | User name for use with earlier operating systems.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| SCL Delete Enabled   | Indicates whether messages that meet the spam confidence level (SCL) are deleted.   | Equals<br>Does not equal   |
| SCL Delete Threshold   | Spam confidence level (SCL) at which messages are considered spam and are to be deleted.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than   |
| SCL Junk Enabled   | Indicates whether messages that meet the spam confidence level (SCL) are moved to the Junk E-Mail folder.   | Equals<br>Does not equal   |
| SCL Junk Threshold   | Spam confidence level (SCL) at which messages are considered spam and are to be moved to the Junk E-Mail folder.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| SCL Quarantine Enabled   | Indicates whether messages that meet the spam confidence level (SCL) are quarantined.   | Equals<br>Does not equal   |
| SCL Quarantine Threshold   | Spam confidence level (SCL) at which messages are considered spam and are to be moved to the quarantine folder.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than   |
| SCL Reject Enabled   | Indicates whether messages that meet the spam confidence level (SCL) are rejected.   | Equals<br>Does not equal   |
| SCL Reject Threshold   | Spam confidence level (SCL) at which messages are considered spam and are to be rejected.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| Send Moderation Notifications   | Moderation notifications for this mailbox.<br>This can be one of the following values:<br>Always <br>Internal <br>Never   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Server Legacy DN   | Legacy domain name for the server.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Server Name   | Name of the server.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Sharing Policy   | Sharing policy associated with the mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Simple Display Name   | Simple display name.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Single Item Recovery Enabled   | Indicates whether the Recovery Items folder can be purged.   | Equals<br>Does not equal   |
| SKU Assigned   | SKU Assigned.   | Equals<br>Does not equal   |
| Start Date For Retention Hold   | Date and time that a retention hold on messages in this mailbox begins.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| Throttling Policy   | Identifier for the throttling policy applied to the mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| UM DTMF Map   | UM DTMF Map.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| UM Enabled   | Indicates whether Unified Messaging (UM) is enabled for this mailbox.   | Equals<br>Does not equal   |
| Usage Location   | Country name.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Use Database Quota Defaults   | Indicates whether this mailbox uses the database defaults for quota properties   | Equals<br>Does not equal   |
| Use Database Retention Defaults   | Indicates whether this mailbox uses the mailbox retention policy specified for the mailbox database that contains the mailbox.   | Equals<br>Does not equal   |
| User Principal Name   | Principal name for the mailbox user.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| When Changed   | Date and time when mailbox was changed.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| When Changed UTC   | UTC date and time when mailbox was changed.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| When Created   | Date and time when mailbox was created.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| When Created UTC   | UTC date and time when mailbox was created.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| When Mailbox Created   | Date and time when mailbox was created.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| When Soft Deleted   | Date and time when mailbox was soft deleted.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| Windows Email Address   | Email address.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Windows Live ID(Live@edu only)   | Windows Live ID associated with the mailbox. <br><br><strong>Note </strong><br> This property is available only in the Live@edu environment. <br><br>   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Needs To Suppress PII   | Needs to Suppress PII (Personally Identifiable Information).   | Equals<br>Does not equal   |

### Optional properties for the Get Mailbox activity

| Element   | Description   | Valid values |
|:---|:---|:---|
| Active Directory Password   | The password to use in order to access Active Directory.   | String   |
| Active Directory User Name  | Specifies the user name to use in order to access Active Directory.   | String   |
| ANR   | A string on which to perform an ambiguous name resolution (ANR) search. You can specify a partial string and search for objects with an attribute that matches that string. The default attributes searched are as follows: <br>CommonName (CN)<br>DisplayName<br>FirstName<br>LastName<br>Alias   | String   |
| Arbitration   | Indicates whether the mailbox for which the command is executed is an arbitration mailbox. Arbitration mailboxes are used for managing approval workflow. For example, an arbitration mailbox is used for handling moderated recipients and distribution group membership approval. Default is True, when selected.   | True, False  |
| Archive   | Indicates whether to return information about the recipient's archive mailbox. Default is True, when selected.   | True, False  |
| Database   | The database (GUID or database name) from which to get the mailbox. This property can't cannot be used in conjunction with activity filters.   | String   |
| Domain Controller   | The fully qualified domain name (FQDN) of the domain controller that retrieves data from Active Directory.   | String   |
| Identity   | Specifies the identity of the mailbox. This property can be one of the following value types:<br>GUID <br>Distinguished name (DN)<br>Display name<br>Domain\\Account <br>User principal name (UPN)<br>LegacyExchangeDN<br>SmtpAddress<br>Alias   | String   |
| Ignore Default Scope   | Indicates whether to ignore the default recipient scope setting for the Exchange Management Shell session and use the entire forest as the scope. This setting allows the command to access Active Directory objects that aren't currently in the default scope. Using the Ignore Default Scope property introduces the following restrictions:<br>Domain Controller property cannot be used. The command uses an appropriate global catalog server automatically.<br>The DN for the Identity property cannot be used. Other forms of identification, such as alias or GUID, aren't accepted.<br>The Organizational Unit and Identity properties cannot be used together.<br>The Active Directory Name and Password properties cannot be used.<br>Default is True, when selected.   | True, False  |
| Mailbox Plan   | Specifies the Get activity to return mailboxes associated with this mailbox plan. A mailbox plan specifies the permissions and features available to a mailbox user. The mailbox plan name you provide must be included in the service plan for the organization in which this mailbox belongs.<br>This property is available for multi-tenant deployments. This property applies to objects in the cloud-based service. It isn't available for on-premises deployments.   | String   |
| Organization   | Specifies the organization to retrieve mailboxes from.<br>This property is available for multi-tenant deployments. It isn't available for on-premises deployments. <br>This property does not accept wildcard characters. This property must be configured with the exact name of the organization.   | String   |
| Organizational Unit   | This property specifies an organizational unit (OU) to which the Get results will be limited. When this property is used, only mailboxes in the specified container will be returned. Specification can be either the OU or the domain name. If the OU is used, the canonical name of the OU must not be specified.   | String   |
| Read From Domain Controller | Specifies that the user information is read from a domain controller in the user's domain. When the recipient scope is set to include all recipients in the forest and this property is not configured, it is possible that the user information is read from a global catalog containing outdated information. If you use this property, multiple reads might be necessary to get the information. By default, the recipient scope is set to the domain that hosts your servers that run Exchange. <br>Default is True, when selected.   | True, False  |
| Recipient Type Details   | This property specifies the type of recipients returned by the Get activity. Recipient types are divided into recipient types and subtypes. <br>Each recipient type contains all common properties for all subtypes. For example, the type UserMailbox represents a user account in Active Directory that has an associated mailbox. Because there are several mailbox types, each mailbox type is identified by the RecipientTypeDetails property. For example, a conference room mailbox has RecipientTypeDetails set to RoomMailbox, whereas a user mailbox has RecipientTypeDetails set to UserMailbox.<br>This property accepts the following values:<br>RoomMailbox <br>EquipmentMailbox <br>LegacyMailbox <br>LinkedMailbox <br>UserMailbox <br>DiscoveryMailbox <br>SharedMailbox | String   |
| Remote Archive   | Specifies whether to disconnect the remote archive for this mailbox. A remote archive exists in a cloud-based service.<br>When you use this property, you cannot also use the Archive property. Default is True, when selected.   | True, False  |
| Result Size   | Specifies the maximum number of results to return. To return all mailboxes that match the query, use "unlimited" for the value of this property. The default value is "unlimited".   | String   |
| Server   | Specifies an individual server by which to limit the results. When you use this property, only mailboxes that reside on the specified server will be returned. Use the common name of the server that you want to specify.   | String   |
| Sort By   | Specifies the attribute by which to sort the results. Results can only be sorted by one attribute at a time. The results are sorted in ascending order. Results can be sorted by the following attributes: <br>Alias<br>Display name<br>Name<br>   | String   |

## Published data for the Get Mailbox activity

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Accept Messages Only From   | Mailbox users and mail-enabled contacts that can send email messages to this distribution group.   | String   |
| Accept Messages Only From DL Members   | Distribution lists that are allowed to send email messages to this mailbox.   | String   |
| Accept Messages Only From Senders Or Members | Senders or members that are allowed to send email messages to this distribution group.   | String   |
| Address Book Policy   | Address book policy for the mailbox.   | String   |
| Address List Membership   | Address list IDs.   | String   |
| Admin Display Version   | The version of the administrator's display.   | String   |
| Alias   | Mail nickname of the user.   | String   |
| Antispam Bypass Enabled   | Indicates whether anti-spam processing is used on the mailbox.   | String   |
| Arbitration Mailbox   | ID of the arbitration mailbox.   | String   |
| Archive Database   | ID of the archive database.   | String   |
| Archive Domain   | Archive domain name.   | String   |
| Archive GUID   | Unique archive identifier for the mailbox.   | String   |
| Archive Name   | Name of the archive mailbox.   | String   |
| Archive Quota   | Maximum size of the archive mailbox.   | String   |
| Archive Release   | Archive release.   | String   |
| Archive State   | Indicates the state of the mailbox archive. This can be one of the following values:<br>HostedPending <br>HostedProvisioned <br>Local <br>None <br>OnPremise   | String   |
| Archive Status   | The archive status (Active or None).   | String   |
| Archive Warning Quota   | Mailbox size at which a warning message is sent.   | String   |
| Audit Admin   | List of admin operations which are logged. This can be one of the following values: <br>Copy<br>Create<br>FolderBind<br>HardDelete<br>MessageBind<br>Move<br>MoveToDeletedItems<br>None<br>SendAs<br>SendOnBehalf<br>SoftDelete<br>Update   | String   |
| Audit Delegate   | List of delegate options which are logged. This can be one of the following values: <br>Copy<br>Create<br>FolderBind<br>HardDelete<br>MessageBind<br>Move<br>MoveToDeletedItems<br>None<br>SendAs<br>SendOnBehalf<br>SoftDelete<br>Update   | String   |
| Audit Enabled   | Indicates whether audit logging is enabled or disabled for the mailbox.   | String   |
| Audit Log Age Limit   | Amount of time that the audit log entries are retained in the mailbox.   | String   |
| Audit Owner   | List of owner operations that are logged. This can be one of the following values: <br>Copy<br>Create<br>FolderBind<br>HardDelete<br>MessageBind<br>Move<br>MoveToDeletedItems<br>None<br>SendAs<br>SendOnBehalf<br>SoftDelete<br>Update   | String   |
| Bypass Moderation From Senders Or Members   | List of senders for whom moderation is to be bypassed.   | String   |
| Calendar Repair Disabled   | Indicates whether calendar items in this mailbox are repaired by the Calendar Repair Assistant.   | String   |
| Calendar Version Store Disabled   | Indicates whether changes to calendar items are logged.   | String   |
| Custom Attribute 1   | Custom attribute value 1.   | String   |
| Custom Attribute 10   | Custom attribute value 10.   | String   |
| Custom Attribute 11   | Custom attribute value 11.   | String   |
| Custom Attribute 12   | Custom attribute value 12.   | String   |
| Custom Attribute 13   | Custom attribute value 13.   | String   |
| Custom Attribute 14   | Custom attribute value 14.   | String   |
| Custom Attribute 15   | Custom attribute value 15.   | String   |
| Custom Attribute 2   | Custom attribute value 2.   | String   |
| Custom Attribute 3   | Custom attribute value 3.   | String   |
| Custom Attribute 4   | Custom attribute value 4.   | String   |
| Custom Attribute 5   | Custom attribute value 5.   | String   |
| Custom Attribute 6   | Custom attribute value 6.   | String   |
| Custom Attribute 7   | Custom attribute value 7.   | String   |
| Custom Attribute 8   | Custom attribute value 8.   | String   |
| Custom Attribute 9   | Custom attribute value 9.   | String   |
| Database   | Active Directory ID of the database that contains this mailbox.   | String   |
| Default Public Folder Mailbox   | Default public folder mailbox.   | String   |
| Deliver To Mailbox And Forward   | Contains the forwarding address of the mailbox.   | String   |
| Disabled Archive Database   | Indicates whether the use of an Archive Database is disabled.   | String   |
| Disabled Archive GUID   | Indicates whether the use of Archive GUIDs is disabled.   | String   |
| Display Name   | The display name for the mailbox user.   | String   |
| Distinguished Name   | The distinguished name for the object.   | String   |
| Downgrade High Priority Messages Enabled   | Indicates whether high-priority messages sent to an X.400 mail system are changed to normal priority.   | String   |
| Email Address Policy Enabled   | Indicates whether Email Address Policy is enabled.   | String   |
| Email Addresses   | Collection of email addresses for the mailbox.   | String   |
| End Date For Retention Hold   | Date and time that retention hold on messages in this mailbox expires.   | DateTime   |
| Exchange Environment   | Indicates the type of Exchange environment where this activity will be executed.   | String   |
| Exchange GUID   | Unique identifier of the Microsoft Exchange installation.   | String   |
| Exchange PowerShell Application   | The application name segment of the connection URI.   | String   |
| Exchange Server Host   | The connected Exchange server host machine.   | String   |
| Exchange Server Port   | The connected Exchange server port.   | String   |
| Exchange User Account Control   | This is a mask that is used to retrieve the user account control flags associated with this mailbox. This can be one of the following values:<br>AccountDisabled <br>CannotChangePassword <br>DoNotExpirePassword <br>DoNotRequirePreauthentication <br>EncryptedTextPasswordAllowed <br>HomeDirectoryRequired <br>InterDomainTrustAccount <br>Lockout <br>MnsLogonAccount <br>None <br>NormalAccount <br>NotDelegated <br>PasswordExpired <br>PasswordNotRequired <br>Script <br>ServerTrustAccount <br>SmartCardRequired <br>TemporaryDuplicateAccount <br>TrustedForDelegation <br>TrustedToAuthenticateForDelegation <br>UseDesKeyOnly <br>WorkstationTrustAccount   | String   |
| Exchange User Name   | Username used to log on to Exchange server.   | String   |
| Exchange Version   | Version of Microsoft Exchange that this object is associated with.   | String   |
| ExtensionCustomAttribute1   | Extension custom attribute 1.   | String   |
| ExtensionCustomAttribute2   | Extension custom attribute 2.   | String   |
| ExtensionCustomAttribute3   | Extension custom attribute 3.   | String   |
| ExtensionCustomAttribute4   | Extension custom attribute 4.   | String   |
| ExtensionCustomAttribute5   | Extension custom attribute 5.   | String   |
| Extensions   | List of extensions.   | String   |
| External Directory Object Id   | External directory object ID.   | String   |
| External OOF Options   | Options for sending Out of Office (OOF) messages to external senders. This property can be one of the following values:<br>InternalOnly<br>External   | String   |
| Forwarding Address   | Forwarding address for this mailbox.   | String   |
| Forwarding SMTP Address   | Forwarding SMTP address for this mailbox.   | String   |
| Grant Send On Behalf To   | List of users with "send on behalf" rights for this mailbox.   | String   |
| GUID   | Globally unique identifier for this object.   | String   |
| Has Picture   | Indicates whether a picture has been associated with this mailbox.   | String   |
| Has Spoken Name   | Indicates whether a spoken name has been associated with this mailbox.   | String   |
| Hidden From Address Lists Enabled   | Indicates whether mailbox information is hidden from address book display.   | String   |
| Identity   | Mailbox identity.   | String   |
| Immutable Id   | Mailbox identifier that will never change.   | String   |
| Include In Garbage Collection   | Include In Garbage Collection.   | String   |
| Is Linked   | Indicates whether a mailbox is linked.   | String   |
| Is Machine To Person Text Messaging Enabled  | Indicates whether the server can send text messages to a user.   | String   |
| Is Mailbox Enabled   | Indicates whether the mailbox is enabled to process messages.   | String   |
| Is Person To Person Text Messaging Enabled   | Indicates whether another mailbox user can send a text message to the owner of this mailbox.   | String   |
| Is Resource   | Indicates whether this mailbox represents a resource, such as a conference room.   | String   |
| Is Shared   | Indicates whether this mailbox is shared by more than one user.   | String   |
| Is Soft Deleted By Disable   | Indicates whether the mailbox is soft deleted as a result of a disable operation.   | String   |
| Is Soft Deleted By Remove   | Indicates whether the mailbox is soft deleted as a result of a remove operation.   | String   |
| Issue Warning Quota   | Mailbox size at which a warning message is sent to the user.   | String   |
| Is Valid   | Indicates whether the object is configured correctly.   | String   |
| Languages   | Preferred languages for this mailbox.   | String   |
| Last Exchange Changed Time   | Last exchange changed time.   | DateTime   |
| Legacy Exchange DN   | Legacy exchange DN.   | String   |
| Linked Master Account   | Master account for the linked mailbox.   | String   |
| Litigation Hold Date   | Date and time when litigation hold was enabled.   | DateTime   |
| Litigation Hold Enabled   | Indicates whether the mailbox is under a litigation hold.   | String   |
| Litigation Hold Owner   | User who enabled the litigation hold.   | String   |
| Mail Tip   | Mail tip.   | String   |
| Mail Tip Translations   | Mail tip translation list.   | String   |
| Mailbox Count   | Number of mailboxes returned by the Get Mailbox activity.   | Number   |
| Mailbox Move Batch Name   | Name of the move batch that contains this mailbox.   | String   |
| Mailbox Move Flags   | Flags for a mailbox move. <br>This can be any of the following values: <br>CrossOrg<br>IntraOrg<br>MoveOnlyArchiveMailbox<br>MoveOnlyPrimaryMailbox<br>None<br>Offline<br>Protected<br>Pull<br>Push<br>RemoteLegacy<br>Suspend<br>SuspendWhenReadyToComplete   | String   |
| Mailbox Move Remote Host Name   | Name of the remote host that is participating in the move.   | String   |
| Mailbox Move Source MDB   | Active Directory identifier of the source database.   | String   |
| Mailbox Move Status   | Indicates the status of a mailbox move. This can be one of the following values:<br>AutoSuspended <br>Completed <br>CompletedWithWarning <br>CompletionInProgress <br>Failed <br>InProgress <br>None <br>Queued <br>Suspended   | String   |
| Mailbox Move Target MDB   | Active Directory identifier of the database that the mailbox is being copied to.   | String   |
| Mailbox Plan   | Mailbox plan for a mailbox.   | String   |
| Mailbox Release   | Mailbox release.   | String   |
| Managed Folder Mailbox Policy   | Messaging Records Management (MRM) policy for the mailbox.   | String   |
| Max Blocked Senders   | Maximum number of senders that can be included in a blocked senders list.   | Number   |
| Max Receive Size   | Received message size limit.   | String   |
| Max Safe Senders   | Maximum number of senders that can be included in a safe senders list.   | Integer   |
| Max Send Size   | Sent message size limit.   | String   |
| Message Tracking Read Status Enabled   | Indicates whether detailed message tracking is enabled for the mailbox.   | String   |
| Microsoft Online Services ID   | ID allowing access to Microsoft Online Services.   | String   |
| Moderated By   | List of users responsible for moderating this mailbox.   | String   |
| Moderation Enabled   | Indicates whether moderation is enabled for this mailbox.   | String   |
| Name   | Name associated with this object.   | String   |
| Needs To Suppress PII   | Needs to Suppress PII (Personally Identifiable Information).   | String   |
| Object Category   | Active Directory object category for this mailbox.   | String   |
| Object Class   | List of Active Directory object classes that apply to this mailbox.   | String   |
| Office   | Microsoft Office attribute for the mailbox.   | String   |
| Offline Address Book   | Offline address book associated with the mailbox.   | String   |
| Organization ID   | Organization for this mailbox.   | String   |
| Organizational Unit   | Organizational unit for this mailbox.   | String   |
| Originating Server   | Originating server.   | String   |
| Partner Object ID   | GUID for partner object ID.   | String   |
| Persisted Capabilities   | Persisted capability list.   | String   |
| Policies Excluded   | List of policies that are excluded.   | String   |
| Policies Included   | List of policies that are included.   | String   |
| Primary SMTP Address   | Primary SMTP address for the mailbox.   | String   |
| Prohibit Send Quota   | Mailbox size at which the user is prohibited from sending email.   | String   |
| Prohibit Send Receive Quota   | Mailbox size at which the user is prohibited from sending or receiving email.   | String   |
| Protocol Settings   | Protocols used by the mailbox.   | String   |
| Query Base DN   | This property is used to control which address list a user can access through Outlook Web App.   | String   |
| Query Base DN Restriction Enabled   | Indicates whether the user can search and view other mailboxes in their organization.   | String   |
| Recipient Limits   | Maximum number of recipients per message that this mailbox can send to.   | String   |
| Recipient Type   | Recipient type. This can be one of the following values:<br>Computer <br>Contact <br>DynamicDistributionGroup<br>Group <br>Invalid <br>MailContact <br>MailNonUniversalGroup <br>MailUniversalDistributionGroup <br>MailUniversalSecurityGroup <br>MailUser <br>MicrosoftExchange <br>PublicDatabase <br>PublicFolder <br>SystemAttendantMailbox <br>SystemMailbox <br>User <br>UserMailbox   | String   |
| Recipient Type Details   | Recipient type details. This can be one of the following values:<br>AllUniqueRecipientTypes <br>ArbitrationMailbox <br>Computer <br>Contact <br>DisabledUser <br>DiscoveryMailbox <br>DynamicDistributionGroup <br>EquipmentMailbox <br>LegacyMailbox <br>LinkedMailbox <br>LinkedUser <br>MailboxPlan <br>MailContact <br>MailForestContact <br>MailNonUniversalGroup <br>MailUniversalDistributionGroup <br>MailUniversalSecurityGroup <br>MailUser <br>MicrosoftExchange <br>None <br>NonUniversalGroup <br>PublicFolder <br>RemoteEquipmentMailbox <br>RemoteRoomMailbox <br>RemoteSharedMailbox <br>RemoteUserMailbox <br>RoleGroup <br>RoomList <br>RoomMailbox <br>SharedMailbox <br>SystemAttendantMailbox <br>SystemMailbox <br>UniversalDistributionGroup <br>UniversalSecurityGroup <br>User <br>UserMailbox | String   |
| Reconciliation Id   | Reconciliation ID.   | String   |
| Recoverable Items Quota   | Size limit for the Recovery Items folder.   | String   |
| Recoverable Items Warning Quota   | Size at which a warning is sent stating that the Recovery Items folder is reaching its limit.   | String   |
| Reject Messages From   | Rejected sender IDs list.   | String   |
| Reject Messages From DL Members   | Rejected sender IDs list.   | String   |
| Reject Messages From Senders Or Members   | Rejected sender IDs list.   | String   |
| Remote Account Policy   | Remote account policy ID.   | String   |
| Remote Recipient Type   | Remote recipient type. This can be one of the following values:<br>DeprovisionArchive <br>DeprovisionMailbox <br>EquipmentMailbox <br>Migrated <br>None <br>ProvisionArchive <br>ProvisionMailbox <br>RoomMailbox <br>SharedMailbox   | String   |
| Require Sender Authentication Enabled   | Indicates whether sender authentication is required.   | String   |
| Resource Capacity   | Capacity of a resource mailbox.   | Number   |
| Resource Custom   | List containing additional information about a resource.   | String   |
| Resource Type   | Type of a resource.   | String   |
| Retain Deleted Items For   | Length of time to keep deleted items.   | String   |
| Retain Deleted Items Until Backup   | Indicates whether deleted items should be kept until the database is backed up.   | String   |
| Retention Comment   | Comment displayed regarding the user's retention hold status.   | String   |
| Retention Hold Enabled   | Indicates whether the contents of the mailbox are subject to retention.   | String   |
| Retention Policy   | Retention policy that is applied to the mailbox.   | String   |
| Retention URL   | URL for a webpage with details about the organization's message retention policies.   | String   |
| Role Assignment Policy   | Management role that was assigned to the mailbox when it was created or enabled.   | String   |
| Rules Quota   | Size limit for rules.   | String   |
| Sam Account Name   | User name for use with earlier operating systems.   | String   |
| SCL Delete Enabled   | Indicates whether messages that meet the spam confidence level (SCL) are deleted.   | String   |
| SCL Delete Threshold   | Spam confidence level (SCL) at which messages are considered spam and are to be deleted.   | Number   |
| SCL Junk Enabled   | Indicates whether messages that meet the spam confidence level (SCL) are moved to the Junk E-Mail folder.   | String   |
| SCL Junk Threshold   | Spam confidence level (SCL) at which messages are considered spam and are to be moved to the Junk E-Mail folder.   | Number   |
| SCL Quarantine Enabled   | Indicates whether messages that meet the spam confidence level (SCL) are quarantined.   | String   |
| SCL Quarantine Threshold   | Spam confidence level (SCL) at which messages are considered spam and are to be moved to the quarantine folder.   | Number   |
| SCL Reject Enabled   | Indicates whether messages that meet the spam confidence level (SCL) are rejected.   | String   |
| SCL Reject Threshold   | Spam confidence level (SCL) at which messages are considered spam and are to be rejected.   | Number   |
| SKU Assigned   | This parameter is reserved for internal Microsoft use.   | String   |
| Send Moderation Notifications   | Moderation notifications for this mailbox.<br>This can be one of the following values:<br>Always <br>Internal <br>Never   | String   |
| Server Legacy DN   | Legacy domain name for the server.   | String   |
| Server Name   | Name of the server.   | String   |
| Sharing Policy   | Sharing policy applied to the mailbox.   | String   |
| Simple Display Name   | Simple display name.   | String   |
| Single Item Recovery Enabled   | Indicates whether the Recovery Items folder can be purged.   | Boolean   |
| Skip CA Check   | Indicates whether the client skips validation that the server certificate is signed by a trusted certification authority (CA) when connecting over Hypertext Transfer Protocol (HTTP) over Secure Sockets Layer (SSL).   | String   |
| Skip CN Check   | Indicates whether the client skips validation that the certificate common name (CN) of the server matches the hostname of the server.   | String   |
| Skip Revocation Check   | Indicates whether the connection skips validation of the revocation status of the server certificate.   | String   |
| Start Date For Retention Hold   | Date and time that a retention hold on messages in this mailbox begins.   | DateTime   |
| Throttling Policy   | Identifier for the throttling policy applied to the mailbox.   | String   |
| UM DTMF Map   | UM DTMF Map.   | String   |
| UM Enabled   | Indicates whether Unified Messaging (UM) is enabled for this mailbox.   | String   |
| Usage Location   | Country name.   | String   |
| Use Database Quota Defaults   | Indicates whether this mailbox uses the database defaults for quota properties.   | String   |
| Use Database Retention Defaults   | Indicates whether this mailbox uses the mailbox retention policy specified for the mailbox database that contains the mailbox.   | String   |
| Use SSL   | Indicates whether SSL encryption is used.   | String   |
| User Principal Name   | Principal name for the mailbox user.   | String   |
| When Changed   | Date and time when mailbox was changed.   | DateTime   |
| When Changed UTC   | UTC date and time when mailbox was changed.   | DateTime   |
| When Created   | Date and time when mailbox was created.   | DateTime   |
| When Created UTC   | UTC date and time when mailbox was created.   | DateTime   |
| When Mailbox Created   | Date and time when mailbox was created.   | DateTime   |
| When Soft Deleted   | Date and time when mailbox was soft deleted.   | DateTime   |
| Windows Email Address   | Email address.   | String   |
| Windows Live ID(Live@edu only)   | Windows Live ID associated with the mailbox. <br><br><strong>Note </strong><br> This property is available only in the Live@edu environment. <br><br>   | String   |



