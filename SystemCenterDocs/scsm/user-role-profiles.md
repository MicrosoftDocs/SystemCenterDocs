---
title:  User role profiles in Service Manager
description: Learn about the scope and properties of user role profiles in Service Manager.
manager: carmonm
ms.topic: reference
author: bandersmsft
ms.author: banders
ms.prod:  system-center-2016
keywords:  
ms.date: 11/28/2016
ms.technology:  service-manager
ms.assetid:  38118405-3578-4e36-b5ec-e1cc5326e161
---

# User role profiles in System Center 2016 - Service Manager

This article provides detailed information about the scope and properties of user role profiles in Service Manager.

## Tabs in the Administrator console

The table below shows the tabs and order that they appear in the console.

| User roles | Tab order in Console |
| --- | --- |
| activity implementer | 1. Work Items <br> 2. Configurations |
| advanced operator | 1. Library <br> 2. Work Items <br> 3. Configurations |
| author | 1. Library <br> 2. Work Items <br> 3. Configurations |
| change initiator | 1. Work Items <br> 2. Configurations |
| change manager | 1. Work Items <br> 2. Configurations |
| incident resolver | 1. Work Items <br> 2. Configurations |
| problem analysts | 1. Work Items <br> 2. Configurations |
| Read Only operator | 1. Work Items <br> 2. Configurations |
| Release Manager | 1. Work Items <br> 2. Configurations |
| Service Request Analyst | 1. Work Items <br> 2. Configurations |
| Workflow | 1. Work Items <br> 2. Configurations |

## Default user roles

| action | allowed roles |
| --- | --- |
| read knowledge articles | activity implementer, advanced operator, author, change initiator, change manager, end user, incident resolver, problem analyst, read only operator, release manager, service request analyst, workflow |
| edit knowledge articles | advanced operator, author |
| create knowledge articles | advanced operator, author |
| delete knowledge article | advanced operator, author |
| create change requests and activities | activity implementer, advanced operator, author, change initiator, change manager, incident resolver, problem analyst, read only operator, release manager, service request analyst, workflow |
| create incident and activities | activity implementer, advanced operator, author, change initiator, change manager, incident resolver, problem analyst, read only operator, release manager, service request analyst, workflow |
| create problem records | activity implementer, advanced operator, author, change initiator, change manager, incident resolver, problem analyst, read only operator, release manager, service request analyst, workflow |
| create release records | activity implementer, advanced operator, author, change initiator, change manager, incident resolver, problem analyst, read only operator, release manager, service request analyst, workflow |
| create service requests and activities | activity implementer, advanced operator, author, change initiator, change manager, incident resolver, problem analyst, read only operator, release manager, service request analyst, workflow |
| edit change requests | advanced operator, author, change manager, workflow |
| edit incidents | advanced operator, author, incident resolver, workflow |
| edit problem records | advanced operator, author, problem analyst, workflow |
| edit release records | advanced operator, author, release manager, workflow |
| edit service requests | advanced operator, author, service request analyst, workflow |
| update status for change requests | advanced operator, author, change manager, workflow |
| update status for incidents | advanced operator, author, incident resolver, workflow |
| update status for problem records | advanced operator, author, problem analyst, workflow |
| update status for release records | advanced operator, author, release manager, workflow |
| update status for service requests | advanced operator, author, service request analyst, workflow |
| update status for manual activity | advanced operator, author, change manager, incident resolver, release manager, service request analyst, workflow |
| update status for review activity | advanced operator, author, change manager, release manager, service request analyst, workflow |
| create CIs | advanced operator, author, workflow |
| update CIs | advanced operator, author, workflow |
| delete CIs | advanced operator, author, workflow |
| create user preference | activity implementer, advanced operator, author, change initiator, change manager, incident resolver, problem analyst, read only operator, release manager, service request analyst, workflow |
| update user preference | They can update them self only. Say Activity implementer user login as "ABC1" user then he can update "ABC1" only. Same with all the user roles.

## Default user role relationships in Service Manager

WorkItemAboutConfigItem -&gt; ConfigurationItem

- change requests - advanced operator, author, change manager, workflow
- incident records - advanced operator, author, incident resolver, workflow
- problem records - advanced operator, author, problem analyst, workflow
- release record - advanced operator, author, release manager, workflow
- service request - advanced operator, author, service request analyst, workflow

WorkItemRelatesToConfigItem &gt; ConfigurationItem

- change request – advanced operator, author, change manager, workflow
- incident record – advanced operator, author, incident resolver, workflow
- problem record – advanced operator, author, problem analyst, workflow
- release record – advanced operator, author, release manager, workflow
- service request – advanced operator, author, service request analyst, workflow

EntityLinksToKnowledgeDocument &gt; ConfigurationItem

- change request – advanced operator, author, change manager, workflow
- incident record – advanced operator, author, incident resolver, workflow
- problem record – advanced operator, author, problem analyst, workflow
- release record – advanced operator, author, release manager, workflow
- service request – advanced operator, author, service request analyst, workflow

WorkItemRelatesToWorkItem &gt; WorkItem

- change request – advanced operator, author, change manager, workflow
- incident record – advanced operator, author, incident resolver, workflow
- problem record – advanced operator, author, problem analyst, workflow
- release record – advanced operator, author, release manager, workflow
- service request – advanced operator, author, service request analyst, workflow


WorkItemAffectedUser

- incident record – advanced operator, author, incident resolver, workflow
- service request – advanced operator, author, service request analyst, workflow

WorkItemAssignedToUser

- change request – advanced operator, author, change manager, workflow
- incident record – advanced operator, author, incident resolver, workflow
- problem record - advanced operator, author, problem analyst, workflow
- release record - advanced operator, author, release manager, workflow
- service request - advanced operator, author, service request analyst, workflow

FileAttachmentAddedByUser

- change request – advanced operator, author, change manager, workflow
- incident record – advanced operator, author, incident resolver, workflow
- problem record - advanced operator, author, problem analyst, workflow
- release record - advanced operator, author, release manager, workflow
- service request - advanced operator, author, service request analyst, workflow

BillableTimeHasWorkingUser

- incident record – advanced operator, author, incident resolver, workflow

IncidentPrimaryOwner

- incident record - advanced operator, author, incident resolver, workflow

TroubleTicketResolvedByUser

- change request – advanced operator, author, change manager, workflow
- incident record – advanced operator, author, incident resolver, workflow
- problem record - advanced operator, author, problem analyst, workflow
- release record - advanced operator, author, release manager, workflow
- service request - advanced operator, author, service request analyst, workflow

TroubleTicketClosedByUser

- change request – advanced operator, author, change manager, workflow
- incident record – advanced operator, author, incident resolver, workflow
- problem record - advanced operator, author, problem analyst, workflow
- release record - advanced operator, author, release manager, workflow
- service request - advanced operator, author, service request analyst, workflow

ReviewerIsUser

- review activity - advanced operator, author, change manager, release manager, service request analyst, workflow

ReviewerVotedByUse

- review activity - advanced operator, author, change manager, release manager, service request analyst, workflow

WorkItemRelatesToRequestOffering &gt; RequestOffering

- advanced operator
- author

ServiceOfferingRelatesToRequestOffering &gt; RequestOffering

- advanced operator
- author

## Implied permissions
The following are implied permissions for Service Manager.

### ImpliedIncidentAffectedUser
The permissions for the implied Affected User profile are granted through the WorkItemAffectedUser relationship.

|Operation|Type|Property|Relationship|
|-------------|--------|------------|----------------|
|Read|Incident or service request instances, and anything that is contained within.|All properties of an incident instance.|All relationships that include the incident or service request instance.|
|Create|Work items that the user is affected by:<br /><br />-   Work item log<br />-   File attachment|All properties of a work item log and a file attachment for the incident or service request instance.|File attachment for an incident or service request instance.|
|Update|Work items that the user is affected by:<br /><br />-   Incident<br />-   Service request<br />-   Work item log<br />-   File attachment|All properties of an incident or service request instance.|Incident instance BillableTimeHasWorkingUser->User.|
|Delete|Work item that the user is affected by -  File attachment|File attachment for an incident or service request instance.|File attachment for an incident or service request instance.|

### ImpliedReviewer
The permissions for the implied Review Activity Reviewer profile are granted through the ReviewerIsUser relationship.

|Operation|Type|Property|Relationship|
|-------------|--------|------------|----------------|
|Read|Reviewer instances and anything that is contained within.|All properties of a Reviewer instances and anything that is contained within.|All relationships that include the Reviewer instance, and anything that is contained within.|
|Create|None|None|None|
|Update|None|Reviewer instances:<br /><br />-   Reviewer.Comments<br />-   Reviewer.DecisionDate<br />-   Reviewer.Decision|Reviewer Instances:<br /><br />-   ReviewerVotedByUser->User<br />-   ReviewerVotedByUser->Reviewer|
|Delete|None|None|None|

### ImpliedActivityEditor
The permissions for the implied Assigned To User profile are granted through the WorkItemAssignedToUser relationship.

|Operation|Type|Property|Relationship|
|-------------|--------|------------|----------------|
|Read|Activity instances and anything that is contained in it.|None|None|
|Create|Work item instances that the user is assigned to:<br /><br />-   Activity<br />-   Reviewer|All properties of Activity and Reviewer instances that are related to a work item instance.|All the Activity and Reviewer instances that are related to a work item Instance.|
|Update|Work item instances that the user is assigned to: Activity|All properties of an activity and the work item instances.|All Activity instances that are related to the work item Instance.|
|Delete|None|None|None|

### ImpliedConfigItemCustodian
The permissions for the implied **CI Owner** profile are granted through the **ConfigItemOwnedByUser** relationship.

|Operation|Type|Property|Relationship|
|-------------|--------|------------|----------------|
|Read|Configuration item instances and anything that is contained within.|All properties of a configuration item instance and anything that is contained in it.|All relationships that include a configuration item instance, and anything that is contained in it.|
|Create|None|None|None|
|Update|None|None|Configuration item Instance - WorkItemAboutConfigItem|
|Delete|None|None|None|

### ImpliedPrimaryComputerUser
The permissions for the implied CI Primary User profile are granted through the ComputerPrimaryUser relationship.

|Operation|Type|Property|Relationship|
|-------------|--------|------------|----------------|
|Read|Configuration item instances and anything that is contained within.|All properties of a configuration item instance and anything that is contained within.|All relationships that include the configuration item instance and anything that is contained within.|
|Create|None|None|None|
|Update|None|None|None|
|Delete|None|None|None|
