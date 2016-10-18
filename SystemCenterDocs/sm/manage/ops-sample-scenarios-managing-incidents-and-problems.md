---
title: Sample Scenarios - Managing Incidents and Problems
manager: cfreeman
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 094a22c8-b315-4bc6-872f-60efe5e8f961
---


# Sample Scenarios - Managing Incidents and Problems

>Applies To: System Center 2016 - Service Manager

These sample scenarios for Service Manager help you achieve your goal of managing incidents and problems by using multiple scenarios end to end. You can think of these sample scenarios as a case study that helps put the individual scenarios and procedures in context.  

## Scenarios for Managing Incidents and Problems  

|Scenario|Description|  
|--------------|-----------------|  
|[Managing Incidents](ops-managing-incidents.md)|Describes how incidents and incident views are created, edited, and resolved.|  
|[Troubleshooting Incidents](ops-troubleshooting-incidents.md)|Describes how to troubleshoot incidents using service maps and by running tasks.|  
|[Managing Problems](ops-managing-problems.md)|Describes how to create and edit problem records, resolve problems and related incidents automatically, and link incidents or change request to a problem record.|  

### Managing Incidents  
 In the scenario that encompasses incident management, Phil uses incident management to restore regular operations as quickly and as cost\-effectively as possible. For example, by using the E\-mail Incident template to populate a new email\-related incident, he can quickly create an incident and ensure that the correct **Impact**, **Urgency**, **Assigned Analyst**, and **Support Tier** fields are configured. Carrying the example further, he creates a new incident for a user who is unable to view an email that was sent with restricted permissions. Phil creates an incident view so that he can easily work with all incidents that are created for email problems. When changes are made to an incident, he edits the incident to reflect the changes.  

 In another example, an end user experiences a printer problem, and she sends an email message to the help desk. Upon receipt of the message, Service Manager automatically creates an incident from the message. Phil investigates the problem, in part, by viewing the service. After the underlying problem has been solved, he resolves and closes the incident.  

 At Woodgrove Bank, connectors are configured in such a way that Service Manager imports configuration items and alerts from, so that some new incidents are created automatically. Phil reviews the automatically created incidents for accuracy.  

### Troubleshooting Incidents  
 In the scenario that encompasses troubleshooting incidents, Phil is conducting an initial investigation of the problem that Joe is experiencing. Phil suspects that the root cause of the problem is that an update for Microsoft Exchange Server needs to be applied to Joe's Exchange server. However, there are other Exchange servers at Woodgrove Bank that probably also need to be updated. Phil starts his investigation by viewing the service that Garret created for the Exchange service. When any incidents affect a service component, that component is marked with an orange icon resembling a square containing an exclamation point. When a change request affects a service component, the component is marked with a special blue icon resembling a square containing a right\-pointing arrow. Phil uses the map view on the **Service Components** tab to view configuration items and view incidents associated with them. Then, he opens other configuration items and adds them to the open incident.  

 To further troubleshoot, Phil wants to ping a remote computer that is exhibiting problems. He can use tasks that are part of the Service Manager console instead of having to use various other tools.  

### Managing Problems  
 In the scenario that encompasses problem management, Phil has created a change request asking the Exchange Administrators group to apply an update, which is expected to resolve the problem. When a root cause is found and mitigated or resolved, the change request is completed and Phil is notified. He then uses the prescribed procedures to resolve a problem and automatically resolve incidents associated with the problem.  
