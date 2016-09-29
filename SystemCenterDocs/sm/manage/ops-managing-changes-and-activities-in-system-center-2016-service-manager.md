---
title: Managing Changes and Activities in System Center - Service Manager
manager: cfreeman
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 2016-10-12
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6228f358-1256-475f-8d63-9bdf62070ecd
---

# Managing Changes and Activities in System Center - Service Manager

>Applies To: System Center 2016 - Service Manager

Information Technology (IT) departments must manage changes to their IT environment and the risk associated with such changes. The change management features in Service Manager help you manage change by providing repeatable, predictable, and measured processes to implement change.

The topics in this section are organized according to common change management scenarios. Even though the sample scenarios refer to a fictitious organization, Woodgrove Bank, the scenarios and steps are based on real use, and they describe how to use the change and activity management features in Service Manager.


## Sample Scenario: Managing Changes and Activities

This sample scenario for System Center 2016 - Service Manager helps you achieve your goal of managing changes and activities by using multiple scenarios end to end. You can think of this sample scenario as a case study that helps put the individual scenarios and procedures in context.  

### Scenarios for Managing Changes and Activities  

|Scenario|Description|  
|--------------|-----------------|  
|[Initiating and Classifying a Change Request](ops-initiating-and-classifying-a-change-request.md)|Describes how change requests are started and classified. Also describes how to add items and activities to change requests.|  
|[Approving and Modifying Change Requests](ops-approving-and-modifying-change-requests.md)|Describes how to modify change requests by adding change details and change reviewers. Also describes how to approve a review activity.|  
|[Suspending and Resuming a Change Request](ops-suspending-and-resuming-a-change-request.md)|Describes how to pause and resume a change request.|  
|[Implementing and Closing a Change Request](ops-implementing-and-closing-a-change-request.md)|Describes how to complete manual activities to track tasks, how to close a change request after you finalize the changes, and how to notify users.|  

### Initiating and Classifying Change Requests  
 In the scenario that encompasses initiating and classifying a change request, Julia, the messaging support analyst, wants to propose and track a change. To do this, she creates a change request to capture information that she and others will use to evaluate, plan, develop, test, deploy, and assess changes. Julia starts by initiating the change request and then identifying its priority and category.  

 In incident management scenarios, Phil created an incident in which a user had a messaging problem, and he completed an initial investigation of the problem. In this scenario, Julia continues to investigate the same incident. She verifies that the cause is a known issue with Microsoft Exchange Server and fixes it. She also determines that all Exchange servers need a update, not just a single server. Next, Julia views the service map for the Exchange service configuration item that requires the update, and she opens a change request from the service's configuration item form. Lastly, Julia attaches a saved screen shot to the change request, which might help later with the change request review.  

 After the change request is created, the change reviewers at Woodgrove Bank must approve the change request, and the change implementers must complete the actions that are required for the change. These review and implementation steps are defined in the change request as a set of review activities and manual activities.  

### Approving Change Requests  
 In the scenario that encompasses approving a change request, Garret wants to enforce the Woodgrove Bank business process of requiring approval of any IT infrastructure changes before the changes are deployed. He wants to enforce this business process by using Service Manager to associate review activities for a change request. By requiring approval, the change request is implemented only after decision makers at Woodgrove Bank agree that the change is necessary. Garret can set up various review methods, such as unanimous voting, percentage of positive votes, or automatic approval.  

 The procedures that are related to this scenario describe a change to Woodgrove Bank's IT infrastructure that is approved before deployment.  

### Suspending and Resuming Change Requests  
 During the course of reviewing the readiness of a change request, Garret occasionally wants to put a change request on hold and then later resume that change request. For example, Julia previously created a change request. That change request depends on the additional work of an external team. Garret wants to put that change request on hold until the external team completes its work. Garret will resume the change request after the external team's work is complete. Garret also wants to occasionally unblock failed change requests.  

### Implementing and Closing Change Requests  
 After changes to Garret's IT infrastructure are tested and approved for deployment, his final step is to finish any remaining manual activities that are associated with the change request. A manual activity must be designated as either completed or failed. When all manual activities are completed, the change request is automatically set as completed, and it appears in the **Change Requests: Completed** view. If a manual activity fails, the change request is automatically set as failed, and it appears in the **Change Requests: Failed** view. When the change request appears in either view, Garret can close the change request. After a change request has been closed, it cannot be reopened.  

 In the scenario that encompasses implementing and closing change requests, Aaron completes a warranty review manual activity. Next, Garret sets the change request's remaining manual activities to **Completed**, and closes the change request. Garret opens a second existing change request, sets the post\-implementation manual activity to **Failed**, and then closes that change request.  
