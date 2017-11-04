---
title: Create Mailbox
description: For an on-premises Exchange environment, the Create Mailbox activity creates a new mailbox and a new Active Directory user associated with the new mailbox.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 9edd8363-704d-41dc-8cc6-0c168c27b901
author: cfreemanwa
ms.author: raynew
manager: carmonm
robots: noindex
---
# Create Mailbox

For an on-premises Exchange environment, the Create Mailbox activity creates a new mailbox and a new Active Directory user associated with the new mailbox.

For the Office 365 online environment, the Create Mailbox activity can create a new user with a mailbox in the cloud-based email service.

The following tables list the required properties, optional properties, and published data for the Create Mailbox activity.

## Required properties for the Create Mailbox activity

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| User Principal Name | Logon name for the user. This user principal name (UPN) consists of a user name and a suffix. Typically, the suffix is the domain name where the user account resides (Example: chris@contoso.com). <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. "On-premises" refers to computing resources that are located within your own facilities. <br><br> | String   |
| Name   | The user's name that appears in listings of Active Directory Users and Computers.   | String   |
| Alias   | The user's email alias that will appear in Active Directory.   | String   |

## Optional properties for the Create Mailbox activity

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Account Disabled   | Indicates whether the mailbox is to be created in a disabled state. Default is True, when selected. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | True, False   |
| Active Sync Mailbox Policy   | The name or identity of the mailbox policy to enable for the new mailbox. If not configured, the default mailbox policy is used.   | String   |
| Address Book Policy   | The name or identity of the address book policy to apply to this mailbox. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | String   |
| Arbitration   | Indicates if the new mailbox is an arbitration mailbox. Arbitration mailboxes are used for managing approval workflow - handling moderated recipients and distribution group membership approval. Default is True, when selected. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | True, False   |
| Arbitration Mailbox   | The mailbox that is used to manage the moderation process. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | String   |
| Archive   | Indicates whether to create an archive mailbox for the specified user. Default is True, when selected. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | True, False   |
| Archive Database   | The Exchange database (GUID or database name) that contains the archive associated with the new mailbox. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | String   |
| Archive Domain   | The cloud-based services domain on which the archive for this mailbox exists. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | String   |
| Database   | The Exchange database (GUID or database name) that contains the new mailbox. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | String   |
| Discovery   | Identifies the new mailbox as a Discovery mailbox. Discovery mailboxes are created as target mailboxes for Discovery searches. After being created or enabled, a Discovery mailbox cannot be repurposed or converted to another type of mailbox. Default is True, when selected.   | True, False   |
| Display Name   | The display name for the new user that is created with this mailbox.   | String   |
| Domain Controller   | The fully qualified domain name (FQDN) of the domain controller that writes this configuration change to Active Directory. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | String   |
| Equipment   | Identifies the new mailbox as equipment if this mailbox is a resource mailbox.   | True, False   |
| Evict Live Id (Live@edu only)   | Specifies the activity to remove an unmanaged Windows Live ID from the cloud-based domain. An unmanaged Windows Live ID is an ID that was created in the domain before the domain was enrolled in the cloud-based service. The Evict Live Id property applies to cloud-based service. It is not available for on-premises deployments. Default is True, when selected. <br><br><strong>Note </strong><br> This property is available only in the Live@edu environment. <br><br>   | True, False   |
| Federated Identity   | Associates an on-premises Active Directory user with a Microsoft Office user. This property applies to cloud-based service. It isn't available for on-premises deployments.   | String   |
| First Name   | The first name of the new Active Directory user.   | String   |
| Immutable ID   | Specifies a unique and immutable identifier in the form of an SMTP address for an Exchange mailbox which is used for federated delegation when requesting Security Assertion Markup Language (SAML) tokens.   | String   |
| Import Live Id (Live@edu only)   | Imports an unmanaged Windows Live ID into the cloud-based domain. An unmanaged Windows Live ID was created in the domain before the domain was enrolled in the cloud-based service. This property applies to cloud-based service. It isn't available for on-premises deployments. Default is True, when selected. <br><br><strong>Note </strong><br> This property is available only in the Live@edu environment. <br><br>   | True, False   |
| Initials   | The initials of the new Active Directory user.   | String   |
| Last Name   | The last name of the new Active Directory user.   | String   |
| Linked Domain Controller   | The domain controller in the forest where the user account resides. The domain controller in this forest is used to get security information for the account specified by the Linked Master Account property. This property is required only if you're creating a linked mailbox. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | String   |
| Linked Domain Password   | Specifies password used to access the domain controller specified by the Linked Domain Controller property. This property is optional, even if when enabling a linked mailbox.   | String   |
| Linked Domain User Name   | Specifies user name used to access the domain controller specified by the Linked Domain Controller property. This property is optional, even if when enabling a linked mailbox. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | String   |
| Linked Master Account   | The master account in the forest where the user account resides. The master account is the account to link the mailbox to. The master account grants access to the mailbox. This property is required only for creating a linked mailbox. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br> This property can be the following value types:<br>Alias <br>Canonical DN <br>Display Name <br>Distinguished Name (DN) <br>Domain\\Account <br>GUID <br>Immutable ID <br>Legacy Exchange DN <br>SMTP Address <br>User Principal Name <br> | String   |
| Mailbox Plan   | The mailbox plan to associate with this mailbox. A mailbox plan specifies the permissions and features that are available to a mailbox user. The mailbox plan name must be included in the service plan of the organization in which this mailbox resides.<br>This property is available for multi-tenant deployments. This property applies to objects in the cloud-based service. It is not available for on-premises deployments.   | String   |
| Managed Folder Mailbox Policy   | The name or identity of the managed folder mailbox policy to apply to the new mailbox. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | String   |
| Managed Folder Mailbox Policy Allowed | Indicates whether to bypass the warning that messaging records management (MRM) features aren't supported for email clients using versions of Microsoft Outlook earlier than Office Outlook 2007. Default is True, when selected. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | True, False   |
| Microsoft Online Services ID   | ID that allows access to Microsoft Online Services. <br><br><strong>Note </strong><br> This property is available only in the Office 365 environment. <br><br>   | String   |
| Moderated By   | A comma-separated list of users who are responsible for moderating the messages sent to this mailbox.   | String   |
| Moderation Enabled   | Indicates whether to enable moderation for the mailbox. Default is True, when selected.   | True, False   |
| Office   | The Microsoft Office attribute for this mailbox   | String   |
| Organization   | The organization in which this Create Mailbox action will be performed. This property is used for multi-tenant deployments. It is not available for on-premises deployments.   | String   |
| Organizational Unit   | The container where the user is created.   | String   |
| Override Recipient Quotas   | Specifies that the recipient quotas for this mailbox can be overridden. Mailboxes that are part of a tenant organization will use the quotas defined in the tenant organization's service plan. Use this property to allow the command to skip the tenant-level recipient quotas check. This property is used for multi-tenant deployments. It isn't available for on-premises deployments. Default is True, when selected.   | True, False   |
| Password   | The initial password for the newly created user. Not required when creating a linked mailbox, resource mailbox, or shared mailbox because the user account for these types of mailboxes is disabled.   | String   |
| Password Confirm   | Confirm the password.   | String   |
| Phone   | The user's telephone number for the new mailbox.   | String   |
| Primary SMTP Address   | The primary SMTP address of the mailbox.   | String   |
| Query Base DN Restriction Enabled   | Specifies whether to restrict a user's ability to view or search for other mailboxes in their organization. This property is used for multi-tenant deployments. It isn't available for on-premises deployments. Default is True, when selected.   | True, False   |
| Remote Archive   | Specifies whether to disconnect the remote archive for this mailbox. A remote archive exists in a cloud-based service. This property cannot be used in conjunction with the Archive property. Default is True, when selected. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | True, False   |
| Remote Power Shell Enabled   | Specifies whether the user can use Remote PowerShell. Remote PowerShell is required in order to open the Exchange Management Shell or the Exchange Management Console on Mailbox, Hub Transport, Unified Messaging, and Client Access servers. Default is True, when selected.   | True, False   |
| Reset Password On Next Logon   | Specifies whether the user must reset the password upon first logon to the new mailbox. Default is True, when selected.   | True, False   |
| Resource Capacity   | Specifies capacity for a new resource mailbox. For example, for a room resource mailbox, specify the maximum occupancy of the room.   | Int32   |
| Retention Policy   | The name or identity of a retention policy to be applied to the new mailbox. Retention policies consist of tags that are applied to mailbox folders and mail items to determine the period of time that the items should be retained. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | String   |
| Role Assignment Policy   | The name or identity of the management role assignment policy to apply to the new mailbox. When this property is not configured, the Default Role Assignment Policy is used.   | String   |
| Room   | Specifies a new resource mailbox as a room. Default is True, when selected.   | True, False   |
| SAM Account Name   | The logon name used to support clients and servers running older versions of the operating system, such as Microsoft Windows NT 4.0, Windows 95, Windows 98, and LAN Manager. This attribute must be less than 20 characters in length in order to support older clients. If not specified, Active Directory automatically creates a SAMAccountName attribute based on the UPN. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | String   |
| Send Modification Notifications   | Specifies whether status notifications are to be sent to users when they send a message to the moderated mailbox. Default is blank.   | Always<br>Internal<br>Never |
| Shared   | Specifies the new mailbox as a shared mailbox. A shared mailbox is a mailbox to which multiple users can log on. A shared mailbox is not specifically associated with any of the users that can log on. It's associated with a disabled user account. Default is True, when selected.   | True, False   |
| Sharing Policy   | The name or identity of the sharing policy applied to the new mailbox. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | String   |
| Throttling Policy   | The name or identity of the throttling policy to be applied to the new mailbox. <br><br><strong>Note </strong><br> This property is available only in an on-premises environment. <br><br>   | String   |
| Use Existing Live Id (Live@edu only)  | Specifies whether to use the Windows Live ID that already exists in the cloud-based domain. The specified Windows Live ID cannot have a mailbox associated with it. This property applies to cloud-based service. It is not available for on-premises deployments. <br><br><strong>Note </strong><br> This property is available only in the Live@edu environment. <br><br>   | True, False   |
| Windows Live ID (Live@edu only)   | The Windows Live ID of the new mailbox. <br><br><strong>Note </strong><br> This property is available only in the Live@edu environment. <br><br>   | String   |

## Published data for the Create Mailbox activity

| **Element**   | **Description**   | **Value Type** |
|:---|:---|:---|
| Accept Messages Only From   | Mailbox users and mail-enabled contacts that can send email messages to this distribution group.   | String   |
| Accept Messages Only From DL Members   | Distribution list that are allowed to send email messages to this mailbox.   | String   |
| Address Book Policy   | Address book policy for the mailbox.   | String   |
| Address List Membership   | Address list IDs.   | String   |
| Alias   | Mail nickname of the user.   | String   |
| Antispam Bypass Enabled   | Indicates whether anti-spam processing is to be used on the mailbox.   | String   |
| Arbitration Mailbox   | ID of the arbitration mailbox.   | String   |
| Archive Database   | ID of the archive database.   | String   |
| Archive Domain   | Archive domain name.   | String   |
| Archive GUID   | Unique identifier for the archive of this mailbox.   | String   |
| Archive Name   | Name of the archive mailbox.   | String   |
| Archive Quota   | Maximum size of the archive mailbox.   | String   |
| Archive Release   | Archive release   | String   |
| Archive State   | Indicates the state of the mailbox archive. This property can be one of the following values:<br>HostedPending <br>HostedProvisioned <br>Local <br>None <br>OnPremise   | String   |
| Archive Status   | Indicates archive status (Active or None).   | String   |
| Archive Warning Quota   | Mailbox size at which a warning message is sent.   | String   |
| Audit Admin   | List of admin operations which are logged. This property can be one of the following values: <br>Copy<br>Create<br>FolderBind<br>HardDelete<br>MessageBind<br>Move<br>MoveToDeletedItems<br>None<br>SendAs<br>SendOnBehalf<br>SoftDelete<br>Update   | String   |
| Audit Delegate   | List of delegate options which are logged. This property can be one of the following values: <br>Copy<br>Create<br>FolderBind<br>HardDelete<br>MessageBind<br>Move<br>MoveToDeletedItems<br>None<br>SendAs<br>SendOnBehalf<br>SoftDelete<br>Update   | String   |
| Audit Enabled   | Indicates whether audit logging is enabled for the mailbox.   | String   |
| Audit Log Age Limit   | Amount of time audit log entries are retained in the mailbox.   | String   |
| Audit Owner   | List of owner operations which are logged. This property can be one of the following values: <br>Copy<br>Create<br>FolderBind<br>HardDelete<br>MessageBind<br>Move<br>MoveToDeletedItems<br>None<br>SendAs<br>SendOnBehalf<br>SoftDelete<br>Update   | String   |
| Bypass Moderation From Senders Or Members   | List of senders for whom moderation is to be bypassed.   | String   |
| Calendar Repair Disabled   | Indicates whether calendar items in this mailbox are to be repaired by the Calendar Repair Assistant.   | String   |
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
| Display Name   | Display name for the mailbox user.   | String   |
| Distinguished Name   | Distinguished name for the object.   | String   |
| Downgrade High Priority Messages Enabled   | Indicates whether high-priority messages sent to an X.400 mail system are changed to normal priority.   | String   |
| Email Address Policy Enabled   | Indicates whether Email Address Policy is enabled.   | String   |
| Email Addresses   | Collection of email addresses for the mailbox.   | String   |
| End Date For Retention Hold   | Date and time that retention hold on messages in this mailbox expires.   | DateTime   |
| Exchange Environment   | Indicates the type of Exchange environment where this activity will be executed.   | String   |
| Exchange GUID   | Globally unique identifier of the Microsoft Exchange installation.   | String   |
| Exchange PowerShell Application   | The application name segment of the connection URI.   | String   |
| Exchange Server Host   | The connected Exchange server host machine.   | String   |
| Exchange Server Port   | The connected Exchange server port.   | String   |
| Exchange User Account Control   | A mask that is used to retrieve the user account control flags associated with this mailbox. This property can be one of the following values:<br>AccountDisabled <br>CannotChangePassword <br>DoNotExpirePassword <br>DoNotRequirePreauthentication <br>EncryptedTextPasswordAllowed <br>HomeDirectoryRequired <br>InterDomainTrustAccount <br>Lockout <br>MnsLogonAccount <br>None <br>NormalAccount <br>NotDelegated <br>PasswordExpired <br>PasswordNotRequired <br>Script <br>ServerTrustAccount <br>SmartCardRequired <br>TemporaryDuplicateAccount <br>TrustedForDelegation <br>TrustedToAuthenticateForDelegation <br>UseDesKeyOnly <br>WorkstationTrustAccount   | String   |
| Exchange User Name   | Username that is used to log on to the Exchange server.   | String   |
| Exchange Version   | Version of Microsoft Exchange that this object is associated with.   | String   |
| ExtensionCustomAttribute1   | Extension custom attribute 1.   | String   |
| ExtensionCustomAttribute2   | Extension custom attribute 2.   | String   |
| ExtensionCustomAttribute3   | Extension custom attribute 3.   | String   |
| ExtensionCustomAttribute4   | Extension custom attribute 4.   | String   |
| ExtensionCustomAttribute5   | Extension custom attribute 5.   | String   |
| Extensions   | List of Extensions.   | String   |
| External Directory Object Id   | External directory object ID.   | String   |
| External OOF Options   | Specifies whether to send Out of Office (OOF) messages to external senders. This property can be one of the following values:<br>InternalOnly<br>External   | String   |
| Forwarding Address   | Forwarding address for the mailbox.   | String   |
| Forwarding SMTP Address   | Forwarding SMTP address for the mailbox.   | String   |
| Grant Send On Behalf To   | List of users with "send on behalf" rights for this mailbox.   | String   |
| GUID   | The globally unique identifier for this object.   | String   |
| Has Picture   | Indicates whether a picture has been associated with this mailbox.   | String   |
| Has Spoken Name   | Indicates whether a spoken name has been associated with this mailbox.   | String   |
| Hidden From Address Lists Enabled   | Indicates whether mailbox information is hidden from address book display.   | String   |
| Identity   | Mailbox identity.   | String   |
| Immutable Id   | Identifier for the mailbox that will never change.   | String   |
| Include In Garbage Collection   | Indicates whether the Include In Garbage Collection property is enabled.   | String   |
| Is Linked   | Indicates whether a mailbox is linked.   | String   |
| Is Machine To Person Text Messaging Enabled | Indicates whether the server can send text messages to a user.   | String   |
| Is Mailbox Enabled   | Indicates whether the mailbox is enabled to process messages.   | String   |
| Is Person To Person Text Messaging Enabled  | Indicates whether another mailbox user can send a text message to the owner of this mailbox.   | String   |
| Is Resource   | Indicates whether this mailbox represents a resource, such as a conference room.   | String   |
| Is Shared   | Indicates whether this mailbox is shared by more than one user.   | String   |
| Is Soft Deleted By Disable   | Indicates whether the mailbox is soft deleted as a result of a disable operation.   | String   |
| Is Soft Deleted By Remove   | Indicates whether the mailbox is soft deleted as a result of a remove operation.   | String   |
| Issue Warning Quota   | Mailbox size at which a warning message is sent to the user.   | String   |
| Is Valid   | Indicates whether the object is configured correctly.   | String   |
| Languages   | List of preferred languages for this mailbox.   | String   |
| Last Exchange Changed Time   | Last Exchange changed time.   | DateTime   |
| Legacy Exchange DN   | Legacy Exchange DN.   | String   |
| Linked Master Account   | Master account for the linked mailbox.   | String   |
| Litigation Hold Date   | Date and time when litigation hold was enabled.   | DateTime   |
| Litigation Hold Enabled   | Indicates whether the mailbox is under a litigation hold.   | String   |
| Litigation Hold Owner   | User who enabled the litigation hold.   | String   |
| Mail Tip   | Mail tip.   | String   |
| Mail Tip Translations   | Mail tip translation list.   | String   |
| Mailbox Move Batch Name   | Name of the move batch that contains this mailbox.   | String   |
| Mailbox Move Flags   | Flags for a mailbox move. <br> This property can be any of the following values: <br>CrossOrg<br>IntraOrg<br>MoveOnlyArchiveMailbox<br>MoveOnlyPrimaryMailbox<br>None<br>Offline<br>Protected<br>Pull<br>Push<br>RemoteLegacy<br>Suspend<br>SuspendWhenReadyToComplete   | String   |
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
| Max Send Size   | Sent message size limit.   | String   |
| Message Tracking Read Status Enabled   | Indicates whether detailed message tracking is enabled for the mailbox.   | String   |
| Microsoft Online Services ID   | ID that enables access to Microsoft Online Services.   | String   |
| Moderated By   | List of users responsible for moderating this mailbox.   | String   |
| Moderation Enabled   | Indicates whether moderation is enabled for this mailbox.   | String   |
| Name   | Name associated with this object.   | String   |
| Needs To Suppress PII   | Needs to Suppress PII (Personally Identifiable Information).   | String   |
| Object Category   | Active Directory object category for this mailbox.   | String   |
| Object Class   | List of Active Directory object classes which apply to this mailbox.   | String   |
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
| Query Base DN Restriction Enabled   | Indicates whether a user can search and view other mailboxes in their organization.   | String   |
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
| Retain Deleted Items Until Backup   | Indicates whether deleted items are to be kept until the database is backed up.   | String   |
| Retention Comment   | The comment that is displayed regarding the user's retention hold status.   | String   |
| Retention Hold Enabled   | Indicates whether the contents of the mailbox are subject to retention.   | String   |
| Retention Policy   | Retention policy that is applied to the mailbox. <br><br><strong>Note </strong><br> This field may not contain data depending on environment or activity configuration. <br><br>   | String   |
| Retention URL   | URL for a webpage with details about the organization's message retention policies.   | String   |
| Role Assignment Policy   | Management role that was assigned to the mailbox when it was created or enabled. <br><br><strong>Note </strong><br> This field may not contain data depending on environment or activity configuration. <br><br>   | String   |
| Rules Quota   | Size limit for rules.   | String   |
| SAM Account Name   | User name for earlier operating systems.   | String   |
| SCL Delete Enabled   | Indicates whether messages that meet the spam confidence level (SCL) are deleted.   | String   |
| SCL Delete Threshold   | Spam confidence level (SCL) at which messages are considered spam and are to be deleted.   | Number   |
| SCL Junk Enabled   | Indicates whether messages that meet the spam confidence level (SCL) are moved to the Junk E-Mail folder.   | String   |
| SCL Junk Threshold   | Spam confidence level (SCL) at which messages are considered spam and are to be moved to the Junk E-Mail folder.   | Number   |
| SCL Quarantine Enabled   | Indicates whether messages that meet the spam confidence level (SCL) are quarantined.   | String   |
| SCL Quarantine Threshold   | Spam confidence level (SCL) at which messages are considered spam and are to be moved to the quarantine folder.   | Number   |
| SCL Reject Enabled   | Indicates whether messages that meet the spam confidence level (SCL) are rejected.   | String   |
| SCL Reject Threshold   | Spam confidence level (SCL) at which messages are considered spam and are to be rejected.   | Number   |
| SKU Assigned   | This parameter is reserved for internal Microsoft use.   | String   |
| Send Moderation Notifications   | Moderation notifications for this mailbox.<br>This property can be one of the following values:<br>Always <br>Internal <br>Never   | String   |
| Server Legacy DN   | Legacy domain name for the server.   | String   |
| Server Name   | Name of the server.   | String   |
| Simple Display Name   | Simple display name.   | String   |
| Single Item Recovery Enabled   | Indicates whether the Recovery Items folder can be purged.   | Boolean   |
| Skip CA Check   | Indicates whether the client skips validation that the server certificate is signed by a trusted certification authority (CA) for connection over Hypertext Transfer Protocol over Secure Socket Layer.   | String   |
| Skip CN Check   | Indicates whether the client skips validation that the certificate common name (CN) of the server matches the hostname of the server.   | String   |
| Skip Revocation Check   | Indicates whether the connection skips validation of the revocation status of the server certificate.   | String   |
| Start Date For Retention Hold   | Date and time that a retention hold on messages in this mailbox begins.   | DateTime   |
| Throttling Policy   | Identifier for the throttling policy applied to the mailbox.   | String   |
| UM DTMF Map   | UM DTMF Map.   | String   |
| UM Enabled   | Indicates whether Unified Messaging (UM) is enabled for this mailbox.   | String   |
| Usage Location   | Country name.   | String   |
| Use Database Quota Defaults   | Indicates whether this mailbox uses the database defaults for quota properties.   | String   |
| Use Database Retention Defaults   | Indicates whether this mailbox uses the mailbox retention policy that is specified for the mailbox database that contains the mailbox.   | String   |
| Use SSL   | Indicates whether SSL encryption is used.   | String   |
| User Principal Name   | Principal name for the mailbox user.   | String   |
| When Changed   | Date and time when mailbox was changed.   | DateTime   |
| When Changed UTC   | UTC date and time when mailbox was changed.   | DateTime   |
| When Created   | Date and time when mailbox was created.   | DateTime   |
| When Created UTC   | UTC date and time when mailbox was created.   | DateTime   |
| When Mailbox Created   | Date and time when mailbox was created.   | DateTime   |
| When Soft Deleted   | Date and time when mailbox was soft deleted.   | DateTime   |
| Windows Email Address   | Email address.   | String   |
| Windows Live ID(Live@edu only)   | Windows Live ID associated with the mailbox.   | String   |

## See Also

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)
