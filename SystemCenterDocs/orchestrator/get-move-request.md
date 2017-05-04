---
title: Get Move Request
description: You can use the Get Move Request activity in a runbook to retrieve detailed information for an existing mailbox move request, for an on-premise environment.
ms.custom: na
ms.date: 4/25/2017
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 3b3e9322-cff6-4b32-af10-6b7fa0f22a65
author: cfreemanwa
ms.author: cfreeman
manager: carmonm
---

# Get Move Request

Applies To: System Center 2016 - Orchestrator

You can use the Get Move Request activity in a runbook to retrieve detailed information for an existing mailbox move request, for an on-premise environment.

The following tables list the filters, optional properties, and published data for this activity.

## Required properties for Get Move Request activity

This Activity has no required properties.

## Filters for Get Move Request activity

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Alias   | Mailbox or mail user alias.   | Equals<br>Does not equal<br>Contains<br>Does not cotain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with   |
| Batch Name   | Descriptive name for moving a batch of mailboxes.   | Equals<br>Does not equal<br>Contains<br>Does not cotain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with   |
| Direction   | Indicates the direction for the move request. It can be one of the following:<br>Push <br>Pull   | Equals<br>Does not equal<br>Contains<br>Does not cotain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with   |
| Display Name   | Mailbox display name.   | Equals<br>Does not equal<br>Contains<br>Does not cotain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with   |
| Distinguished Name   | Distinguished name for the mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not cotain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with   |
| Exchange GUID   | Unique identifier of the Microsoft Exchange installation.   | Equals<br>Does not equal<br>Contains<br>Does not cotain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with   |
| Exchange Version   | Version of Microsoft Exchange that this object is associated with.   | Equals<br>Does not equal<br>Contains<br>Does not cotain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with   |
| Extension Custom Attribute 1   | Custom attribute.   | Equals<br>Does not equal<br>Contains<br>Does not cotain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with   |
| Extension Custom Attribute 2   | Custom attribute.   | Equals<br>Does not equal<br>Contains<br>Does not cotain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with   |
| Extension Custom Attribute 3   | Custom attribute.   | Equals<br>Does not equal<br>Contains<br>Does not cotain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with   |
| Extension Custom Attribute 4   | Custom attribute.   | Equals<br>Does not equal<br>Contains<br>Does not cotain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with   |
| Extension Custom Attribute 5   | Custom attribute.   | Equals<br>Does not equal<br>Contains<br>Does not cotain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with   |
| External Directory Object Id   | External directory object ID.   | Equals<br>Does not equal<br>Contains<br>Does not contain<br>Matches <br>Does not match<br>Starts with<br>Ends with   |
| Flags   | Request flags. It can be one of the following:<br>CrossOrg <br>IntraOrg <br>MoveOnlyArchiveMailbox<br>MoveOnlyPrimaryMailbox <br>None <br>Offline <br>Protected <br>Pull <br>Push <br>RemoteLegacy <br>Suspend <br>SuspendWhenReadyToComplete<br>HighPriority   | Equals<br>Does not equal<br>Contains<br>Does not cotain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with   |
| GUID   | Mailbox GUID.   | Equals<br>Does not equal<br>Contains<br>Does not cotain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with   |
| Identity   | Identity of the mailbox or mail user.   | Equals<br>Does not equal<br>Contains<br>Does not cotain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with   |
| Is Offline   | Indicates if this is an offline move request.   | Equals<br>Does not equal   |
| Is Valid   | Indicates whether the object was configured correctly.   | Equals<br>Does not equal   |
| Last Exchange Changed Time   | Last Exchange Changed Time   | Equals<br>Does not equal<br>Is less than or equal to<br>Is greater than or equal to<br>Is less than<br>Is greater than   |
| Name   | Mailbox name.   | Equals<br>Does not equal<br>Contains<br>Does not cotain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with   |
| Needs To Suppress PII   | Needs to suppress the Personally Identifiable Information (PII).   | Equals<br>Does not equal   |
| Organization ID   | Organization for this mailbox.   | Equals<br>Does not equal<br>Contains<br>Does not cotain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with   |
| Originating Server   | Originates the server.   | Equals<br>Does not equal<br>Contains<br>Does not cotain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends withpattern |
| Protect   | Indicates if this mailbox is moved in protected mode.   | Equals<br>Does not equal   |
| Recipient Type   | Recipient type. It can be one of the following:<br>Computer <br>Contact <br>DynamicDistributionGroup <br>Group <br>Invalid <br>MailContact <br>MailNonUniversalGroup <br>MailUniversalDistributionGroup <br>MailUniversalSecurityGroup <br>MailUser <br>MicrosoftExchange <br>PublicDatabase <br>PublicFolder <br>SystemAttendantMailbox <br>SystemMailbox <br>User<br>UserMailbox   | Equals<br>Does not equal<br>Contains<br>Does not cotain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with   |
| Recipient Type Details   | Recipient type details. It can be one of the following:<br>AllUniqueRecipientTypes <br>ArbitrationMailbox <br>Computer <br>Contact <br>DisabledUser <br>DiscoveryMailbox <br>DynamicDistributionGroup <br>EquipmentMailbox <br>LegacyMailbox <br>LinkedMailbox <br>LinkedUser <br>MailboxPlan <br>MailContact <br>MailForestContact <br>MailNonUniversalGroup <br>MailUniversalDistributionGroup <br>MailUniversalSecurityGroup <br>MailUser <br>MicrosoftExchange <br>None <br>NonUniversalGroup <br>PublicFolder <br>RemoteEquipmentMailbox <br>RemoteRoomMailbox <br>RemoteSharedMailbox <br>RemoteUserMailbox <br>RoleGroup <br>RoomList <br>RoomMailbox <br>SharedMailbox <br>SystemAttendantMailbox <br>SystemMailbox <br>UniversalDistributionGroup <br>UniversalSecurityGroup <br>User <br>UserMailbox | Equals<br>Does not equal<br>Contains<br>Does not cotain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with   |
| Remote Host Name   | The fully qualified domain name (FQDN) of the cross-forest organization from which the mailbox is moved.   | Equals<br>Does not equal<br>Contains<br>Does not cotain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with   |
| Request Style   | Indicates whether the "move" request is within the same organization or between different organizations. It can be one of the following:<br>IntraOrg <br>CorssOrg   | Equals<br>Does not equal<br>Contains<br>Does not cotain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with   |
| Source Archive Database   | Mailbox database where the mailbox archive is being moved from.   | Equals<br>Does not equal<br>Contains<br>Does not cotain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with   |
| Source Database   | Mailbox database where the mailbox is being moved from.   | Equals<br>Does not equal<br>Contains<br>Does not cotain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with   |
| Status   | Request status. It can be one of the following:<br>AutoSuspended <br>Completed <br>CompletedWithWarning <br>CompletionInProgress <br>Failed <br>InProgress <br>None <br>Queued<br>Suspended   | Equals<br>Does not equal<br>Contains<br>Does not cotain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with   |
| Suspend   | Indicates if the request is suspended when queued.   | Equals<br>Does not equal   |
| Suspend When Ready To Complete | Indicates if the request is suspended before it completes.   | Equals<br>Does not equal   |
| Target Archive Database   | Mailbox database, where the mailbox archive is being moved to.   | Equals<br>Does not equal<br>Contains<br>Does not cotain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with   |
| Target Database   | Mailbox database, where the mailbox is being moved to.   | Equals<br>Does not equal<br>Contains<br>Does not cotain<br>Matches pattern<br>Does not match pattern<br>Starts with<br>Ends with   |

## Optional properties for Get Move Request activity

| **Element**   | **Description**   | **Valid values**   |
|:---|:---|:---|
| Batch Name   | Descriptive name that is necessary for moving a batch of mailboxes.   | String   |
| Domain Controller   | The fully FQDN of the domain controller that writes this configuration change to the Active Directory.   | String   |
| Identity   | Mailbox identity.   | String   |
| Offline   | Indicates if this is an offline move request. The default value is True, when selected.   | True, False   |
| Move Status   | Specifies to return "move" requests with the specified configured status.<br>Cannot be used in conjunction with Identity property. The Value range is one of the following:<br>Auto Suspended <br>Completed <br>Completed With Warning <br>Completion In Progress <br>Failed <br>In Progress <br>None <br>Queued <br>Suspended <br>Default is blank, when selected. | AutoSuspended<br>Completed CompletedWithWaring<br>CompletionInProgress<br>Failed<br>InProgress<br>None<br>Queued<br>Suspended |
| Multi Tenant   | Specifies that the search should be performed across the entire forest, not just across the organization that's currently scoped. The default value is True, when selected   | True, False   |
| Organization   | Specifies the organization in which the search will be performed. This filter is available for multi-tenant deployments. It is not available for on-premises deployments.   | String   |
| Organizational Unit   | Specifies an organizational unit (OU) and is used to limit the results.   | String   |
| Password   | Specifies the password used by the mail user to secure the user account and the associated mailbox in the service.   | String   |
| Protect   | Returns the moved mailboxes in protected mode. <br>Cannot be used in conjunction with the Identity property. The default value is True, when selected.   | True, False   |
| Remote Host Name   | Specifies the FQDN of the cross-forest organization from which the mailbox is moved. <br>Cannot be used in conjunction with the Identity property.   | String   |
| Result Size   | Specifies the maximum number of results to return. If you want to return all requests that match the query, use 'unlimited' for the value of this property. The default value is 1000.   | String   |
| Source Database   | Mailbox database where the mailbox is being moved from.   | String   |
| Suspend   | Indicates if the request is suspended when queued. The default value is True, when selected.   | True, Flase   |
| Suspend When Ready to Complete | Indicates if the request is suspended before it completes. The default is True, when selected.   | True, False   |
| Target Database   | Mailbox database where the mailbox is being moved to.   | String   |
| User Name   | Specifies the user name to use to access the on-premises Active Directory.   | String   |

## Published data for Get Move Request activity

| **Element**   | **Description**   | **Value type** |
|:---|:---|:---|
| Alias   | Mailbox or mail user alias.   | String   |
| Batch Name   | Descriptive name for moving a batch of mailboxes.   | String   |
| Direction   | The move request direction.   | String   |
| Display Name   | Mailbox display name.   | String   |
| Distinguished Name   | Distinguished name for the mailbox.   | String   |
| Exchange Environment   | Indicates the type of Exchange environment where this activity will be executed.   | String   |
| Exchange GUID   | Unique identifier of the Microsoft Exchange installation.   | String   |
| Exchange PowerShell Application | Specifies the name segment of the connection URI for the application.   | String   |
| Exchange Server Host   | Exchange Server connected.   | String   |
| Exchange Server Port   | Exchange Server port connected.   | String   |
| Exchange User Name   | Username that is used to connect to Exchange Server.   | String   |
| Exchange Version   | Version of Microsoft Exchange that this object is associated with.   | String   |
| Extension Custom Attribute 1   | Custom attribute.   | String   |
| Extension Custom Attribute 2   | Custom attribute.   | String   |
| Extension Custom Attribute 3   | Custom attribute.   | String   |
| Extension Custom Attribute 4   | Custom attribute.   | String   |
| Extension Custom Attribute 5   | Custom attribute.   | String   |
| External Directory Object Id   | External Directory Object ID.   | String   |
| Flags   | Request flags. It can be one of the following:<br>CrossOrg <br>IntraOrg <br>MoveOnlyArchiveMailbox MoveOnlyPrimaryMailbox <br>None <br>Offline <br>Protected <br>Pull <br>Push <br>RemoteLegacy <br>Suspend <br>SuspendWhenReadyToComplete | String   |
| GUID   | Mailbox GUID.   | String   |
| Identity   | Identity of the mailbox or mail user.   | String   |
| Is Offline   | Indicates if this is an offline "move" request.   | String   |
| Is Valid   | Indicates whether the object was configured correctly.   | String   |
| Last Exchange Changed Time   | Last Exchange Changed Time   | DateTime   |
| Move Request Count   | Number of move requests found.   | Number   |
| Name   | Mailbox name.   | String   |
| Needs To Suppress PII   | Needs to suppress the PII.   | String   |
| Organization ID   | Organization for this mailbox.   | String   |
| Originating Server   | Organization server.   | String   |
| Protect   | Indicates if this mailbox is moved in protected mode.   | String   |
| Recipient Type   | Recipient type.   | String   |
| Recipient Type Details   | Recipient type details.   | String   |
| Remote Host Name   | FQDN of the cross-forest organization from which the mailbox is moved.   | String   |
| Request Style   | Indicates whether the move request is within the same organization or between different organizations.   | String   |
| Skip CA Check   | Indicates whether the client does not validate that the server certificate is signed by a trusted certification authority (CA), when connecting through HTTPS. It is used when the Use SSL value is True.   | String   |
| Skip CN Check   | Indicates whether the certificate common name (CN) of the server and the configured hostname of the server are not checked for being the same. It is used when the Use SSL value is True.   | String   |
| Skip Revocation Check   | Indicates whether the revocation status of the server certificate is to be checked or not.   | String   |
| Source Archive Database   | Mailbox database from which the mailbox archive is moved.   | String   |
| Source Database   | Mailbox database from which the mailbox is moved.   | String   |
| Status   | Request status. It can be one of the following:<br>AutoSuspended <br>Completed <br>CompletedWithWarning <br>CompletionInProgress <br>Failed <br>InProgress <br>None <br>Queued<br>Suspended   | String   |
| Suspend   | Indicates if the request is suspended when queued.   | String   |
| Suspend When Ready To Complete  | Indicates if the request is suspended before it completes.   | String   |
| Target Archive Database   | Mailbox database where the mailbox archive is being moved to.   | String   |
| Target Database   | Mailbox database where the mailbox is being moved to.   | String   |
| Use SSL   | Indicates whether the communication with the Exchange Server is to be encrypted with SSL.   | String   |


