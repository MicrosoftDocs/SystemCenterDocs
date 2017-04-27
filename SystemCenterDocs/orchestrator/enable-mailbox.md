---
title: Enable Mailbox
description: You can use the Enable Mailbox activity in an on-premises environment to enable a mailbox for an existing Active Directory user or InetOrgPerson object.
ms.custom: na
ms.date: 4/25/2017
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 1825d27b-c016-4d16-8237-350fbced1686
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
---

# Enable Mailbox

Applies To: System Center 2016 - Orchestrator

You can use the Enable Mailbox activity in an on-premises environment to enable a mailbox for an existing Active Directory user or InetOrgPerson object. This activity creates additional mailbox attributes on the user object in Active Directory. When the user logs on to the mailbox or receives email messages, the system creates a mailbox object in the Exchange database.

For an online cloud-based environment, you can use this activity with the Archive parameter to enable an archive for an existing mailbox.

The following tables list the required properties, optional properties, and published data for this activity.

## Required properties for the Enable Mailbox activity

| **Element** | **Description**   | **Valid values** |
|:---|:---|:---|
| Identity   | Identifies the Active Directory user. This property can be one of the following value types:<br>ADObjectID <br>GUID <br>Distinguished name (DN)<br>Domain\\SamAccountName<br>User principal name (UPN)<br>LegacyExchangeDN<br>Email Address<br>User alias | String   |

## Optional properties for the Enable Mailbox activity

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Active Sync Mailbox Policy   | Specifies the name or identity of the mailbox policy to apply to the new mailbox. If this property is not configured, the default mailbox policy will be applied. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | String   |
| Address Book Policy   | Specifies the name or identity of the address book policy to apply to this new mailbox. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | String   |
| Alias   | The mail nickname of the user. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | String   |
| Arbitration   | Specifies that the newly enabled mailbox is an arbitration mailbox. Arbitration mailboxes are used for managing approval workflow. For example, an arbitration mailbox is used for handling moderated recipients and distribution group membership approval.<br>Default is True, when selected. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | True, False   |
| Archive   | Specifies whether to disconnect the archive mailbox from the associated mailbox user. This property cannot be used with the Remote Archive property.<br>Default is True, when selected. <br><br><strong>Note </strong><br> This property is not available in the Live@edu environment. <br><br>   | True, False   |
| Archive Database   | The archive mailbox database. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | String   |
| Archive Domain   | Specifies the cloud-based services domain on which the archive associated with this mailbox exists. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | String   |
| Archive Name   | The archive mailbox name. <br><br><strong>Note </strong><br> This property is not available in the Live@edu environment. <br><br>   | String   |
| Bypass Moderation From Senders or Members | A list of Senders or Members of a list whose messages are not subject to approval. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | String   |
| Database   | The Exchange database (GUID or database name) that contains the new mailbox. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | String   |
| Discovery   | Specifies the mailbox as a Discovery mailbox. Discovery mailboxes are created as target mailboxes for Discovery searches. After being created or enabled, a Discovery mailbox cannot be repurposed or converted to another type of mailbox.<br>Default is True, when selected. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | True, False   |
| Display Name   | The contents of the Simple Display Name field. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | String   |
| Domain Controller   | The fully qualified domain name (FQDN) of the domain controller that writes this configuration change to Active Directory. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | String   |
| Equipment   | Specifies the new mailbox as equipment if this mailbox is a resource mailbox.<br>Default is True, when selected. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | True, False   |
| Linked Domain Controller   | The domain controller in the forest where the user account resides. This domain controller is used to get security information for the account specified by the Linked Master Account property. This property is required only if you are creating a linked mailbox. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | String   |
| Linked Domain Password   | The password that is used to access the domain controller specified by the Linked Domain Controller property. This property is optional, even if when enabling a linked mailbox. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | String   |
| Linked Domain User Name   | The user name that is used to access the domain controller specified by the Linked Domain Controller property. This property is optional, even if when enabling a linked mailbox. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | String   |
| Linked Master Account   | The master account in the forest where the user account resides. This master account is the account to link the mailbox to. The master account grants access to the mailbox. This property is required only if you are creating a linked mailbox.<br>This property can be one of the following value types:<br>GUID <br>DN<br>Domain\\Account <br>UPN<br>LegacyExchangeDN<br>SmtpAddress<br>Alias <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br> | String   |
| Managed Folder Mailbox Policy Allowed   | Specifies whether to bypass the warning that messaging records management (MRM) features are not supported for email clients using versions of Microsoft Outlook earlier than Office Outlook 2007.<br>Default is True, when selected. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | True, False   |
| Managed Folder Mailbox Policy   | The name or identity of the managed folder mailbox policy to apply to the mailbox. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | String   |
| Primary SMTP Address   | Primary SMTP address for the mailbox. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | String   |
| Remote Archive   | Specifies whether to disconnect the remote archive for this mailbox. When you enable this property, the RemoteRecipientType property for the mailbox is reset to specify that this mailbox does not have a remote archive. A remote archive exists in a cloud-based service. This property cannot be used with the Archive property. <br>Default is True, when selected. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | True, False   |
| Retention Policy   | The retention policy that is applied to the mailbox. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | String   |
| Role Assignment Policy   | The management role that was assigned to the mailbox when it was created or enabled. <br><br><strong>Note </strong><br> This property is not available in the Live@edu environment. <br><br>   | String   |
| Room   | Specifies that the mailbox in the service is to be created as a room resource mailbox. <br>This property cannot be set to True when the Equipment property is also set to True.<br>Default is True, when selected. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | True, False   |
| Shared   | Specifies the new mailbox as a shared mailbox. A shared mailbox is a mailbox to which multiple users can log on. A shared mailbox is not associated with any of the users that can log on. It is associated with a disabled user account. <br>Default is True, when selected. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | True, False   |

## Published data for the Enable Mailbox activity

| Element   | Description   | Valid values |
|:---|:---|:---|
| Accept Messages Only From   | Mailbox users and mail-enabled contacts that can send email messages to this distribution group.   | String   |
| Accept Messages Only From DL Members   | Distribution list that are allowed to send email messages to this mailbox.   | String   |
| Accept Messages Only From Senders Or Members | Senders or members that are allowed to send email messages to this distribution group.   | String   |
| Address Book Policy   | Address book policy for the mailbox.   | String   |
| Address List Membership   | Address list IDs.   | String   |
| Alias   | Mail nickname of the user.   | String   |
| Antispam Bypass Enabled   | Indicates whether anti-spam processing is to be used on the mailbox.   | String   |
| Arbitration Mailbox   | ID of the arbitration mailbox.   | String   |
| Archive Database   | ID of the archive database.   | String   |
| Archive Domain   | Archive domain name.   | String   |
| Archive GUID   | Unique archive identifier for the mailbox.   | String   |
| Archive Name   | Name of the archive mailbox.   | String   |
| Archive Quota   | Maximum size of the archive mailbox.   | String   |
| Archive Release   | Archive release.   | String   |
| Archive State   | Indicates the state of the mailbox archive. This property can be one of the following values:<br>HostedPending <br>HostedProvisioned <br>Local <br>None <br>OnPremise   | String   |
| Archive Status   | Indicates archive status (Active or None).   | String   |
| Archive Warning Quota   | Mailbox size at which a warning message is sent.   | String   |
| Audit Admin   | List of admin operations that are logged. This property can be one of the following values: <br>Copy<br>Create<br>FolderBind<br>HardDelete<br>MessageBind<br>Move<br>MoveToDeletedItems<br>None<br>SendAs<br>SendOnBehalf<br>SoftDelete<br>Update   | String   |
| Audit Delegate   | List of delegate options that are logged. This property can be one of the following values: <br>Copy<br>Create<br>FolderBind<br>HardDelete<br>MessageBind<br>Move<br>MoveToDeletedItems<br>None<br>SendAs<br>SendOnBehalf<br>SoftDelete<br>Update   | String   |
| Audit Enabled   | Indicates whether audit logging is enabled or disabled for the mailbox.   | String   |
| Audit Log Age Limit   | Amount of time audit log entries are retained in the mailbox.   | String   |
| Audit Owner   | List of owner operations that are logged. This property can be one of the following values: <br>Copy<br>Create<br>FolderBind<br>HardDelete<br>MessageBind<br>Move<br>MoveToDeletedItems<br>None<br>SendAs<br>SendOnBehalf<br>SoftDelete<br>Update   | String   |
| Bypass Moderation From Senders Or Members   | List of senders for whom moderation is to be bypassed.   | String   |
| Calendar Repair Disabled   | Indicates whether calendar items in this mailbox will be repaired by the Calendar Repair Assistant.   | String   |
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
| Deliver To Mailbox And Forward   | The forwarding address of the mailbox.   | String   |
| Disabled Archive Database   | Indicates whether the use of an Archive Database is disabled.   | String   |
| Disabled Archive GUID   | Indicates whether the use of Archive GUIDs is disabled.   | String   |
| Display Name   | Display name for the mailbox user.   | String   |
| Distinguished Name   | Distinguished name for the object.   | String   |
| Downgrade High Priority Messages Enabled   | Indicates whether high-priority messages sent to an X.400 mail system are changed to normal priority.   | String   |
| Email Address Policy Enabled   | Indicates whether Email Address Policy is enabled.   | String   |
| Email Addresses   | Collection of email addresses for the mailbox.   | String   |
| End Date For Retention Hold   | Date and time that retention hold on messages in this mailbox is set to expire.   | DateTime   |
| Exchange Environment   | Indicates the type of Exchange environment where this activity will be executed.   |   |
| Exchange GUID   | Globally unique identifier of the Microsoft Exchange installation.   | String   |
| Exchange PowerShell Application   | The application name segment of the connection URI.   | String   |
| Exchange Server Host   | The connected Exchange server host machine.   | String   |
| Exchange Server Port   | The connected Exchange server port.   | String   |
| Exchange User Account Control   | A mask that is used to retrieve the user account control flags associated with this mailbox. This property can be one of the following values:<br>AccountDisabled <br>CannotChangePassword <br>DoNotExpirePassword <br>DoNotRequirePreauthentication <br>EncryptedTextPasswordAllowed <br>HomeDirectoryRequired <br>InterDomainTrustAccount <br>Lockout <br>MnsLogonAccount <br>None <br>NormalAccount <br>NotDelegated <br>PasswordExpired <br>PasswordNotRequired <br>Script <br>ServerTrustAccount <br>SmartCardRequired <br>TemporaryDuplicateAccount <br>TrustedForDelegation <br>TrustedToAuthenticateForDelegation <br>UseDesKeyOnly <br>WorkstationTrustAccount   | String   |
| Exchange User Name   | Username used to log on to Exchange server.   | String   |
| Exchange Version   | Version of Microsoft Exchange that this object is associated with.   | String   |
| Extension Custom Attribute 1   | Extension custom attribute 1.   | String   |
| Extension Custom Attribute 2   | Extension custom attribute 2.   | String   |
| Extension Custom Attribute 3   | Extension custom attribute 3.   | String   |
| Extension Custom Attribute 4   | Extension custom attribute 4.   | String   |
| Extension Custom Attribute 5   | Extension custom attribute 5.   | String   |
| Extensions   | List of extensions.   |   |
| External Directory Object Id   | External directory object ID.   | String   |
| External OOF Options   | Options for sending Out of Office (OOF) messages to external senders. This property can be one of the following values:<br>InternalOnly<br>External   | String   |
| Forwarding Address   | Forwarding address for this mailbox.   | String   |
| Forwarding SMTP Address   | Forwarding SMTP address for this mailbox.   | String   |
| Grant Send On Behalf To   | A list of users with "send on behalf" rights for this mailbox.   | String   |
| GUID   | The globally unique identifier for this object.   | String   |
| Has Picture   | Indicates whether a picture has been associated with this mailbox.   | String   |
| Has Spoken Name   | Indicates whether a spoken name has been associated with this mailbox.   | String   |
| Hidden From Address Lists Enabled   | Indicates whether mailbox information is hidden from address book.   | String   |
| Identity   | Mailbox identity.   | String   |
| Immutable ID   | Identifier for the mailbox that will never change.   | String   |
| Include In Garbage Collection   | Include In Garbage Collection.   | String   |
| Is Linked   | Indicates whether this mailbox is linked.   | String   |
| Is Machine To Person Text Messaging Enabled  | Indicates whether the server can send text messages to a user.   | String   |
| Is Mailbox Enabled   | Indicates whether this mailbox is enabled to process messages.   | String   |
| Is Person To Person Text Messaging Enabled   | Indicates whether another mailbox user can send a text message to the owner of this mailbox.   | String   |
| Is Resource   | Indicates whether this mailbox represents a resource, such as a conference room.   | String   |
| Is Shared   | Indicates whether this mailbox is shared by more than one user.   | String   |
| Is Soft Deleted By Disable   | Indicates whether this mailbox has been soft-deleted as a result of a disable operation.   | String   |
| Is Soft Deleted By Remove   | Indicates whether this mailbox has been soft-deleted as a result of a remove operation.   | String   |
| Issue Warning Quota   | Mailbox size at which a warning message is sent to the user.   | String   |
| Is Valid   | Indicates whether the object is configured correctly.   | String   |
| Languages   | Preferred languages for this mailbox.   | String   |
| Last Exchange Changed Time   | Last Exchange changed time.   | DateTime   |
| Legacy Exchange DN   | Legacy Exchange DN.   | String   |
| Linked Master Account   | Master account for the linked mailbox.   | String   |
| Litigation Hold Date   | Date and time when litigation hold was enabled.   | DateTime   |
| Litigation Hold Enabled   | Indicates whether the mailbox is under a litigation hold.   | String   |
| Litigation Hold Owner   | User who enabled the litigation hold.   | String   |
| Mail Tip   | Mail tip.   | String   |
| Mail Tip Translations   | Mail tip translation list.   | String   |
| Mailbox Move Batch Name   | Name of the move batch that contains this mailbox.   | String   |
| Mailbox Move Flags   | Flags for a mailbox move. This property can be one of the following values: <br>CrossOrg<br>IntraOrg<br>MoveOnlyArchiveMailbox<br>MoveOnlyPrimaryMailbox<br>None<br>Offline<br>Protected<br>Pull<br>Push<br>RemoteLegacy<br>Suspend<br>SuspendWhenReadyToComplete   | String   |
| Mailbox Move Remote Host Name   | Name of the remote host that is participating in the move.   | String   |
| Mailbox Move Source MDB   | Active Directory identifier of the source database.   | String   |
| Mailbox Move Status   | Indicates the status of a mailbox move. This property can be one of the following values:<br>AutoSuspended <br>Completed <br>CompletedWithWarning <br>CompletionInProgress <br>Failed <br>InProgress <br>None <br>Queued <br>Suspended   | String   |
| Mailbox Move Target MDB   | Active Directory identifier of the database that the mailbox is being copied to.   | String   |
| Mailbox Plan   | Mailbox plan for a mailbox.   | String   |
| Mailbox Release   | Mailbox release.   | String   |
| Managed Folder Mailbox Policy   | Messaging Records Management (MRM) policy for the mailbox.   | String   |
| Max Blocked Senders   | Maximum number of senders that can be included in a blocked senders list.   | Number   |
| Max Receive Size   | Received message size limit.   | String   |
| Max Safe Senders   | Maximum number of senders that can be included in a safe senders list.   | Integer   |
| Max Send Size   | Size limit for sent messages.   | String   |
| Message Tracking Read Status Enabled   | Indicates whether detailed message tracking is enabled for the mailbox.   | String   |
| Microsoft Online Services ID   | An ID that allows access to Microsoft Online Services.   | String   |
| Moderated By   | List of users who are responsible for moderating this mailbox.   | String   |
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
| Protocol Settings   | Protocols that are used by the mailbox.   | String   |
| Query Base DN   | This property controls which address list a user can access through Outlook Web App.   | String   |
| Query Base DN Restriction Enabled   | Indicates whether the user can search and view other mailboxes in their organization.   | String   |
| Recipient Limits   | Maximum number of recipients per message that this mailbox can send to.   | String   |
| Recipient Type   | Recipient type. This property can be one of the following values:<br>Computer <br>Contact <br>DynamicDistributionGroup<br>Group <br>Invalid <br>MailContact <br>MailNonUniversalGroup <br>MailUniversalDistributionGroup <br>MailUniversalSecurityGroup <br>MailUser <br>MicrosoftExchange <br>PublicDatabase <br>PublicFolder <br>SystemAttendantMailbox <br>SystemMailbox <br>User <br>UserMailbox   | String   |
| Recipient Type Details   | Recipient type details. This property can be one of the following values:<br>AllUniqueRecipientTypes <br>ArbitrationMailbox <br>Computer <br>Contact <br>DisabledUser <br>DiscoveryMailbox <br>DynamicDistributionGroup <br>EquipmentMailbox <br>LegacyMailbox <br>LinkedMailbox <br>LinkedUser <br>MailboxPlan <br>MailContact <br>MailForestContact <br>MailNonUniversalGroup <br>MailUniversalDistributionGroup <br>MailUniversalSecurityGroup <br>MailUser <br>MicrosoftExchange <br>None <br>NonUniversalGroup <br>PublicFolder <br>RemoteEquipmentMailbox <br>RemoteRoomMailbox <br>RemoteSharedMailbox <br>RemoteUserMailbox <br>RoleGroup <br>RoomList <br>RoomMailbox <br>SharedMailbox <br>SystemAttendantMailbox <br>SystemMailbox <br>UniversalDistributionGroup <br>UniversalSecurityGroup <br>User <br>UserMailbox | String   |
| Reconciliation Id   | Reconciliation ID.   | String   |
| Recoverable Items Quota   | Size limit for the Recovery Items folder.   | String   |
| Recoverable Items Warning Quota   | Size at which a warning is sent that the Recovery Items folder is reaching its limit.   | String   |
| Reject Messages From   | Rejected sender IDs list.   | String   |
| Reject Messages From DL Members   | Rejected sender IDs list.   | String   |
| Reject Messages From Senders Or Members   | Rejected sender IDs list.   | String   |
| Remote Account Policy   | Remote account policy ID.   | String   |
| Remote Recipient Type   | Remote recipient type. This property can be one of the following values:<br>DeprovisionArchive <br>DeprovisionMailbox <br>EquipmentMailbox <br>Migrated <br>None <br>ProvisionArchive <br>ProvisionMailbox <br>RoomMailbox <br>SharedMailbox   | String   |
| Require Sender Authentication Enabled   | Indicates whether sender authentication is required.   | String   |
| Resource Capacity   | Capacity of a resource mailbox.   | Number   |
| Resource Custom   | A list of additional information about a resource.   | String   |
| Resource Type   | Type of a resource.   | String   |
| Retain Deleted Items For   | Length of time to keep deleted items.   | String   |
| Retain Deleted Items Until Backup   | Indicates whether deleted items should be kept until the database is backed up.   | String   |
| Retention Comment   | Comment that is displayed regarding the user's retention hold status.   | String   |
| Retention Hold Enabled   | Indicates whether the contents of the mailbox are subject to retention.   | String   |
| Retention Policy   | Retention policy that is applied to the mailbox.   | String   |
| Retention URL   | URL for a webpage with details about the organization's message retention policies.   | String   |
| Role Assignment Policy   | Management role that was assigned to the mailbox when it was created or enabled.   | String   |
| Rules Quota   | Size limit for rules.   | String   |
| SAM Account Name   | User name for use with earlier operating systems.   | String   |
| SCL Delete Enabled   | Indicates whether messages that meet the spam confidence level (SCL) are deleted.   | String   |
| SCL Delete Threshold   | Spam confidence level (SCL) at which messages are considered spam and should be deleted.   | Number   |
| SCL Junk Enabled   | Indicates whether messages that meet the spam confidence level (SCL) are moved to the Junk E-Mail folder.   | String   |
| SCL Junk Threshold   | Spam confidence level (SCL) at which messages are considered spam and are to be moved to the Junk E-Mail folder.   | Number   |
| SCL Quarantine Enabled   | Indicates whether messages that meet the spam confidence level (SCL) are quarantined.   | String   |
| SCL Quarantine Threshold   | Spam confidence level (SCL) at which messages are considered spam and are to be moved to the quarantine folder.   | Number   |
| SCL Reject Enabled   | Indicates whether messages that meet the spam confidence level (SCL) are rejected.   | String   |
| SCL Reject Threshold   | Spam confidence level (SCL) at which messages are considered spam and are to be rejected.   | Number   |
| SKU Assigned   | This parameter is reserved for internal Microsoft use.   | String   |
| Send Moderation Notifications   | Moderation notifications for this mailbox. This property can be one of the following values:<br>Always <br>Internal <br>Never   | String   |
| Server Legacy DN   | Legacy domain name for the server.   | String   |
| Server Name   | Name of the server.   | String   |
| Simple Display Name   | Simple display name.   | String   |
| Single Item Recovery Enabled   | Indicates whether the Recovery Items folder can be purged.   |   |
| Skip CA Check   | Indicates whether the client skips validation that the server certificate is signed by a trusted certification authority (CA) when connecting over Hypertext Transfer Protocol (HTTP) over Secure Sockets Layer (SSL).   | String   |
| Skip CN Check   | Indicates whether the client skips validation that the certificate common name (CN) of the server matches the hostname of the server.   | String   |
| Skip Revocation Check   | indicates whether the connection skips validation of the revocation status of the server certificate.   | String   |
| Start Date For Retention Hold   | Date and time that a retention hold on messages in this mailbox begins.   | DateTime   |
| Throttling Policy   | Identifier for the throttling policy applied to the mailbox.   | String   |
| UM DTMF Map   | UM DTMF Map.   | String   |
| UM Enabled   | Indicates whether Unified Messaging (UM) is enabled for this mailbox.   | String   |
| Usage Location   | Country name.   | String   |
| Use Database Quota Defaults   | Indicates whether this mailbox uses the database defaults for quota properties.   | String   |
| Use Database Retention Defaults   | Indicates whether this mailbox uses the mailbox retention policy specified for the mailbox database that contains the mailbox.   | String   |
| Use SSL   | Indicates whether SSL encryption is used.   | String   |
| User Principal Name   | The principal name for the mailbox user.   | String   |
| When Changed   | Date and time when mailbox was changed.   | DateTime   |
| When Changed UTC   | UTC date and time when mailbox was changed.   | DateTime   |
| When Created   | Date and time when mailbox was created.   | DateTime   |
| When Created UTC   | UTC date and time when mailbox was created.   | DateTime   |
| When Mailbox Created   | Date and time when mailbox was created.   | DateTime   |
| When Soft Deleted   | Date and time when mailbox was soft deleted.   | DateTime   |
| Windows Email Address   | Email address .   | String   |
| Windows Live ID (Live@edu only)   | Windows Live ID associated with the mailbox.   | String   |

