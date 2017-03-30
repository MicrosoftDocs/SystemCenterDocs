---
title: Create Move Request
description: You can use the Create Move Request activity to create a new mailbox move request and to begin the process of an asynchronous mailbox or personal archive move for an on-premises environment.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 346a8baa-10d7-4d04-931e-82f12ebf6c58
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Create Move Request

Applies To: System Center 2016 - Orchestrator

You can use the Create Move Request activity to create a new mailbox move request and to begin the process of an asynchronous mailbox or personal archive move for an on-premises environment.

The following tables list the required properties, optional properties, and published data for this activity.

## Required properties for the Create Move Request activity

| **Element** | **Description**   | **Valid values** |
|:---|:---|:---|
| Identity   | Specifies the identity of the mailbox or mail user. This can be one of the following value types:<br>Globally unique identifier (GUID)<br>Distinguished name (DN)<br>Domain\\Account <br>User principal name (UPN)<br>LegacyExchangeDN<br>SMTP address<br>Alias | String   |

## Optional properties for the Create Move Request activity

| **Element**   | **Description**   | **Valid values** |
|:---|:---|:---|
| Accept Large Data Loss   | Specifies that a large amount of data loss is acceptable if the Bad Item Limit property is set to 51 or higher. An item is considered corrupted if it cannot be read from the source database or cannot be written to the target database. Corrupted items will not be available in the destination mailbox or .pst file. <br>Default is True, when selected.   | True, False   |
| Archive Domain   | Specifies the fully qualified domain name (FQDN) of the external domain to which the archive is moved. This property is used to move the archive to a cloud-based service.   | String   |
| Archive Only   | Specifies that only the personal archive associated with the mailbox is to be moved. This property cannot be set to True when the Primary Only property is True.<br>Default is True, when selected.   | True, False   |
| Archive Target Database   | Specifies the target database for the new location of the personal archive. If a target database is not specified, the archive is moved to the same database as the primary mailbox. If a target database is not specified and the Archive Only property is True, the archive is moved to the homeMDB attribute of the primary mailbox. <br>This can be one of the following value types:<br>GUID of the database<br>Database name   | String   |
| Bad Item Limit   | Specifies the allowable number of bad items to skip if the request encounters corrupted items in the mailbox. Use 0 to not skip bad items. The valid input range for this property is from 0 through 2147483647. The default value is 0. <br> In general, you should keep the default value of 0 and only change the Bad Item Limit property value if the request fails.<br>If you set the Bad Item Limit property to more than 50 and the command fails due to excessive corrupt items, the system displays a warning: "Please confirm your intention to accept a large amount of data loss by specifying Accept Large Data Loss." If this occurs, you can run the command with the Accept Large Data Loss property set to True. No further warnings will appear and the corrupted items will become unavailable after the process is complete. | Integer   |
| Batch Name   | Specifies a descriptive name for moving a batch of mailboxes. The name can then be used in the Batch Name property as a search string for the Get Move Request mode.   | String   |
| Do Not Preserve Mailbox Signature | Specifies that the command will not preserve the mailbox mapping signature. <br>Generally, you should enable this property only if the move request fails due to depletion of Named Property identifiers. When this property is set to True, the mailbox user must restart Microsoft Outlook after the move request is complete. <br>Default is True, when selected.   | True, False   |
| Domain Controller   | Specifies the FQDN of the domain controller that writes this configuration change to Active Directory.   | String   |
| Ignore Rule Limit Errors   | Specifies that the command will not move the user's rules to the target server that runs Exchange.<br>Default is True, when selected.   | True, False   |
| MRS Server   | Specifies the FQDN of the Client Access server that runs the Microsoft Exchange Mailbox Replication service (MRS). This property is used for debugging purposes only.   | String   |
| Outbound   | Specifies that a cross-forest mailbox move is to be initiated from the source forest. <br>Default is True, when selected.   | True, False   |
| Primary Only   | Specifies that the command will only move the primary mailbox and will not move the personal archive. This property cannot be set to True when the Archive Only property is True.<br>Default is True, when selected.   | True, False   |
| Remote   | Specifies that the move is outside the organization and that this move is being initiated from the target forest. This property cannot be set to True when the Outbound property is True.<br>Default is True, when selected.   | True, False   |
| Remote Archive Target Database   | Specifies the name of the target database in the remote forest for the new location of the personal archive. Use this property to move users with archives from the local forest to a remote forest. For moves from a remote forest to the local forest, use the Archive Target Database property.<br>When you use this property, you must also specify the Remote or Remote Legacy property.   | String   |
| Remote Credential Password   | Specifies the password for the administrator identified in the Remote Credential User Name property.   | String   |
| Remote Credential User Name   | Specifies user name for an administrator who has permission to perform the mailbox move.   | String   |
| Remote Global Catalog   | Specifies the FQDN of the global catalog server for the remote forest.   | String   |
| Remote Host Name   | Specifies the FQDN of the cross-forest organization from which you are moving the mailbox.   | String   |
| Remote Legacy   | Specifies that this mailbox move is from a remote forest that does not have Exchange 2010 installed. <br>Default is True, when selected.   | True, False   |
| Remote Target Database   | Specifies the name of the target database in the remote forest. Use this property to move mailboxes from the local forest to a remote forest. For moves from a remote forest to the local forest, use the Target Database property.<br>When you use this property, you must also specify the Remote or Remote Legacy property.   | String   |
| Suspend   | Specifies whether to suspend the request. If you enable this property, the move request will be queued but will not reach the status of InProgress until the request is resumed.<br>Default is True, when selected.   | True, False   |
| Suspend Comment   | Specifies the reason for suspending the move request or other related comment. This property can only be used when the Suspend property is True.   | String   |
| Suspend When Ready To Complete   | Specifies whether to suspend the move request before it reaches the status of CompletionInProgress. After the move is suspended per this setting, it has a status of AutoSuspended. The move can then be manually completed with the Resume-MoveRequest command.<br>You can only use the Suspend When Ready To Complete property for online mailbox moves and when moving mailboxes from Exchange Server 2007 or Exchange 2010 mailbox databases. You cannot use this property for offline moves or when moving from Exchange Server 2003 mailbox databases. <br>Default is True, when selected.   | True, False   |
| Target Database   | Specifies the identity of the database to which the mailbox is being moved. If the target database is not specified, the command uses the automatic mailbox distribution logic to determine the target database. This can be one of the following value types:<br>GUID of the database<br>Database name   | String   |
| Target Delivery Domain   | Specifies the FQDN of the external email address that this move request creates in the source forest for the mail-enabled user. This property is allowed only to perform remote moves with the Remote or RemoteLegacy property.   | String   |

## Published data for the Create Move Request activity

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Alias   | The alias identifier of the mailbox or mail user.   | String   |
| Allow Large Items   | The Allow Large Items property.   | String   |
| Archive Domain   | The FQDN of the external domain to which the archive is being moved.   | String   |
| Archive GUID   | Globally unique identifier of the mailbox archive.   | String   |
| Bad Item Limit   | The specified allowable number of bad items to skip if the request encounters corrupted items in the mailbox.   | Number   |
| Bad Items Encountered   | The number of corrupted items encountered in the move.   | String   |
| Batch Name   | Descriptive name for moving a batch of mailboxes.   | String   |
| Bytes Transferred   | The number of bytes transferred.   | String   |
| Bytes Transferred Per Minute   | The rate of bytes transferred per minute.   | String   |
| Completed Request Age Limit   | Completed Request Age Limit.   | String   |
| Completion Timestamp   | Timestamp of when the move was completed.   | String   |
| Direction   | Indicates the move request direction. This can be one of the following values:<br>Push <br>Pull   | String   |
| Display Name   | Mailbox display name.   | String   |
| Distinguished Name   | Distinguished name for the mailbox.   | String   |
| Do Not Preserve Mailbox Signature   | Indicates that the move does not preserve the mailbox mapping signature.   | String   |
| Exchange Environment   | Indicates the type of Exchange environment where this activity will be executed. The default is On-Premises.   | String   |
| Exchange GUID   | Globally unique identifier of the Microsoft Exchange installation.   | String   |
| Exchange PowerShell Application   | Specifies the application name segment of the connection URI.   | String   |
| Exchange Server Host   | The connected host Exchange server.   | String   |
| Exchange Server Port   | The connected Exchange server port.   | String   |
| Exchange User Name   | Username used to log on to the Exchange server.   | String   |
| Failure Code   | Failure Code.   | String   |
| Failure Side   | This can be one of the following values:<br>None <br>Source <br>Target   | String   |
| Failure Timestamp   | Failure Timestamp.   | String   |
| Failure Type   | Failure Type.   |   |
| Final Sync Timestamp   | Timestamp for final sync.   | String   |
| Flags   | Request flags. This can be one of the following values:<br>CrossOrg <br>IntraOrg <br>MoveOnlyArchiveMailbox<br>MoveOnlyPrimaryMailbox <br>None <br>Offline <br>Protected <br>Pull <br>Push <br>RemoteLegacy <br>Suspend <br>SuspendWhenReadyToComplete   | String   |
| Identity   | Identity of the object.   | String   |
| Ignore Rule Limit Errors   | Specifies that the command does not move the user's rules to the target location Exchange server.   | String   |
| Initial Seeding Completed Timestamp   | Timestamp of when the move was completed.   | DateTime   |
| Internal Flags   | Move request internal flags.   | String   |
| Is Offline   | Indicates if this is an offline move request.   | String   |
| Is Valid   | Indicates whether the object was configured correctly.   | String   |
| Items Transferred   | The number of items transferred.   | Number   |
| Large Item Limit   | Large Item Limit.   | Number   |
| Large Items Encountered   | The number of large items encountered.   | Number   |
| Last Update Timestamp   | Timestamp of when the move request was last updated.   | DateTime   |
| MRS Server Name   | FQDN of the Client Access server on which the instance of the Microsoft Exchange Mailbox Replication service (MRS) runs.   | String   |
| Mailbox Identity   | The identity of the mailbox or mail user.   | String   |
| Message   | Message.   | String   |
| Needs To Suppress PII   | Needs to Suppress PII (Personally Identifiable Information).   | String   |
| Overall Duration   | Overall Duration.   | String   |
| Percent Complete   | Percent Complete.   | Number   |
| Position In Queue   | Position In Queue.   | String   |
| Priority   | Move request priority.   | String   |
| Protect   | Indicates if this mailbox is moved in protected mode.   | String   |
| Queued Timestamp   | Timestamp of when the move request was queued.   | DateTime   |
| Release Info   | Release Info.   | String   |
| Remote Archive Database GUID   | GUID for the Remote Archive Database.   | String   |
| Remote Archive Database Name   | Name of the target database in the remote forest. This applies when moving users with archives from the local forest to a remote forest.   | String   |
| Remote Credential User Name   | Administrator who has permission to perform the mailbox move.   | String   |
| Remote Database GUID   | GUID for the Remote Database.   | String   |
| Remote Database Name   | Name of the target database in the remote forest. This applies when moving mailboxes from the local forest to a remote forest.   | String   |
| Remote Global Catalog   | FQDN of the global catalog server for the remote forest.   | String   |
| Remote Host Name   | FQDN of the cross-forest organization from which the mailbox is being moved.   | String   |
| Report   | Report.   | String   |
| Request GUID   | Request GUID.   | String   |
| Request Queue   | Request Queue.   | String   |
| Request Style   | Indicates whether the move request is within the same organization or between different organizations. This can be one of the following values:<br>IntraOrg <br>CrossOrg   | String   |
| Skip CA Check   | Indicates whether the client validates that the server certificate is signed by a trusted certification authority (CA) for connections over Hypertext Transfer Protocol over Secure Socket Layer.   | String   |
| Skip CN Check   | Indicates whether the client validates that the certificate common name (CN) of the server matches the hostname of the server.   | String   |
| Skip Revocation Check   | Indicates whether the connection skips the validation of the revocation status of the server certificate.   | String   |
| Source Archive Database   | Mailbox database from which the mailbox archive is being moved.   | String   |
| Source Archive Server   | Server from which the mailbox archive is being moved.   | String   |
| Source Archive Version   | Version of Exchange installation on the source archive server.   | String   |
| Source Database   | Mailbox database from which the mailbox is being moved.   | String   |
| Source Server   | Server from which the mailbox is being moved.   | String   |
| Start Timestamp   | Timestamp of when the move was started.   | DateTime   |
| Source Version   | Version of Exchange installation from which the mailbox is being moved.   | String   |
| Status   | Request status. This can be one of the following values:<br>AutoSuspended <br>Completed <br>CompletedWithWarning <br>CompletionInProgress <br>Failed <br>InProgress <br>None <br>Queued <br>Suspended   | String   |
| Status Detail   | Request status details. This can be one of the following values:<br>AutoSuspended <br>Canceled <br>Cleanup <br>Completed <br>CompletedWithWarnings <br>Completion <br>CopyingMessages <br>CreatingFolderHierarchy<br>CreatingInitialSyncCheckpoint <br>CreatingMailbox <br>DataReplicationWait <br>Failed <br>FailedBadItemLimit <br>FailedMAPI <br>FailedNetwork <br>FailedOther <br>FailedStallDueToCI <br>FailedStallDueToHA <br>Finalization <br>IncrementalSync <br>InitializingMove <br>InitialSeeding <br>InProgress <br>LoadingMessages <br>MDBOffline <br>NetworkFailure <br>None <br>OverallMove <br>ProxyBackoff <br>Queued <br>Relinquished <br>Stalled <br>StalledDueToCI <br>StalledDueToHA <br>Suspended <br>TransientFailure | String   |
| Suspend   | Indicates if the request is suspended when queued.   | String   |
| Suspend When Ready To Complete   | Indicates if the request is suspended before it completes.   | String   |
| Suspended Timestamp   | Timestamp of when the move request was suspended.   | DateTime   |
| Sync Stage   | Sync stage. This can be one of the following values:<br>Cleanup <br>CopyingMessages <br>CreatingFolderHierarchy<br>CreatingInitialSyncCheckpoint <br>CreatingMailbox <br>Error <br>FinalIncrementalSync <br>IncrementalSync <br>LoadingMessages <br>MailboxCreated <br>None <br>SyncFinished   | String   |
| Target Archive Database   | Mailbox database to which the mailbox archive is being moved.   | String   |
| Target Archive Server   | Server to which the mailbox archive is being moved.   | String   |
| Target Archive Version   | Version of Exchange installation to which the mailbox archive is being moved.   | String   |
| Target Version   | Version of Exchange installation to which the mailbox is being moved.   | String   |
| Target Database   | Mailbox database to which the mailbox is being moved.   | String   |
| Target Delivery Domain   | FQDN of the external email address created by the move in the source forest for the mail-enabled user.   | String   |
| Target Server   | Server to which the mailbox is being moved.   | String   |
| Target Version   | Version of Exchange installation to which the mailbox is being moved.   | String   |
| Total Archive Item Count   | The number of items in the archive.   | Number   |
| Total Archive Size   | Total Archive Size.   | String   |
| Total Data Replication Wait Duration   | Total Data Replication Wait Duration.   | String   |
| Total Failed Duration   | Total Failed Duration.   | String   |
| Total Finalization Duration   | Total Finalization Duration.   | String   |
| Total In Progress Duration   | Total In Progress Duration.   | String   |
| Total Mailbox Item Count   | Total Mailbox Item Count.   | Number   |
| Total Proxy Backoff Duration   | Total Proxy Backoff Duration.   | String   |
| Total Queued Duration   | Total Queued Duration.   | String   |
| Total Stalled Due To CI Duration   | Total Stalled Due To CI Duration.   | String   |
| Total Stalled Due To HA Duration   | Total Stalled Due To HA Duration.   | String   |
| Total Stalled Due To Mailbox Locked Duration | Total Stalled Due To Mailbox Locked Duration.   | String   |
| Total Stalled Due To Read CPU   | Total Stalled Due To Read CPU.   | String   |
| Total Stalled Due To Read Throttle   | Total Stalled Due To Read Throttle.   | String   |
| Total Stalled Due To Read Unknown   | Total Stalled Due To Read Unknown.   | String   |
| Total Stalled Due To Write CPU   | Total Stalled Due To Write CPU.   | String   |
| Total Stalled Due To Write Throttle   | Total Stalled Due To Write Throttle.   | String   |
| Total Stalled Due To Write Unknown   | Total Stalled Due To Write Unknown.   | String   |
| Total Suspended Duration   | Total Suspended Duration.   | String   |
| Total Transient Failure Duration   | Total Transient Failure Duration.   | String   |
| Total Mailbox Size   | Total Mailbox Size.   | String   |
| Use SSL   | Indicates whether SSL encryption is used.   | String   |
| Validation Message   | Validation Message.   | String   |
| Workload Type   | Workload type.   | String   |

#### Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)

