---
description:  
manager:  cfreeman
ms.topic:  article
author: bandersmsft
ms.prod:  system-center-2016
keywords:  
ms.date: 2016-10-12
title:  Appendix A - List of User Role Profiles in Service Manager
ms.technology:  service-manager
ms.assetid:  38118405-3578-4e36-b5ec-e1cc5326e161
---

# Appendix A - List of User Role Profiles in Service Manager

>Applies To: System Center 2016 - Service Manager

This appendix provides detailed information about the scope and properties of user role profiles in Service Manager.

## Tabs in the Administrator Console

The table below shows the tabs and order that they appear in the console.

| User roles | Tab order in Console |
| --- | --- |
| activity implementer | 1. Work Items <br> 2. Configurations |
| advanced operator | 1. Library <br> 2. Work Items <br> 3. Configurations |
| author | 1. Library <br> 2. Work Items <br> 3. Configurations |
| change initiator | 1. Work Items <br> 2. Configurations |
| change manager | 1. Work Items <br> 2. Configurations |
| incident resolver | 1. Work Items <br> 2. Configurations |
| problem analysts | 1. Work Items 2. Configurations |

## Default User Roles

| action | allowed roles |
| --- | --- |
| read knowledge articles | activity implementer, advanced operator, author, change initiator, change manager, end user, incident resolver, problem analyst, read only operator, release manager, service request analyst, workflow |
| edit knowledge articles | advanced operator, author |
| create knowledge articles | advanced operator, author |
| delete knowledge article | advanced operator, author |
| create change requests and activities | advanced operator, author, change initiator, change manager, workflow |
| create incident and activities | advanced operator, author, incident resolver, workflow |
| create problem records | advanced operator, author, problem analyst, workflow |
| create release records | advanced operator, author, release manager, workflow |
| create service requests and activities | advanced operator, author, service request analyst, workflow |
| edit change requests | advanced operator, author, change manager, workflow |
| edit incidents | advanced operator, author, incident resolver, workflow |
| edit problem records | advanced operator, author, problem analyst, workflow |
| edit release records | advanced operator, author, release manager, workflow |
| edit service requests | advanced operator, author, service request analyst, workflow |
| update status for change requests | advanced operator, author, change manager, workflow |
| update status for incidents | advanced operator, author, incident resolver, workflow |
| update status for service requests | advanced operator, author, service request analyst, workflow |
| update status for manual activity | advanced operator, author, change manager, incident resolver, release manager, service request analyst, workflow |
| update status for review activity | advanced operator, author, change manager, incident resolver, release manager, service request analyst, workflow |
| create CIs | advanced operator, author, workflow |
| update CIs | advanced operator, author, workflow |
| delete CIs | advanced operator, author, workflow |
| create user preference | advanced operator, author, workflow |
| update user preference | advanced operator, author, release manager, service request analyst, workflow |
| create work item log | advanced operator, author, author, change initiator, change manager, incident resolver, problem analyst, release manager, service request analyst, workflow |
| update work item log | advanced operator, author, author, change initiator, change manager, incident resolver, problem analyst, release manager, service request analyst, workflow |

## Default user role relationships in Service Manager

WorkItemAboutConfigItem -&gt; ConfigurationItem

- change requests - change manager
- incident records - incident resolver
- problem records - problem analyst
- release record - release manager
- service request - service request analyst

WorkItemRelatesToConfigItem &gt; ConfigurationItem

- change request – change manager
- incident record – incident resolver
- problem record – problem analyst
- release record – release manager
- service request – service request analyst

EntityLinksToKnowledgeDocument &gt; ConfigurationItem

- change request – change manager
- incident record – incident resolver
- problem record – problem analyst
- release record – release manager
- service request – service request analyst

WorkItemRelatesToWorkItem &gt; WorkItem

- change request – change manager
- incident record – incident resolver
- problem record – problem analyst
- release record – release manager
- service request – service request analyst

UserHasPreference-&gt;User

- activity implementer
- advanced operator
- author
- incident resolver
- problem analysts
- release manager
- service request analyst

WorkItemAffectedUser

- incident record – advanced operator, author, incident resolver
- service request – advanced operator, author, service request analyst

WorkItemAssignedToUser

- change request – advanced operator, author, change manager
- incident record – advanced operator, author, incident resolver
- problem record - advanced operator, author, problem analyst
- release record - advanced operator, author, release manager
- service request - advanced operator, author, service request analyst

WorkItemCreatedByUser

- change request - advanced operator, author,

FileAttachmentAddedByUser

- change request - advanced operator, author, change manager
- incident record - advanced operator, author, incident resolver
- problem record - advanced operator, author, problem analyst
- release record - advanced operator, author, release manager
- service request - advanced operator, author, service request analyst

BillableTimeHasWorkingUser

- incident record – activity implementer, advanced operator, author, incident resolver

IncidentPrimaryOwner

- incident record - advanced operator, author, incident resolver

TroubleTicketResolvedByUser

- change request - advanced operator, author, change manager
- incident record - advanced operator, author, incident resolver
- problem record - advanced operator, author, problem analyst
- release record - advanced operator, author
- service request - advanced operator, author

TroubleTicketClosedByUser

- change request - advanced operator, author, change manager
- incident record - advanced operator, author, incident resolver
- problem record - advanced operator, author, problem analyst
- release record - advanced operator, author,
- service request - advanced operator, author,

ReviewerIsUser

- review activity - advanced operator, author, change manager, release manager, service request analyst

ReviewerVotedByUse

- review activity - advanced operator, author, change manager, release manager, service request analyst

WorkItemRelatesToRequestOffering &gt; RequestOffering

- advanced operator
- author

ServiceOfferingRelatesToRequestOffering &gt; RequestOffering

- author

## Implied Permissions

Implied Incident Affected User

- read – activity implementer, advanced operator, author, change initiator, change manager, incident resolver, problem analyst, read only operator, release manager, service request analyst, workflow
- create - activity implementer, advanced operator, author, change initiator, change manager, incident resolver, problem analyst, read only operator, release manager, service request analyst, workflow
- update - activity implementer, advanced operator, author, change initiator, change manager, incident resolver, problem analyst, read only operator, release manager, service request analyst, workflow
- delete - activity implementer, advanced operator, author, change initiator, change manager, incident resolver, problem analyst, read only operator, release manager, service request analyst, workflow

Implied Reviewer

- read - activity implementer, advanced operator, author, change initiator, change manager, incident resolver, problem analyst, read only operator, release manager, service request analyst, workflow
- create – not applicable
- update - not applicable
- delete - not applicable

Implied Activity Editor

- read - activity implementer, advanced operator, author, change initiator, change manager, incident resolver, problem analyst, read only operator, release manager, service request analyst, workflow
- create – advanced operator, author, workflow
- update - advanced operator, author, incident resolver, workflow
- delete - activity implementer, advanced operator, author, change initiator, change manager, incident resolver, problem analyst, read only operator, release manager, service request analyst, workflow

Implied ConfigItem Custodian

- read - activity implementer, advanced operator, author, change initiator, change manager, incident resolver, problem analyst, read only operator, release manager, service request analyst, workflow
- create - not applicable
- update - not applicable
- delete - not applicable

Implied Primary Computer User

- read - activity implementer, advanced operator, author, change initiator, change manager, incident resolver, problem analyst, read only operator, release manager, service request analyst, workflow
- create – not applicable
- update - not applicable
- delete - not applicable

## Implied Incident Affected User

Create work items

- activity implementer
- advanced operator
- author
- change initiator
- change manager
- incident resolver
- problem analyst
- read only operator
- release manager
- service request analyst
- workflow

Delete work items

- activity implementer
- advanced operator
- author
- change initiator
- change manager
- incident resolver
- problem analyst
- read only operator
- release manager
- service request analyst
- workflow

Relationships

- Create – activity implementer, advanced operator, author, change initiator, change manager, incident resolver, problem analyst, read only operator, release manager, service request analyst, workflow
- Update – activity implementer, advanced operator, author, change initiator, change manager, incident resolver, problem analyst, read only operator, release manager, service request analyst, workflow
- Delete – activity implementer, advanced operator, author, change initiator, change manager, incident resolver, problem analyst, read only operator, release manager, service request analyst, workflow

## Implied Reviewer

- Create activity – activity implementer, change initiator, incident resolver, problem analyst, read only operator
- Update activity – activity implementer, change initiator, incident resolver, problem analyst, read only operator
- Delete activity – activity implementer, change initiator, incident resolver, problem analyst, read only operator
- Relationship update - activity implementer, advanced operator, author, change initiator, change manager, incident resolver, problem analyst, read only operator, release manager, service request analyst, workflow

## Implied Activity Editor

- Create activity – advanced operator, author, workflow
- Update activity – advanced operator, author, incident resolver, workflow
- Delete activity – activity implementer, advanced operator, author, change initiator, change manager, incident resolver, problem analyst, read only operator, release manager, service request analyst, workflow
- Relationship create – advanced operator, author, workflow
- Relationship update – advanced operator, author, incident resolver, workflow

## Implied Configuration Item Custodian

- Create configuration item – activity implementer, change initiator, change manager, incident resolver, problem analyst, read only operator, release manager, service request analyst
- Update configuration item – activity implementer, change initiator, change manager, incident resolver, problem analyst, read only operator, release manager, service request analyst
- Delete configuration item – activity implementer, change initiator, change manager, incident resolver, problem analyst, read only operator, release manager, service request analyst
- Relationship update – advanced operator, author, workflow

## Implied Primary Computer User

- Create configuration item – activity implementer, change initiator, change manager, incident resolver, problem analyst, read only operator, release manager, service request analyst
- Update configuration item – Create configuration item – activity implementer, change initiator, change manager, incident resolver, problem analyst, read only operator, release manager, service request analyst
- Create configuration item – activity implementer, change initiator, change manager, incident resolver, problem analyst, read only operator, release manager, service request analyst
