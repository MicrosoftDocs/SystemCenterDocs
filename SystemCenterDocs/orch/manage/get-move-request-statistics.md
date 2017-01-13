---
title: Get Move Request Statistics
description: You can use the Get Move Request Statistics activity to retrieve statistical information about existing move requests for an on-premise environment.
ms.custom: na
ms.date: 12/02/2016
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 62e227c1-8233-4201-8bc1-cfbd4aa70f9e
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
robots: noindex
---
# Get Move Request Statistics

Applies To: System Center 2016 - Orchestrator

You can use the Get Move Request Statistics activity to retrieve statistical information about existing move requests for an on-premise environment.

The following tables list the optional properties, filters, and published data for this activity.

## Required properties for Get Move Request Statistics

This activity has no required properties.

## Filters for Get Move Request Statistics

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Mailbox Identity   | Identity of the mailbox or mail user.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Distinguished Name   | Distinguished name for the mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Display Name   | Mailbox display name.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Alias   | Mailbox or mail user alias.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with  |
| Exchange GUID   | Unique identifier of the Microsoft Exchange installation.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern <br>Starts with<br>Ends with |
| Archive GUID   | Mailbox archive identifier.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern <br>Starts with<br>Ends with |
| Status   | Specifies the request status. It can be one of the following:<br>AutoSuspended <br>Completed <br>CompletedWithWarning <br>CompletionInProgress <br>Failed <br>InProgress <br>None <br>Queued <br>Suspended   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern <br>Starts with<br>Ends with |
| Status Detail   | Specifies the request status details. It can be one of the following:<br>AutoSuspended <br>Canceled <br>Cleanup <br>Completed <br>CompletedWithWarnings <br>Completion <br>CopyingMessages <br>CreatingFolderHierarchy<br>CreatingInitialSyncCheckpoint <br>CreatingMailbox <br>DataReplicationWait <br>Failed <br>FailedBadItemLimit <br>FailedMAPI <br>FailedNetwork <br>FailedOther <br>FailedStallDueToCI <br>FailedStallDueToHA <br>Finalization <br>IncrementalSync <br>InitializingMove <br>InitialSeeding <br>InProgress <br>LoadingMessages <br>MDBOffline <br>NetworkFailure <br>None <br>OverallMove <br>ProxyBackoff <br>Queued <br>Relinquished <br>Stalled <br>StalledDueToCI <br>StalledDueToHA <br>Suspended <br>TransientFailure<br>ADUpdate<br>StalledDueToMailboxLock<br>StalledDueToReadThrottle<br>StalledDueToWriteThrottle<br>StalledDueToReadCpu<br>StalledDueToWriteCpu<br>StalledDueToReadUnknown<br>StalledDueToWriteUnknown | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br> Starts with<br>Ends with |
| Sync Stage   | Specifies the sync stage. It can be one of the following:<br>Cleanup <br>CopyingMessages <br>CreatingFolderHierarchy<br>CreatingInitialSyncCheckpoint <br>CreatingMailbox <br>Error <br>FinalIncrementalSync <br>IncrementalSync <br>LoadingMessages <br>MailboxCreated <br>None <br>SyncFinished   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br> Starts with<br>Ends with |
| Flags   | Specifies the request flags. It can be one of the following:<br>CrossOrg <br>IntraOrg <br>MoveOnlyArchiveMailbox<br>MoveOnlyPrimaryMailbox <br>None <br>Offline <br>Protected <br>Pull <br>Push <br>RemoteLegacy <br>Suspend <br>SuspendWhenReadyToComplete   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches<br>Does not match<br>Starts with<br>Ends with   |
| Request Style   | Indicates whether the move request is within the same organization or between different organizations. One of the move request can be one of the following:<br>IntraOrg <br>CorssOrg   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern <br>Starts with<br>Ends with |
| Direction   | Indicates the move request direction. It can be one of the following::<br>Push <br>Pull   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern <br>Starts with<br>Ends with |
| Is Offline   | Indicates if this is an offline move request.   | Equals<br>Does not equal   |
| Protect   | Indicates if this mailbox is moved in protected mode.   | Equals<br>Does not equal   |
| Workload Type   | Workload type.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br> Starts with<br>Ends with |
| Suspend   | Indicates if the request is suspended when queued.   | Equals<br>Does not equal   |
| Suspend When Ready To Complete   | Indicates if the request is suspended before it completes.   | Equals<br>Does not equal   |
| Ignore Rule Limit Errors   | Specifies that the command does not move the user's rules to the target server that runs Exchange.   | Equals<br>Does not equal   |
| Source Database   | Mailbox database where the mailbox is being moved from.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br> Starts with<br>Ends with |
| Source Server   | Server where the mailbox is being moved from.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br> Starts with<br>Ends with |
| Source Version   | Version of Exchange installation where the mailbox is being moved from.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br> Starts with<br>Ends with |
| Target Version   | Version of Exchange installation where the mailbox is being moved to.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern <br>Starts with<br>Ends with |
| Target Database   | Mailbox database where the mailbox is being moved to.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern <br>Starts with<br>Ends with |
| Target Server   | Server where the mailbox is being moved to.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern <br>Starts with<br>Ends with |
| Source Archive Database   | Mailbox database where the mailbox archive is being moved from.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern <br>Starts with<br>Ends with |
| Source Archive Version   | Version of Exchange installation where the mailbox archive is being moved from.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern <br>Starts with<br>Ends with |
| Source Archive Server   | Server where the mailbox archive is being moved from.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern <br>Starts with<br>Ends with |
| Target Archive Database   | Mailbox database where the mailbox archive is being moved to.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br> Starts with<br>Ends with |
| Target Archive Version   | Version of Exchange installation where the mailbox archive is being moved to.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br> Starts with<br>Ends with |
| Target Archive Server   | Server where the mailbox archive is being moved to.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern <br>Starts with<br>Ends with |
| Remote Host Name   | FQDN of the cross-forest organization from which the mailbox is being moved.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br> Starts with<br>Ends with |
| Remote Global Catalog   | FQDN of the global catalog server for the remote forest.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern <br>Starts with<br>Ends with |
| Batch Name   | Descriptive name for moving a batch of mailboxes.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br> Starts with<br>Ends with |
| Remote Credential User name   | Administrator who has permission to perform the mailbox move.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br> Starts with<br>Ends with |
| Remote Database Name   | Name of the target database in the remote forest when moving mailboxes from the local forest to a remote forest.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br> Starts with<br>Ends with |
| Remote Database GUID   | GUID for the Remote Database.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern <br>Starts with<br>Ends with |
| Remote Archive Database Name   | Name of the target database in the remote forest when moving users with archives from the local forest to a remote forest.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern <br>Starts with<br>Ends with |
| Remote Archive Database GUID   | GUID for the Remote Archive Database.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern <br>Starts with<br>Ends with |
| Target Delivery Domain   | FQDN of the external email address that is created in the source forest for the mail-enabled user when the move request is complete.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern <br>Starts with<br>Ends with |
| Archive Domain   | FQDN of the external domain to which the archive is being moved.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern <br>Starts with<br>Ends with |
| Bad Item Limit   | Number of bad items to skip if the request encounters corruption in the mailbox. The number can be "unlimited" or a positive integer.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Bad Items Encountered   | Number of bad items encountered in the move. The number can be "unlimited" or a positive integer.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Large Item Limit   | Large item limit. It can be "unlimited" or a positive integer.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Large Items Encountered   | Number of large items encountered. It can be "unlimited" or a positive integer.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Allow Large Items   | Allow Large Items   | Equals<br>Does not equal   |
| Queued Timestamp   | Timestamp when the move request was queued.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Start Timestamp   | Timestamp when the move was started.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Last Update Timestamp   | Timestamp when the move request was last updated.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Initial Seeding Completed Timestamp   | Timestamp when the initial seeding was completed.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Final Sync Timestamp   | Timestamp for final sync.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Completion Timestamp   | Timestamp when the move was completed.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Suspended Timestamp   | Timestamp when the move request was suspended.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Overall Duration   | Overall Duration. <br>Format: d.hh:mm:ss where d = days, h = hours, m = minutes, and s = seconds.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Total Finalization Duration   | Total Finalization duration.<br>Format: d.hh:mm:ss where d = days, h = hours, m = minutes, and s = seconds.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Total Data Replication Wait Duration   | Total wait duration for data replication. <br>Format: d.hh:mm:ss where d = days, h = hours, m = minutes, and s = seconds.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Total Suspended Duration   | Total Suspended duration.<br>Format: d.hh:mm:ss where d = days, h = hours, m = minutes, and s = seconds.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Total Failed Duration   | Total Failed duration.<br>Format: d.hh:mm:ss where d = days, h = hours, m = minutes, and s = seconds.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Total Queued Duration   | Total Queued duration.<br>Format: d.hh:mm:ss where d = days, h = hours, m = minutes, and s = seconds.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Total In Progress Duration   | Total In Progress duration.<br>Format: d.hh:mm:ss where d = days, h = hours, m = minutes, and s = seconds.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Total Stalled Due To CI Duration   | Total Stalled Due To CI duration.<br>Format: d.hh:mm:ss where d = days, h = hours, m = minutes, and s = seconds.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Total Stalled Due To HA Duration   | Total Stalled Due To HA duration<br>Format: d.hh:mm:ss where d = days, h = hours, m = minutes, and s = seconds.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Total Stalled Due To Mailbox Locked Duration | Total Stalled Due To Mailbox Locked duration.<br>Format: d.hh:mm:ss where d = days, h = hours, m = minutes, and s = seconds.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Total Stalled Due To Read Throttle   | Total duration for Stalled Due To Read Throttle.<br>Format: d.hh:mm:ss where d = days, h = hours, m = minutes, and s = seconds.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Total Stalled Due To Write Throttle   | Total duration for Stalled Due To Write Throttle.<br>Format: d.hh:mm:ss where d = days, h = hours, m = minutes, and s = seconds.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Total Stalled Due To Read CPU   | Total duration for Stalled Due To Read CPU.<br>Format: d.hh:mm:ss where d = days, h = hours, m = minutes, and s = seconds.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Total Stalled Due To Write CPU   | Total duration for Stalled Due To Write CPU.<br>Format: d.hh:mm:ss where d = days, h = hours, m = minutes, and s = seconds.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Total Stalled Due To Read Unknown   | Total duration for Stalled Due To Read Unknown.<br>Format: d.hh:mm:ss where d = days, h = hours, m = minutes, and s = seconds.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Total Stalled Due To Write Unknown   | Total duration for Stalled Due To Write Unknown.<br>Format: d.hh:mm:ss where d = days, h = hours, m = minutes, and s = seconds.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Total Transient Failure Duration   | Total Transient Failure duration.<br>Format: d.hh:mm:ss where d = days, h = hours, m = minutes, and s = seconds.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Total Proxy Backoff Duration   | Total Proxy Backoff duration.<br>Format: d.hh:mm:ss where d = days, h = hours, m = minutes, and s = seconds.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| MRS Server Name   | FQDN of the Client Access server on which the instance of the Microsoft Exchange Mailbox Replication service (MRS) is running.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern <br>Starts with<br>Ends with |
| Total Mailbox Size   | Total mailbox size.<br>It can be either "unlimited" or a string with <br>format &lt;integer&gt; &lt;unit&gt;, where unit can be one of: KB, MB, GB, TB. The default unit value is Byte, when it is not specified.<br>For example, 55 GB, unlimited, 77, 14 KB   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Total Mailbox Item Count   | Total mailbox item count.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Total Archive Size   | Total archive size.<br>It can be either "unlimited" or a string with <br>format &lt;integer&gt; &lt;unit&gt;, where unit can be one of: KB, MB, GB, TB. The default unit value is Byte, when unit is not specified.<br>For example, 55 GB, unlimited, 77, 14 KB.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Total Archive Item Count   | Total archive item count.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Bytes Transferred   | Total transferred bytes. <br>It can be either "unlimited" or a string with <br>format &lt;integer&gt; &lt;unit&gt;, where unit can be one of: KB, MB, GB, TB. The default value is Byte, when unit is not specified.<br>For example, 55 GB, unlimited, 77, 14 KB.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Bytes Transferred Per Minute   | Total bytes transferred per minute.<br>The total can be either "unlimited" or a string with <br>format &lt;integer&gt; &lt;unit&gt;, where unit can be one of: KB, MB, GB, TB. The default is Byte, when unit is not specified.<br>For example, 55 GB, unlimited, 77, 14 KB.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Items Transferred   | Items transferred.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Percent Complete   | Percent complete.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Completed Request Age Limit   | Age limit of a completed request. <br>Format: d.hh:mm:ss where d = days, h = hours, m = minutes, and s = seconds.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Position In Queue   | Position in Queue.   | Equals<br>Does not equal<br>Contains<br>Does not cotain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with   |
| Failure Code   | Failure code.   | Equals<br>Does not equal<br>Contains<br>Does not cotain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with   |
| Failure Type   | Failure type.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br> Starts with<br>Ends with |
| Failure Side   | Failure side.<br>Can be one of:<br>None <br>Source <br>Target   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern <br>Starts with<br>Ends with |
| Message   | Message   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern <br>Starts with<br>Ends with |
| Failure Timestamp   | Failure timestamp.   | Equals<br>Does not equal<br>Is less than<br>Is greater than<br>Is less than or equal to<br>Is greater than or equal to   |
| Is Valid   | Indicates whether the object was configured correctly.   | Equals<br>Does not equal   |
| Validation Message   | Validation message.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern <br>Starts with<br>Ends with |
| Request GUID   | Request GUID.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br> Starts with<br>Ends with |
| Request Queue   | Request Queue.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern <br>Starts with<br>Ends with |
| Identity   | Identity of the object.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern <br>Starts with<br>Ends with |
| Report   | String   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern <br>Starts with<br>Ends with |
| Needs To Suppress PII   | Needs to suppress PII (Personally Identifiable Information).   | Equals<br>Does not equal   |
| Do Not Preserve Mailbox Signature   | Indicates that the move does not preserve the mailbox mapping signature.   | Equals<br>Does not equal   |
| Internal Flags   | Internal flags.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern <br>Starts with<br>Ends with |
| Priority   | Request priority.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br> Starts with<br>Ends with |
| Release Info   | Release info.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches pattern<br>Does not match pattern<br> Starts with<br>Ends with |

### Optional properties for Get Move Request Statistics

| Element   | Description   | Valid values |
|:---|:---|:---|
| Domain Controller  | Specifies the fully qualified domain name (FQDN) of the domain controller that retrieves data from Active Directory.   | String   |
| Identity   | Specifies the identity of the mailbox or mail user. Can be one of the following value types:<br>GUID<br>Distinguished name (DN)<br>Domain\\Account <br>User principal name (UPN)<br>Legacy Exchange DN<br>SMTP address<br>Alias<br>This property cannot be used in conjunction with the Move Request Queue, MRS Instance, or Mailbox GUID properties. | String   |
| Include Report   | Specifies whether to return additional details about the request, which can be used for troubleshooting.   | True, False  |
| Mailbox GUID   | Specifies the GUID of a mailbox for which you want to view the move request statistics.<br>This property cannot be used in conjunction with the Identity property.   | String   |
| Move Request Queue | Specifies the mailbox database on which the move request resides. You can use one of the following values:<br>GUID of the database<br>Database name<br>This property cannot be used in conjunction with the Identity or MRS Instance properties.   | String   |

### Published data for Get Move Request Statistics

| Element   | Description   | Valid values |
|:---|:---|:---|
| Alias   | Mailbox or mail user alias.   | String   |
| Allow Large Items   | Allow large items.   | String   |
| Archive Domain   | FQDN of the external domain to which the archive is being moved.   | String   |
| Archive GUID   | Mailbox archive identifier.   | String   |
| Bad Item Limit   | Number of bad items to skip if the request encounters corruption in the mailbox.   | Number   |
| Bad Items Encountered   | Number of bad items encountered in the move.   | String   |
| Batch Name   | Descriptive Name for moving a batch of mailboxes.   | String   |
| Bytes Transferred   | Total transferred Bytes.   | String   |
| Bytes Transferred Per Minute   | Bytes transferred per minute.   | String   |
| Completed Request Age Limit   | Age limit for a completed request.   | String   |
| Completion Timestamp   | Timestamp when the move was completed.   | String   |
| Direction   | Indicates the move request direction. Can be one of the following:<br>Push <br>Pull   | String   |
| Display Name   | Mailbox display name.   | String   |
| Distinguished Name   | Distinguished name for the mailbox.   | String   |
| Do Not Preserve Mailbox Signature   | Indicates that the move does not preserve the mailbox mapping signature.   | String   |
| Exchange Environment   | Indicates the type of Exchange environment where this activity will be executed. Default is On-Premise.   | String   |
| Exchange GUID   | Unique identifier of the Microsoft Exchange installation.   | String   |
| Exchange PowerShell Application   | Specifies the application name segment of the connection URI.   | String   |
| Exchange Server Host   | Exchange Server connected.   | String   |
| Exchange Server Port   | Exchange Server port connected.   | String   |
| Exchange User Name   | Username used to connect to Exchange Server.   | String   |
| Failure Code   | Failure code.   | String   |
| Failure Side   | Failure side.<br>Can be one of:<br>None <br>Source <br>Target   | String   |
| Failure Timestamp   | Failure timestamp.   | String   |
| Failure Type   | Failure Type.   |   |
| Final Sync Timestamp   | Timestamp for final sync.   | String   |
| Flags   | Request flags. Can be one of:<br>CrossOrg <br>IntraOrg <br>MoveOnlyArchiveMailbox<br>MoveOnlyPrimaryMailbox <br>None <br>Offline <br>Protected <br>Pull <br>Push <br>RemoteLegacy <br>Suspend <br>SuspendWhenReadyToComplete   | String   |
| Identity   | Identity of the object.   | String   |
| Ignore Rule Limit Errors   | Specifies that the command does not move the user's rules to the target server running Exchange.   | String   |
| Initial Seeding Completed Timestamp   | Timestamp when the move was completed.   | DateTime   |
| Internal Flags   | Move request internal flags.   | String   |
| Is Offline   | Indicates if this is an offline move request.   | String   |
| Is Valid   | Indicates whether the object was configured correctly.   | String   |
| Items Transferred   | Transferred items.   | Number   |
| Large Item Limit   | Large item limit.   | Number   |
| Large Items Encountered   | Large items encountered.   | Number   |
| Last Update Timestamp   | Timestamp when the move request was last updated.   | DateTime   |
| MRS Server Name   | FQDN of the Client Access server on which the instance of the Microsoft Exchange Mailbox Replication service (MRS) is running.   | String   |
| Mailbox Identity   | Identity of the mailbox or mail user.   | String   |
| Message   | Message   | String   |
| Move Request Count   | Number of move requests found.   | Number   |
| Move Request Queue   | Name of the move request queue.   | String   |
| MRS Instance   | The name of the instance of the Microsoft Exchange Mailbox Replication service (MRS).   | String   |
| Needs To Suppress PII   | Needs to suppress PII (Personally Identifiable Information).   | String   |
| Overall Duration   | Overall duration.   | String   |
| Percent Complete   | Percent complete.   | Number   |
| Position In Queue   | Position in Queue.   | String   |
| Priority   | Move request priority.   | String   |
| Protect   | Indicates if this mailbox is moved in protected mode.   | String   |
| Queued Timestamp   | Timestamp when the move request was queued.   | DateTime   |
| Release Info   | Release info.   | String   |
| Remote Archive Database GUID   | GUID for the Remote Archive Database.   | String   |
| Remote Archive Database Name   | Name of the target database in the remote forest when moving users with archives from the local forest to a remote forest.   | String   |
| Remote Credential User Name   | Administrator who has permission to perform the mailbox move.   | String   |
| Remote Database GUID   | GUID for the Remote Database.   | String   |
| Remote Database Name   | Name of the target database in the remote forest when moving mailboxes from the local forest to a remote forest.   | String   |
| Remote Global Catalog   | FQDN of the global catalog server for the remote forest.   | String   |
| Remote Host Name   | FQDN of the cross-forest organization from which the mailbox is being moved.   | String   |
| Report   | Report   | String   |
| Request GUID   | Request GUID.   | String   |
| Request Queue   | Request queue.   | String   |
| Request Style   | Indicates whether the move request is within the same organization or between different organizations. Can be one of the following:<br>IntraOrg <br>CorssOrg   | String   |
| Skip CA Check   | Indicates whether the client validates that the server certificate is signed by a trusted certification authority (CA) when connecting over Hypertext Transfer Protocol over Secure Socket Layer.   | String   |
| Skip CN Check   | Indicates whether the client validates that the certificate common name (CN) of the server matches the hostname of the server.   | String   |
| Skip Revocation Check   | Indicates whether the connection does not validate the revocation status of the server certificate.   | String   |
| Source Archive Database   | Mailbox database where the mailbox archive is being moved from.   | String   |
| Source Archive Server   | Server where the mailbox archive is being moved from.   | String   |
| Source Archive Version   | Version of Exchange installation where the mailbox archive is being moved from.   | String   |
| Source Database   | Mailbox database where the mailbox is being moved from.   | String   |
| Source Server   | Server where the mailbox is being moved from.   | String   |
| Start Timestamp   | Timestamp when the move was started.   | DateTime   |
| Source Version   | Version of Exchange installation where the mailbox is being moved from.   | String   |
| Status   | Request status. Can be one of the following:<br>AutoSuspended <br>Completed <br>CompletedWithWarning <br>CompletionInProgress <br>Failed <br>InProgress <br>None <br>Queued <br>Suspended   | String   |
| Status Detail   | Request status details. Can be one of:<br>AutoSuspended <br>Canceled <br>Cleanup <br>Completed <br>CompletedWithWarnings <br>Completion <br>CopyingMessages <br>CreatingFolderHierarchy<br>CreatingInitialSyncCheckpoint <br>CreatingMailbox <br>DataReplicationWait <br>Failed <br>FailedBadItemLimit <br>FailedMAPI <br>FailedNetwork <br>FailedOther <br>FailedStallDueToCI <br>FailedStallDueToHA <br>Finalization <br>IncrementalSync <br>InitializingMove <br>InitialSeeding <br>InProgress <br>LoadingMessages <br>MDBOffline <br>NetworkFailure <br>None <br>OverallMove <br>ProxyBackoff <br>Queued <br>Relinquished <br>Stalled <br>StalledDueToCI <br>StalledDueToHA <br>Suspended <br>TransientFailure | String   |
| Suspend   | Indicates if the request is suspended when queued.   | String   |
| Suspend When Ready To Complete   | Indicates if the request is suspended before it completes.   | String   |
| Suspended Timestamp   | Timestamp when the move request was suspended.   | DateTime   |
| Sync Stage   | Specifies the sync stage. Can be one of the following:<br>Cleanup <br>CopyingMessages <br>CreatingFolderHierarchy<br>CreatingInitialSyncCheckpoint <br>CreatingMailbox <br>Error <br>FinalIncrementalSync <br>IncrementalSync <br>LoadingMessages <br>MailboxCreated <br>None <br>SyncFinished   | String   |
| Target Archive Database   | Mailbox database where the mailbox archive is being moved to.   | String   |
| Target Archive Server   | Server where the mailbox archive is being moved to.   | String   |
| Target Archive Version   | Version of Exchange installation where the mailbox archive is being moved to.   | String   |
| Target Version   | Version of Exchange installation where the mailbox is being moved to.   | String   |
| Target Database   | Mailbox database where the mailbox is being moved to.   | String   |
| Target Delivery Domain   | FQDN of the external email address created in the source forest for the mail-enabled user when the move request is complete.   | String   |
| Target Server   | Server where the mailbox is being moved to.   | String   |
| Target Version   | Version of Exchange installation where the mailbox is being moved to.   | String   |
| Total Archive Item Count   | Total item count for Archive.   | Number   |
| Total Archive Size   | Total archive size.   | String   |
| Total Data Replication Wait Duration   | Total wait duration for data replication.   | String   |
| Total Failed Duration   | Total Failed duration.   | String   |
| Total Finalization Duration   | Total Finalization duration.   | String   |
| Total In Progress Duration   | Total In Progress duration.   | String   |
| Total Mailbox Item Count   | Total mailbox item count.   | Number   |
| Total Proxy Backoff Duration   | Total Proxy Backoff duration.   | String   |
| Total Queued Duration   | Total Queued duration.   | String   |
| Total Stalled Due To CI Duration   | Total Stalled Due To CI duration.   | String   |
| Total Stalled Due To HA Duration   | Total Stalled Due To HA duration.   | String   |
| Total Stalled Due To Mailbox Locked Duration | Total Stalled Due To Mailbox Locked duration.   | String   |
| Total Stalled Due To Read CPU   | Total Stalled Due To Read CPU.   | String   |
| Total Stalled Due To Read Throttle   | Total Stalled Due To Read Throttle.   | String   |
| Total Stalled Due To Read Unknown   | Total Stalled Due To Read Unknown.   | String   |
| Total Stalled Due To Write CPU   | Total Stalled Due To Write CPU.   | String   |
| Total Stalled Due To Write Throttle   | Total Stalled Due To Write Throttle.   | String   |
| Total Stalled Due To Write Unknown   | Total Stalled Due To Write Unknown.   | String   |
| Total Suspended Duration   | Total Suspended duration.   | String   |
| Total Transient Failure Duration   | Total Transient Failure duration.   | String   |
| Total Mailbox Size   | Total mailbox size.   | String   |
| Use SSL   | Indicates whether SSL encryption is used.   | String   |
| Validation Message   | Validation message.   | String   |
| Workload Type   | Workload type.   | String   |

#### Other Resources

[Using Runbooks in System Center 2016 - Orchestrator](https://technet.microsoft.com/en-us/library/hh403791.aspx)

