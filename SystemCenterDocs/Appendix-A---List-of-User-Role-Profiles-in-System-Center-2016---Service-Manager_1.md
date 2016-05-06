---
title: Appendix A - List of User Role Profiles in System Center 2016 - Service Manager_1
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 796e8eaf-649d-40b9-8a47-9f79fc6df038
robots: noindex,nofollow
---
# Appendix A - List of User Role Profiles in System Center 2016 - Service Manager_1
This appendix provides detailed information about the scope and properties of user role profiles in [!INCLUDE[scsm_threshold_1](Token/scsm_threshold_1_md.md)].

## EndUser

|Operation|Instance Type Scope|Properties|Relationships|Presentational Elements Scope|
|-------------|-----------------------|--------------|-----------------|---------------------------------|
|Read|All|All|All|Object Templates|
|Create|-   Work Item<br />-   Work Item Log<br />-   File Attachment<br />-   Reviewer<br />-   User Preference|All for the specified types.|All for the specified types.|None|
|Update|-   File Attachment<br />-   Work Item Log<br />-   Star Rating|All for the specified types.|-   DocumentHasAverageRating\->KnowledgeArticle<br />-   UserHasPreference\->User<br />-   WorkItemAffectedUser\->User<br />-   WorkItemAssignedToUser\->User<br />-   WorkItemCreatedByUser\->User<br />-   FileAttachmentAddedByUser\->User<br />-   BillableTimeHasWorkingUser\->User<br />-   IncidentPrimaryOwner\->User<br />-   TroubleTicketResolvedByUser\->User<br />-   TroubleTicketClosedByUser\->User<br />-   ReviewerIsUser\->User<br />-   ReviewerVotedByUser\->User<br />-   WorkItemRelatesToWorkItem\->WorkItem<br />-   WorkItemRelatesToRequestOffering\->RequestOffering<br />-   WorkItemRelatesToConfigItem\->ConfigurationItem<br />-   WorkItemAboutConfigItem\->ConfigurationItem|None|
|Delete|None|None|None|None|

## ReadOnlyOperator

|Operation|Instance Type Scope|Properties|Relationships|Presentational Elements Scope|
|-------------|-----------------------|--------------|-----------------|---------------------------------|
|Read|All|All|All|All|
|Create|-   User Preference<br />-   Personal Notification|All for the specified types.|All for the specified types.|None|
|Update|||-   WorkItemAboutConfigItem\->ConfigurationItem<br />-   WorkItemRelatesToConfigItem\->ConfigurationItem<br />-   EntityLinksToKnowledgeDocument\->ConfigurationItem<br />-   UserHasPreference\->User<br />-   WorkItemAffectedUser\->User<br />-   WorkItemAssignedToUser\->User<br />-   WorkItemCreatedByUser\->User<br />-   FileAttachmentAddedByUser\->User<br />-   BillableTimeHasWorkingUser\->User<br />-   IncidentPrimaryOwner\->User<br />-   TroubleTicketResolvedByUser\->User<br />-   TroubleTicketClosedByUser\->User<br />-   ReviewerIsUser\->User<br />-   ReviewerVotedByUser\->User<br />-   WorkItemRelatesToRequestOffering\->RequestOffering<br />-   WorkItemRelatesToWorkItem\->WorkItem|None|
|Delete|None|None|None|None|

## IncidentResolver

|Operation|Instance Type Scope|Properties|Relationships|Presentational Elements Scope|
|-------------|-----------------------|--------------|-----------------|---------------------------------|
|Read|All|All|All|All|
|Create|-   Incident<br />-   Manual Activity<br />-   File Attachment<br />-   Work Item Log<br />-   User Preference<br />-   Personal Notification|All for the specified types.|All for the specified types.|None|
|Update|-   File Attachment<br />-   Work Item Log<br />-   Manual Activity<br />-   Star Rating|All for the specified types.|-   WorkItemAboutConfigItem\->ConfigurationItem<br />-   WorkItemRelatesToConfigItem\->ConfigurationItem<br />-   EntityLinksToKnowledgeDocument\->ConfigurationItem<br />-   WorkItemRelatesToWorkItem\->WorkItem<br />-   DocumentHasAverageRating\->KnowledgeArticle<br />-   UserHasPreference\->User<br />-   WorkItemAffectedUser\->User<br />-   WorkItemAssignedToUser\->User<br />-   WorkItemCreatedByUser\->User<br />-   FileAttachmentAddedByUser\->User<br />-   WorkItem.BillableTimeHasWorkingUser\->User<br />-   WorkItem.IncidentPrimaryOwner\->User<br />-   WorkItem.TroubleTicketResolvedByUser\->User<br />-   WorkItem.TroubleTicketClosedByUser\->User<br />-   ReviewerIsUser\->User<br />-   ReviewerVotedByUser\->User|None|
|Delete|-   File Attachment<br />-   Manual Activity|All for the specified types.|All for the specified types.|None|

## ChangeInitiator

|Operation|Instance Type Scope|Properties|Relationships|Presentational Elements Scope|
|-------------|-----------------------|--------------|-----------------|---------------------------------|
|Read|All|All|All|All|
|Create|-   Change Request<br />-   Activity<br />-   File Attachment<br />-   Work Item Log<br />-   Reviewer<br />-   User Preference<br />-   Personal Notification|All for the specified types.|All for the specified types.|None|
|Update|Star Rating|All for the specified types.|-   WorkItemAboutConfigItem\->ConfigurationItem<br />-   WorkItemRelatesToConfigItem\->ConfigurationItem<br />-   EntityLinksToKnowledgeDocument\->ConfigurationItem<br />-   WorkItemRelatesToWorkItem\->WorkItem<br />-   DocumentHasAverageRating\->KnowledgeArticle<br />-   UserHasPreference\->User<br />-   WorkItemAffectedUser\->User<br />-   WorkItemAssignedToUser\->User<br />-   WorkItemCreatedByUser\->User<br />-   FileAttachmentAddedByUser\->User<br />-   BillableTimeHasWorkingUser\->User<br />-   IncidentPrimaryOwner\->User<br />-   TroubleTicketResolvedByUser\->User<br />-   TroubleTicketClosedByUser\->User<br />-   ReviewerIsUser\->User<br />-   ReviewerVotedByUser\->User<br />-   WorkItemAboutCatalogItem\->CatalogItem|None|
|Delete|None|None|None|None|

## ActivityImplementer

|Operation|Instance Type Scope|Properties|Relationships|Presentational Elements Scope|
|-------------|-----------------------|--------------|-----------------|---------------------------------|
|Read|All|All|All|All|
|Create|-   User Preference<br />-   Personal Notification|All for the specified types.|All for the specified types.|None|
|Update|Star Rating|-   ManualActivity. Status<br />-   ManualActivity.Notes|-   WorkItemAboutConfigItem\->ConfigurationItem<br />-   WorkItemRelatesToConfigItem\->ConfigurationItem<br />-   EntityLinksToKnowledgeDocument\->ConfigurationItem<br />-   WorkItemRelatesToWorkItem\->WorkItem<br />-   DocumentHasAverageRating\->KnowledgeArticle<br />-   UserHasPreference\->User<br />-   WorkItemAffectedUser\->User<br />-   WorkItemAssignedToUser\->User<br />-   WorkItemCreatedByUser\->User<br />-   FileAttachmentAddedByUser\->User<br />-   BillableTimeHasWorkingUser\->User<br />-   IncidentPrimaryOwner\->User<br />-   TroubleTicketResolvedByUser\->User<br />-   TroubleTicketClosedByUser\->User<br />-   ReviewerIsUser\->User<br />-   ReviewerVotedByUser\->User|None|
|Delete|None|None|None|None|

## ProblemAnalyst

|Operation|Instance Type Scope|Properties|Relationships|Presentational Elements Scope|
|-------------|-----------------------|--------------|-----------------|---------------------------------|
|Read|All|All|All|All|
|Create|-   Problem<br />-   File Attachment<br />-   Work Item Log<br />-   User Preference<br />-   Personal Notification|All for the specified types.|All for the specified types.|None|
|Update|-   Problem<br />-   File Attachment<br />-   Work Item Log<br />-   Star Rating|All for the specified types.|-   WorkItemAboutConfigItem\->ConfigurationItem<br />-   WorkItemRelatesToConfigItem\->ConfigurationItem<br />-   EntityLinksToKnowledgeDocument\->ConfigurationItem<br />-   WorkItemRelatesToWorkItem\->WorkItem<br />-   DocumentHasAverageRating\->KnowledgeArticle<br />-   UserHasPreference\->User<br />-   WorkItemAffectedUser\->User<br />-   WorkItemAssignedToUser\->User<br />-   WorkItemCreatedByUser\->User<br />-   FileAttachmentAddedByUser\->User<br />-   BillableTimeHasWorkingUser\->User<br />-   IncidentPrimaryOwner\->User<br />-   TroubleTicketResolvedByUser\->User<br />-   TroubleTicketClosedByUser\->User<br />-   ReviewerIsUser\->User<br />-   ReviewerVotedByUser\->User|None|
|Delete|File Attachment|All for the specified types.|All for the specified types.|None|

## ServiceRequestAnalyst

|Operation|Instance Type Scope|Properties|Relationships|Presentational Elements Scope|
|-------------|-----------------------|--------------|-----------------|---------------------------------|
|Read|All|All|All|All|
|Create|All for the specified types.|All for the specified types.|All for the specified types.|None|
|Update|-   Service Request<br />-   Activity<br />-   File Attachment<br />-   Work Item Log<br />-   Reviewer<br />-   Star Rating||-   WorkItemAboutConfigItem\->ConfigurationItem<br />-   WorkItemRelatesToConfigItem\->ConfigurationItem<br />-   EntityLinksToKnowledgeDocument\->ConfigurationItem<br />-   WorkItemRelatesToWorkItem\->WorkItem<br />-   Knowledge.DocumentHasAverageRating\->KnowledgeArticle<br />-   WorkItemAffectedUser\->User<br />-   UserHasPreference\->User<br />-   WorkItemAssignedToUser\->User<br />-   WorkItemCreatedByUser\->User<br />-   FileAttachmentAddedByUser\->User<br />-   ReviewerIsUser\->User<br />-   ReviewerVotedByUser\->User<br />-   WorkItemRelatesToRequestOffering\->RequestOffering|None|
|Delete|-   Activity<br />-   File Attachment<br />-   Reviewer|All for the specified types.|All for the specified types.|None|

## ReleaseManager

|Operation|Instance Type Scope|Properties|Relationships|Presentational Elements Scope|
|-------------|-----------------------|--------------|-----------------|---------------------------------|
|Read|All|All|All|All|
|Create|-   Release Record<br />-   Activity<br />-   File Attachment<br />-   Work Item Log<br />-   Reviewer<br />-   User Preference<br />-   Personal Notification|All for the specified types.|All for the specified types.|None|
|Update|-   Release Record<br />-   Activity<br />-   File Attachment<br />-   Work Item Log<br />-   Reviewer<br />-   Star Rating|All for the specified types.|-   WorkItemAboutConfigItem\->ConfigurationItem<br />-   WorkItemRelatesToConfigItem\->ConfigurationItem<br />-   EntityLinksToKnowledgeDocument\->ConfigurationItem<br />-   WorkItemRelatesToWorkItem\->WorkItem<br />-   DocumentHasAverageRating\->KnowledgeArticle<br />-   WorkItemAffectedUser\->User<br />-   UserHasPreference\->User<br />-   WorkItemAssignedToUser\->User<br />-   WorkItemCreatedByUser\->User<br />-   FileAttachmentAddedByUser\->User<br />-   ReviewerIsUser\->User<br />-   ReviewerVotedByUser\->User|None|
|Delete|-   Activity<br />-   File Attachment<br />-   Reviewer|All for the specified types.|All for the specified types.|None|

## ChangeManager

|Operation|Instance Type Scope|Properties|Relationships|Presentational Elements Scope|
|-------------|-----------------------|--------------|-----------------|---------------------------------|
|Read|All|All|All|All|
|Create|-   Change Request<br />-   Activity<br />-   File Attachment<br />-   Work Item Log<br />-   Reviewer<br />-   User Preference<br />-   Personal Notification|All for the specified types.|All for the specified types.|None|
|Update|-   Change Request<br />-   Change Request<br />-   Activity<br />-   File Attachment<br />-   Work Item Log<br />-   Reviewer<br />-   Star Rating|All for the specified types.|-   WorkItemAboutConfigItem\->ConfigurationItem<br />-   WorkItemRelatesToConfigItem\->ConfigurationItem<br />-   EntityLinksToKnowledgeDocument\->ConfigurationItem<br />-   WorkItemRelatesToWorkItem\->WorkItem<br />-   Knowledge.DocumentHasAverageRating\->KnowledgeArticle<br />-   WorkItemAffectedUser\->User<br />-   UserHasPreference\->User<br />-   WorkItemAssignedToUser\->User<br />-   WorkItemCreatedByUser\->User<br />-   FileAttachmentAddedByUser\->User<br />-   WorkItem.BillableTimeHasWorkingUser\->User<br />-   WorkItem.IncidentPrimaryOwner\->User<br />-   WorkItem.TroubleTicketResolvedByUser\->User<br />-   WorkItem.TroubleTicketClosedByUser\->User<br />-   ReviewerIsUser\->User<br />-   ReviewerVotedByUser\->User<br />-   WorkItemAboutCatalogItem \->CatalogItem|None|
|Delete|-   Activity<br />-   File Attachment<br />-   Reviewer|All for the specified types.|All for the specified types.|None|

## AdvancedOperator

|Operation|Instance Type Scope|Properties|Relationships|Presentational Elements Scope|
|-------------|-----------------------|--------------|-----------------|---------------------------------|
|Read|All|All|All|All|
|Create|-   Work Item<br />-   Configuration Item<br />-   Announcement<br />-   File Attachment<br />-   Work Item Log<br />-   Reviewer<br />-   User Preference<br />-   Personal Notification|All for the specified types.|All for the specified types.|None|
|Update|-   Work Item<br />-   Configuration Item<br />-   Announcement<br />-   File Attachment<br />-   Work Item Log<br />-   Reviewer<br />-   User Preference|All for the specified types.|-   Knowledge.DocumentHasAverageRating\->KnowledgeArticle<br />-   UserHasPreference\->User<br />-   WorkItemAffectedUser\->User<br />-   WorkItemAssignedToUser\->User<br />-   WorkItemCreatedByUser\->User<br />-   FileAttachmentAddedByUser\->User<br />-   BillableTimeHasWorkingUser\->User<br />-   IncidentPrimaryOwner\->User<br />-   TroubleTicketResolvedByUser\->User<br />-   TroubleTicketClosedByUser\->User<br />-   ReviewerIsUser\->User<br />-   ReviewerVotedByUser\->User<br />-   WorkItemRelatesToRequestOffering\->RequestOffering|None|
|Delete|-   Announcement<br />-   Activity<br />-   Reviewer<br />-   File Attachment|All for the specified types.|All for the specified types.|None|

## Author

|Operation|Instance Type Scope|Properties|Relationships|Presentational Elements Scope|
|-------------|-----------------------|--------------|-----------------|---------------------------------|
|Read|All|All|All|All|
|Create|-   Work Item<br />-   Configuration Item<br />-   Catalog Item<br />-   Announcement<br />-   File Attachment<br />-   Work Item Log<br />-   Reviewer<br />-   User Preference<br />-   Personal Notification|All for the specified types.|All for the specified types.|-   Template<br />-   View<br />-   Folder<br />-   Enumeration|
|Update|-   Work Item<br />-   Configuration Item<br />-   Catalog Item<br />-   Announcement<br />-   File Attachment<br />-   Work Item Log<br />-   Reviewer<br />-   Star Rating||-   DocumentHasAverageRating\->KnowledgeArticle<br />-   UserHasPreference\->User<br />-   WorkItemAffectedUser\->User<br />-   WorkItemAssignedToUser\->User<br />-   WorkItemCreatedByUser\->User<br />-   FileAttachmentAddedByUser\->User<br />-   BillableTimeHasWorkingUser\->User<br />-   IncidentPrimaryOwner\->User<br />-   TroubleTicketResolvedByUser\->User<br />-   TroubleTicketClosedByUser\->User<br />-   ReviewerIsUser\->User<br />-   ReviewerVotedByUser\->User<br />-   ServiceOfferingRelatesToRequestOffering\->RequestOffering|-   Template<br />-   View<br />-   Folder<br />-   Enumeration|
|Delete|-   Activity<br />-   Reviewer<br />-   File Attachment<br />-   Announcement|All for the specified types.|All for the specified types.|-   Template<br />-   View<br />-   Folder<br />-   Enumeration|

## Workflow

|Operation|Instance Type Scope|Properties|Relationships|Presentational Elements Scope|
|-------------|-----------------------|--------------|-----------------|---------------------------------|
|Read|All|All|All|All|
|Create|-   Work Item<br />-   Configuration Item<br />-   Announcement<br />-   File Attachment<br />-   Work Item Log<br />-   Reviewer<br />-   SLA Information<br />-   Admin Item SLA<br />-   User Preference|All for the specified types.|All for the specified types.|None|
|Update|-   Work Item<br />-   Configuration Item<br />-   Announcement<br />-   File Attachment<br />-   Work Item Log<br />-   Reviewer<br />-   SLA Information<br />-   Admin Item SLA<br />-   Star Rating|-   System.Knowledge.DocumentHasAverageRating<br />-   System.UserHasPreference<br />-   System.WorkItemAffectedUser<br />-   System.WorkItemAssignedToUser<br />-   System.WorkItemCreatedByUser<br />-   System.FileAttachmentAddedByUser<br />-   System.WorkItem.BillableTimeHasWorkingUser<br />-   System.WorkItem.IncidentPrimaryOwner<br />-   System.WorkItem.TroubleTicketResolvedByUser<br />-   System.WorkItem.TroubleTicketClosedByUser<br />-   System.ReviewerIsUser<br />-   System.ReviewerVotedByUser|None|
|Delete|DCM\_NonCompliance\_CI|All for the specified types.|All for the specified types.|None|

## ReportUser

|Operation|Instance Type Scope|Properties|Relationships|Presentational Elements Scope|
|-------------|-----------------------|--------------|-----------------|---------------------------------|
|Read|SRS Resource Store|All for the specified type|All for the specified type|None|
|Create|Personal Notification|All for the specified type|All for the specified type|None|
|Update|None|None|None|None|
|Delete|None|None|None|None|

## ImpliedIncidentAffectedUser
The permissions for the implied Affected User profile are granted through the WorkItemAffectedUser relationship.

|Operation|Type|Property|Relationship|
|-------------|--------|------------|----------------|
|Read|Incident or service request instances, and anything that is contained within.|All properties of an incident instance.|All relationships that include the incident or service request instance.|
|Create|Work items that the user is affected by:<br /><br />-   Work item log<br />-   File attachment|All properties of a work item log and a file attachment for the incident or service request instance.|File attachment for an incident or service request instance.|
|Update|Work items that the user is affected by:<br /><br />-   Incident<br />-   Service request<br />-   Work item log<br />-   File attachment|All properties of an incident or service request instance.|Incident instance BillableTimeHasWorkingUser\->User.|
|Delete|Work item that the user is affected by \-  File attachment|File attachment for an incident or service request instance.|File attachment for an incident or service request instance.|

## ImpliedReviewer
The permissions for the implied Review Activity Reviewer profile are granted through the ReviewerIsUser relationship.

|Operation|Type|Property|Relationship|
|-------------|--------|------------|----------------|
|Read|Reviewer instances and anything that is contained within.|All properties of a Reviewer instances and anything that is contained within.|All relationships that include the Reviewer instance, and anything that is contained within.|
|Create|None|None|None|
|Update|None|Reviewer instances:<br /><br />-   Reviewer.Comments<br />-   Reviewer.DecisionDate<br />-   Reviewer.Decision|Reviewer Instances:<br /><br />-   ReviewerVotedByUser\->User<br />-   ReviewerVotedByUser\->Reviewer|
|Delete|None|None|None|

## ImpliedActivityEditor
The permissions for the implied Assigned To User profile are granted through the WorkItemAssignedToUser relationship.

|Operation|Type|Property|Relationship|
|-------------|--------|------------|----------------|
|Read|Activity instances and anything that is contained in it.|None|None|
|Create|Work item instances that the user is assigned to:<br /><br />-   Activity<br />-   Reviewer|All properties of Activity and Reviewer instances that are related to a work item instance.|All the Activity and Reviewer instances that are related to a work item Instance.|
|Update|Work item instances that the user is assigned to: Activity|All properties of an activity and the work item instances.|All Activity instances that are related to the work item Instance.|
|Delete|None|None|None|

## ImpliedConfigItemCustodian
The permissions for the implied **CI Owner** profile are granted through the **ConfigItemOwnedByUser** relationship.

|Operation|Type|Property|Relationship|
|-------------|--------|------------|----------------|
|Read|Configuration item instances and anything that is contained within.|All properties of a configuration item instance and anything that is contained in it.|All relationships that include a configuration item instance, and anything that is contained in it.|
|Create|None|None|None|
|Update|None|None|Configuration item Instance \- WorkItemAboutConfigItem|
|Delete|None|None|None|

## ImpliedPrimaryComputerUser
The permissions for the implied CI Primary User profile are granted through the ComputerPrimaryUser relationship.

|Operation|Type|Property|Relationship|
|-------------|--------|------------|----------------|
|Read|Configuration item instances and anything that is contained within.|All properties of a configuration item instance and anything that is contained within.|All relationships that include the configuration item instance and anything that is contained within.|
|Create|None|None|None|
|Update|None|None|None|
|Delete|None|None|None|


