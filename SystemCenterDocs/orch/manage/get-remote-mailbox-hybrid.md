---
title: Get Remote Mailbox (Hybrid)
description: You can use the Get Remote Mailbox (Hybrid) activity to retrieve the mail-related attributes of one or more users in on-premises Active Directory that are associated with mailboxes in the cloud-based service (hybrid environment).
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8172f3a7-8890-4ef1-9c0f-ff6d81ec9f33
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
Get Remote Mailbox (Hybrid)
===========================

Applies To: System Center 2016 - Orchestrator

You can use the Get Remote Mailbox (Hybrid) activity to retrieve the mail-related attributes of one or more users in on-premises Active Directory that are associated with mailboxes in the cloud-based service (hybrid environment).

The following tables list the required properties, optional properties, filters, and published data for this activity.

Required properties for Get Remote Mailbox (Hybrid)
---------------------------------------------------

This activity has no required properties.

Optional properties for Get Remote Mailbox (Hybrid)
---------------------------------------------------

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Active Directory Password   | Specifies the user password that you will use to access the on-premises Active Directory.   | String   |
| Active Directory User Name   | Specifies the user name that you will use to access the on-premises Active Directory.   | String   |
| ANR   | Specifies a string on which to perform an ambiguous name resolution (ANR) search. You can specify a partial string and search for objects with an attribute that matches that string. The default searched attributes are the following: <br>CommonName (CN)<br>DisplayName<br>FirstName<br>LastName<br>Alias   | String   |
| Archive   | Specifies whether to return information about the recipient's archive mailbox.   | True, False   |
| Domain Controller   | Specifies the fully qualified domain name (FQDN) of the domain controller that retrieves data from Active Directory.   | String   |
| Identity   | Identifies the remote mailbox. The remote mailbox identity can be one the following value types:<br>GUID <br>Distinguished name (DN)<br>Domain\\Account <br>User principal name (UPN)<br>LegacyExchangeDN<br>SmtpAddress<br>Alias   | String   |
| Ignore Default Scope   | Instructs the command to ignore the default recipient scope setting for the Exchange Management Shell session and to use the entire forest as the scope. This allows the command to access the Active Directory objects that are not currently in the default scope. Using this property introduces the following restrictions:<br>You cannot use the Domain Controller property. The command uses an appropriate global catalog server automatically.<br>You can only use the DN for the Identity property. Other forms of identification, such as alias, are not accepted.<br>You cannot use the On Premises Organizational Unit and Identity properties together.<br>You cannot use the User Name and Password properties. | True, False   |
| On-Premises Organizational Unit | Specifies a container in the on-premises organization in which to limit the results. You can specify either an organizational unit (OU) or a domain. The canonical name should be specified, such as,<br>OU: westcoast.contoso.com/users <br>Domain: westcoast.contoso.com   | String   |
| Read From Domain Controller   | Specifies that the user information is read from a domain controller in the user's domain. If you set the recipient scope to include all recipients in the forest and do not use this property, it is possible that the user information is read from a global catalog with outdated information. If you use this property, multiple reads might be necessary in order to get the information.<br>By default, the recipient scope is set to the domain that hosts your servers that run Exchange.   | True, False   |
| Result Size   | Specifies the maximum number of results to return. If you want to return all mailboxes that match the query, use **unlimited** for the value of this property. The default value is **unlimited**.   | String   |
| Sort By   | Specifies the attribute by which to sort the results. You can sort by only one attribute at a time. You can sort by the following attributes: <br>Alias<br>Display name<br>Name<br> **Note** The results are sorted in ascending order.   | String   |

Filters for Get Remote Mailbox (Hybrid)
---------------------------------------

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Accept Messages Only From   | Specifies the mailbox users and mail-enabled contacts that can send email messages to this mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Accept Messages Only From DL Members   | Specifies the distribution list of mail users that are allowed to send email messages to this mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Accept Messages Only From Senders Or Members | Specifies the senders or members that are allowed to send email messages to this distribution group.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Address List Membership   | Specifies the address list IDs.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Alias   | Specifies the mail nickname of the user.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Arbitration Mailbox   | Specifies the ID of the arbitration mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Archive Database   | Specifies the ID of the archive database.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Archive GUID   | Specifies the unique archive identifier for the mailbox archive.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Archive Name   | Specifies the name of the archive mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Archive Quota   | Specifies the maximum size of the archive mailbox.<br>It be either "unlimited" or a string with <br>format &lt;integer&gt; &lt;unit&gt;, where unit can be one of the following: KB, MB, GB, TB. The default value is Byte, when the unit is not specified.<br>For example, 55 GB, unlimited, 77, 14 KB.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| Archive Status   | Indicates the archive status (Active or None).   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Archive Warning Quota   | Specifies the mailbox size at which a warning message is sent, when this size is exceeded<br>The size can be either "unlimited" or a string with <br>format &lt;integer&gt; &lt;unit&gt;, where the unit can be one of the following: KB, MB, GB, TB. The default unit is Byte, when unit is not specified.<br>For example, 55 GB, unlimited, 77, 14 KB.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| Bypass Moderation From Senders Or Members   | Specifies the list of senders for whom moderation is to be bypassed.   | Equals<br>Does not equal   |
| Calendar Version Store Disabled   | Indicates whether calendar items in this mailbox will be repaired by the Calendar Repair Assistant.   | Equals<br>Does not equal   |
| Custom Attribute 1 - 15   | Custom attribute value.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Deliver To Mailbox And Forward   | Indicates whether messages that are sent to this mailbox are forwarded to another mailbox.   | Equals<br>Does not equal   |
| Disabled Archive Database   | Indicates the ID of the disabled archive database.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Disabled Archive GUID   | Indicates the GUID of the disabled archive.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Display Name   | Specifies the display name for the mailbox user.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Distinguished Name   | Specifies the distinguished name for the object.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Email Addresses   | Specifies the collection of email addresses for the mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Email Address Policy Enabled   | Indicates whether the Email Address policy is enabled.   | Equals<br>Does not equal   |
| End Date For Retention Hold   | Specifies the date and time that a retention hold on messages in this mailbox expires.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| Exchange GUID   | Specifies the unique identifier of the Microsoft Exchange installation.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Exchange User Account Control   | Specifies a mask that is used to retrieve the user account control flags that are associated with this mailbox. Can be one of the following:<br>AccountDisabled <br>CannotChangePassowrd <br>DoNotExpirePassword <br>DoNotRequirePreauthentication <br>EncryptedTextPasswordAllowed <br>HomeDirectoryRequired <br>InterDomainTrustAccount <br>Lockout <br>MnsLogonAccount <br>None <br>NormalAccount <br>NotDelegated <br>PasswordExpired <br>PasswordNotRequired <br>Script <br>ServerTrustAccount <br>SmartCardRequired <br>TemporaryDuplicateAccount <br>TrustedForDelegation <br>TrustedToAuthenticateForDelegation <br>UseDesKeyOnly <br>WorkstationTrustAccount   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Exchange Version   | Specifies the version of Microsoft Exchange that this object is associated with.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Extension Custom Attribute 1 - 5   | Extension custom attribute.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Extensions   | Extensions list.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| External Directory Object Id   | External directory object ID.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Forwarding Address   | Specifies the forwarding address for a mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Grant Send On Behalf To   | Specifies the list of users with "send on behalf" rights for this mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| GUID   | Unique identifier for this object.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Has Picture   | Indicates whether a picture has been associated with this mailbox.   | Equals<br>Does not equal   |
| Has Spoken Name   | Indicates whether a spoken name has been associated with this mailbox.   | Equals<br>Does not equal   |
| Hidden From Address Lists Enabled   | Indicates whether the mailbox information is hidden from the address book.   | Equals<br>Does not equal   |
| Identity   | Mailbox identity.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Immutable ID   | Specifies the identifier for the mailbox that will never change.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Is Valid   | Indicates whether the object is configured correctly.   | Equals<br>Does not equal   |
| Last Exchange Changed Time   | Indicates the last exchange changed time.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| Legacy Exchange DN   | Legacy exchange DN.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Litigation Hold Date   | Specifies the date and time when the litigation hold was enabled.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| Litigation Hold Enabled   | Indicates whether the mailbox is under a litigation hold.   | Equals<br>Does not equal   |
| Litigation Hold Owner   | Specifies the user who enabled the litigation hold.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Mailbox Move Batch Name   | Specifies the name of the move batch that contains this mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Mailbox Move Flags   | Specifies the flags for a mailbox move. <br>It can be one of the following: <br>CrossOrg<br>IntraOrg<br>MoveOnlyArchiveMailbox<br>MoveOnlyPrimaryMailbox<br>None<br>Offline<br>Protected<br>Pull<br>Push<br>RemoteLegacy<br>Suspend<br>SuspendWhenReadyToComplete   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Mailbox Move Remote Host Name   | Specifies the name of the remote host that is participating in the move.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Mailbox Move Source MDB   | Active Directory identifier of the source database.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Mailbox Move Status   | Indicates the status of a mailbox move. It can be one of the following:<br>AutoSuspended <br>Completed <br>CompletedWithWarning <br>CompletionInProgress <br>Failed <br>InProgress <br>None <br>Queued <br>Suspended   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Mailbox Move Target MDB   | Specifies the Active Directory identifier of the database that the mailbox is being copied to.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Mail Tip   | Mail tip.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Mail Tip Translations   | Mail tip translation list.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Max Receive Size   | Specifies the size limit of the received messages.<br>The size can be either "unlimited" or a string with <br>format &lt;integer&gt; &lt;unit&gt;, where unit can be one of the following: KB, MB, GB, TB. The default unit it Byte when the unit is not specified.<br>For example, 55 GB, unlimited, 77, 14 KB.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| Max Send Size   | Specifies the size limit for received messages. <br>The size can be either "unlimited" or a string with <br>format &lt;integer&gt; &lt;unit&gt;, where unit can be one of the following: KB, MB, GB, TB. The default unit it Byte, when unit is not specified.<br>For example, 55 GB, unlimited, 77, 14 KB.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| Moderated By   | Specifies the list of users that are responsible for moderating this mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Moderation Enabled   | Indicates whether moderation is enabled for this mailbox.   | Equals<br>Does not equal   |
| Name   | Specifies the name associated with this object.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Object Category   | Specifies the Active Directory object category for this mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Object Class   | Specifies the list of Active Directory object classes that apply to this mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| On-Premises Organizational Unit   | Indicates the organizational unit for this mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Organization ID   | Specifies the organization for this mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Originating Server   | Originating server.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern Starts with<br>Ends with   |
| Partner Object ID   | Specifies the GUID for partner object ID.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Persisted Capabilities   | Specifies the list of persisted capabilities.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Policies Excluded   | Specifies the list of policies that are excluded.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Policies Included   | Specifies the list of policies that are included.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Primary SMTP Address   | Specifies the primary SMTP address for the mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Protocol Settings   | Specifies the protocols used by the mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Recipient Limits   | Specifies the maximum number of recipients per message that this mailbox can send to. The value number can be 'unlimited' or an integer.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| Recipient Type   | Specifies the recipient type. It can be one of the following:<br>Computer <br>Contact <br>DynamicDistributionGroup <br>Group <br>Invalid <br>MailContact <br>MailNonUniversalGroup <br>MailUniversalDistributionGroup <br>MailUniversalSecurityGroup <br>MailUser <br>MicrosoftExchange <br>PublicDatabase <br>PublicFolder <br>SystemAttendantMailbox <br>SystemMailbox <br>User <br>UserMailbox   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Recipient Type Details   | Specifies the recipient type details. The type details can be one of:<br>AllUniqueRecipientTypes <br>ArbitrationMailbox <br>Computer <br>Contact <br>DisabledUser <br>DiscoveryMailbox <br>DynamicDistributionGroup <br>EquipmentMailbox <br>LegacyMailbox <br>LinkedMailbox <br>LinkedUser <br>MailboxPlan <br>MailContact <br>MailForestContact <br>MailNonUniversalGroup <br>MailUniversalDistributionGroup <br>MailUniversalSecurityGroup <br>MailUser <br>MicrosoftExchange <br>None <br>NonUniversalGroup <br>PublicFolder <br>RemoteEquipmentMailbox <br>RemoteRoomMailbox <br>RemoteSharedMailbox <br>RemoteUserMailbox <br>RoleGroup <br>RoomList <br>RoomMailbox <br>SharedMailbox <br>SystemAttendantMailbox <br>SystemMailbox <br>UniversalDistributionGroup <br>UniversalSecurityGroup <br>User <br>UserMailbox | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Reject Messages From   | Specifies the list of the rejected sender IDs.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Reject Messages From DL Members   | Rejected sender IDs list   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Reject Messages From Senders Or Members   | Rejected sender IDs list.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Remote Recipient Type   | Specifies the remote recipient type. It can be one of:<br>DeprovisionArchive <br>DeprovisionMailbox <br>EquipmentMailbox <br>Migrated <br>None <br>ProvisionArchive <br>ProvisionMailbox <br>RoomMailbox <br>SharedMailbox   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Remote Routing Address   | Specifies the remote routing address for the remote mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Require Sender Authentication Enabled   | Indicates whether the sender authentication is required.   | Equals<br>Does not equal   |
| Retain Deleted Items For   | Specifies the length of time to keep the deleted items.<br>You can set the time length in the following format: d.hh:mm:ss where d = days, h = hours, m = minutes, and s = seconds.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| Retention Comment   | Shows the comment that is displayed regarding the user's retention hold status.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Retention Hold Enabled   | Indicates whether the contents of the mailbox are subject to retention.   | Equals<br>Does not equal   |
| Retention URL   | Indicates the URL for a webpage with details about the organization's message retention policies.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| SAM Account Name   | Specifies the user name for earlier operating systems.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Send Moderation Notifications   | Specifies the moderation notifications for this mailbox.<br>Can be one of the following:<br>Always <br>Internal <br>Never   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Simple Display Name   | Simple display name.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| Single Item Recovery Enabled   | Indicates whether the Recovery Items folder can be purged.   | Equals<br>Does not equal   |
| Start Date For Retention Hold   | Specifies the date and time that a retention hold on messages in this mailbox begins.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| UM DTMF Map   | UM DTMF Map.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| User Principal Name   | Specifies the principal name for the mail box user.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |
| When Changed   | Specifies the date and time when the mailbox was changed.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| When Changed UTC   | Specifies the UTC date and time when the mailbox was changed.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| When Created   | Specifies the date and time when the mailbox was created.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| When Created UTC   | Specifies the UTC date and time when the mailbox was created.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| When Mailbox Created   | Specifies the Date and time when the mailbox was created.   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| Windows Email Address   | Specifies the Windows email address.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with |

Published data for Get Remote Mailbox (Hybrid)
----------------------------------------------

| Element   | Description   | Valid values |
|:---|:---|:---|
| Accept Messages Only From   | Specifies the mailbox users and mail-enabled contacts that can send email messages to this distribution group.   | String   |
| Accept Messages Only From DL Members   | Specifies the distribution lists that are allowed to send email messages to this mailbox.   | String   |
| Accept Messages Only From Senders Or Members | Specifies the senders or members that are allowed to send email messages to this distribution group.   | String   |
| Address List Membership   | Contains address lists that the mailbox is part of.   | String   |
| Alias   | Indicates the mail nickname of the user.   | String   |
| Arbitration Mailbox   | Specifies the mailbox that is used to manage the moderation process.   | String   |
| Archive Database   | Specifies the archive mailbox database.   |   |
| Archive GUID   | Specifies the archive mailbox identifier.   | String   |
| Archive Name   | Specifies the archive mailbox name.   | String   |
| Archive Quota   | Specifies the Quota parameter for the archive mailbox.   | String   |
| Archive Status   | Indicates the archive status (Active or None).   | String   |
| Archive Warning Quota   | Specifies the mailbox size at which a warning message is sent.   | String   |
| Bypass Moderation From Senders Or Members   | Specifies the list of Senders or Members of a list who's messages are not subject to approval.   | String   |
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
| Deliver to Mailbox And Forward   | Contains the forwarding address of the mailbox.   | String   |
| Disabled Archive Database   | Specifies the ID of the disabled archive database.   | String   |
| Disabled Archive GUID   | Indicates the GUID of the disabled archive.   | String   |
| Display Name   | Specifies the content of the Simple Display Name field.   | String   |
| Distinguished Name   | Specifies the distinguished name Exchange legacy.   | String   |
| Email Address Policy Enabled   | Indicated whether the use of Address Policies is enabled.   | String   |
| Email Addresses   | Specifies the collection of email addresses for the mailbox.   | String   |
| End Date For Retention Hold   | Specifies the end date of the Retention Hold period.   | String   |
| Exchange Environment   | Indicates the type of Exchange environment where this activity will be executed. Default is On-Premise.   | String   |
| Exchange GUID   | Specifies the unique identifier of the Microsoft Exchange installation.   | String   |
| Exchange PowerShell Application   | Specifies the application name segment of the connection URI.   | String   |
| Exchange Server Host   | Specifies the connected Exchange Server.   | String   |
| Exchange Server Port   | Specifies the connected Exchange Server port.   | String   |
| Exchange User Account Control   | Retrieves the user account control flags that are associated with this mailbox. Can be one of the following:<br>AccountDisabled <br>CannotChangePassowrd <br>DoNotExpirePassword <br>DoNotRequirePreauthentication <br>EncryptedTextPasswordAllowed <br>HomeDirectoryRequired <br>InterDomainTrustAccount <br>Lockout <br>MnsLogonAccount <br>None <br>NormalAccount <br>NotDelegated <br>PasswordExpired <br>PasswordNotRequired <br>Script <br>ServerTrustAccount <br>SmartCardRequired <br>TemporaryDuplicateAccount <br>TrustedForDelegation <br>TrustedToAuthenticateForDelegation <br>UseDesKeyOnly <br>WorkstationTrustAccount | String   |
| Exchange User Name   | Specifies the username used to connect to Exchange Server.   | String   |
| Exchange Version   | Specifies the version of the Exchange Server.   | String   |
| Extension Custom Attribute 1   | Extension Custom Attribute 1.   | String   |
| Extension Custom Attribute 2   | Extension Custom Attribute 2.   | String   |
| Extension Custom Attribute 3   | Extension Custom Attribute 3.   | String   |
| Extension Custom Attribute 4   | Extension Custom Attribute 4.   | String   |
| Extension Custom Attribute 5   | Extension Custom Attribute 5.   | String   |
| Extensions   | Extension List.   | String   |
| External Directory Object Id   | Specifies the ID of the mailbox in the external directory.   | String   |
| Forwarding Address   | Indicates the forwarding Address that is defined for the mailbox.   | String   |
| GUID   | Specifies the mailbox GUID.   | String   |
| Grant Send On Behalf To   | Lists users who are allowed to send messages on the owner's behalf.   | String   |
| Has Picture   | Indicates whether a picture is associated with the mailbox.   | String   |
| Has Spoken Name   | Indicates whether a spoken name is associated with the mailbox.   | String   |
| Hidden from Address Lists Enabled   | Indicates whether mailbox information is hidden from address book.   | String   |
| Identity   | Specifies the mailbox identity.   | String   |
| Immutable ID   | Specifies the identifier for the mailbox that will never change.   | String   |
| Is Valid   | Indicates whether the object is configured correctly.   | String   |
| Last Exchange Changed Time   | Last exchange changed time.   | String   |
| Legacy Exchange DN   | Legacy exchange DN.   | String   |
| Litigation Hold Date   | Specifies the date and time when the litigation hold was enabled.   | String   |
| Litigation Hold Enabled   | Indicates whether the mailbox is under a litigation hold.   | String   |
| Litigation Hold Owner   | Specifies the user who enabled the litigation hold.   | String   |
| Mail Tip   | Mail tip.   | String   |
| Mail Tip Translations   | Mail tip translation list.   | String   |
| Mailbox Count   | Specifies the number of mailboxes returned by the activity.   | Number   |
| Mailbox Move Batch Name   | Specifies the name of the move batch that contains this mailbox.   | String   |
| Mailbox Move Flags   | Indicates the flags for a mailbox move. <br>Can be one of the following: <br>CrossOrg<br>IntraOrg<br>MoveOnlyArchiveMailbox<br>MoveOnlyPrimaryMailbox<br>None<br>Offline<br>Protected<br>Pull<br>Push<br>RemoteLegacy<br>Suspend<br>SuspendWhenReadyToComplete   | String   |
| Mailbox Move Remote Host Name   | Specifies the name of the remote host that is participating in the move.   | String   |
| Mailbox Move Source MDB   | Active Directory identifier of the source database.   | String   |
| Mailbox Move Status   | Indicates the status of a mailbox move. Can be one of the following:<br>AutoSuspended <br>Completed <br>CompletedWithWarning <br>CompletionInProgress <br>Failed <br>InProgress <br>None <br>Queued <br>Suspended   | String   |
| Mailbox Move Target MDB   | Active Directory identifier of the database that the mailbox is being copied to.   | String   |
| Max Receive Size   | Specifies the size limit for received messages.   | String   |
| Max Send Size   | Specifies the size limit for sent messages   | String   |
| Moderated By   | List of users that are responsible for moderating this mailbox.   | String   |
| Moderation Enabled   | Indicates whether moderation is enabled for this mailbox.   | String   |
| Name   | Specifies the name associated with this object.   | String   |
| Object Category   | Specifies the Active Directory object category for this mailbox.   | String   |
| Object Class   | Lists the Active Directory object classes that apply to this mailbox.   | String   |
| On-Premises Organizational Unit   | Specifies the organizational unit for this mailbox.   | String   |
| Organization ID   | Specifies the organization for this mailbox.   | String   |
| Originating Server   | Specifies the originating server.   | String   |
| Partner Object ID   | Specifies the GUID for partner object ID.   | String   |
| Persisted Capabilities   | Specifies the list of persisted capabilities.   | String   |
| Policies Excluded   | Lists the excluded policies.   | String   |
| Policies Included   | Lists the included policies.   | String   |
| Primary SMTP Address   | Specifies the primary SMTP address for the mailbox.   | String   |
| Protocol Settings   | Specifies the protocols used by the mailbox.   | String   |
| Recipient Limits   | Specifies the maximum number of recipients per message that this mailbox can send to.   | String   |
| Recipient Type   | Recipient type.   | String   |
| Recipient Type Details   | Recipient type details.   | String   |
| Reject Messages From   | Rejected sender IDs list.   | String   |
| Reject Messages From DL Members   | Rejected sender IDs list.   | String   |
| Reject Messages From Senders Or Members   | Rejected sender IDs list.   | String   |
| Remote Recipient Type   | Remote recipient type.   | String   |
| Remote Routing Address   | Specifies the SMTP address of the mailbox in the service that's associated with this mail-enabled user.   | String   |
| Require Sender Authentication Enabled   | Indicates whether sender authentication is required.   | String   |
| Retain Deleted Items For   | Specifies the length of time to keep deleted items.   | String   |
| Retention Comment   | Indicates the comment displayed regarding the user's retention hold status.   | String   |
| Retention Hold Enabled   | Indicates whether the contents of the mailbox are subject to retention.   | String   |
| Retention URL   | Specifies the retention policy that is applied to the mailbox.   | String   |
| SAM Account Name   | Specifies the URL for a webpage with details about the organization's message retention policies.   | String   |
| Send Moderation Notifications   | Specifies the moderation notifications for this mailbox   | String   |
| Simple Display Name   | Specifies the simple display name.   | String   |
| Single Item Recovery Enabled   | Indicates whether the Recovery Items folder can be purged.   | String   |
| Skip CA Check   | Indicates whether the client validates that the server certificate is signed by a trusted certification authority (CA) when connecting over Hypertext Transfer Protocol over Secure Socket Layer.   | String   |
| Skip CN Check   | Indicates whether the client validates that the certificate common name (CN) of the server matches the hostname of the server.   | String   |
| Skip Revocation Check   | Indicates whether the connection does not validate the revocation status of the server certificate.   | String   |
| Start Date For Retention Hold   | Indicates the date and time that a retention hold on messages in this mailbox begins.   | String   |
| UM DTMF Map   | UM DTMF Map.   | String   |
| Use SSL   | Indicates whether SSL encryption is used.   | String   |
| User Principal Name   | Specifies the principal name for the mail box user.   | String   |
| When Changed   | Specifies the date and time when mailbox was changed.   | String   |
| When Changed UTC   | Specifies the UTC date and time when mailbox was changed.   | String   |
| When Created   | Specifies the date and time when mailbox was created.   | String   |
| When Created UTC   | Specifies the UTC date and time when mailbox was created.   | String   |
| When Mailbox Created   | Specifies the date and time when mailbox was created.   | String   |
| Windows Email Address   | Specifies the Windows email address.   | String   |

#### Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)

