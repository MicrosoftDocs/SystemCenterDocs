---
title: Sample Scenarios: Managing Incidents and Problems
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e6993e0d-c9db-4b46-b71f-e02d6639bdd8
robots: noindex,nofollow
---
# Sample Scenarios: Managing Incidents and Problems
These sample scenarios for [!INCLUDE[scsm_threshold_1](../Token/scsm_threshold_1_md.md)] help you achieve your goal of managing incidents and problems by using multiple scenarios end to end. You can think of these sample scenarios as a case study that helps put the individual scenarios and procedures in context.

## Scenarios for Managing Incidents and Problems

|Scenario|Description|
|------------|---------------|
|[Managing Incidents_Retired](../Topic/Managing-Incidents_Retired.md)|Describes how incidents and incident views are created, edited, and resolved.|
|[Troubleshooting incidents](assetId:///44090039-636d-4ab2-bed7-b2196397d781)|Describes how to troubleshoot incidents using service maps and by running tasks.|
|[Managing Problems](assetId:///62f1e2c8-2c78-41f6-a737-8d8fefd6079d)|Describes how to create and edit problem records, resolve problems and related incidents automatically, and link incidents or change request to a problem record.|

### Managing Incidents
In the scenario that encompasses incident management, Phil uses incident management to restore regular operations as quickly and as cost\-effectively as possible. For example, by using the E\-mail Incident template to populate a new email\-related incident, he can quickly create an incident and ensure that the correct **Impact**, **Urgency**, **Assigned Analyst**, and **Support Tier** fields are configured. Carrying the example further, he creates a new incident for a user who is unable to view an email that was sent with restricted permissions. Phil creates an incident view so that he can easily work with all incidents that are created for email problems. When changes are made to an incident, he edits the incident to reflect the changes.

In another example, an end user experiences a printer problem, and she sends an email message to the help desk. Upon receipt of the message, [!INCLUDE[smshort12](../Token/smshort12_md.md)] automatically creates an incident from the message. Phil investigates the problem, in part, by viewing the service. After the underlying problem has been solved, he resolves and closes the incident.

At Woodgrove Bank, connectors are configured in such a way that [!INCLUDE[smshort12](../Token/smshort12_md.md)] imports configuration items and alerts from, so that some new incidents are created automatically. Phil reviews the automatically created incidents for accuracy.

### Troubleshooting Incidents
In the scenario that encompasses troubleshooting incidents, Phil is conducting an initial investigation of the problem that Joe is experiencing. Phil suspects that the root cause of the problem is that Microsoft Exchange Server 2010 Service Pack 1 \(SP1\) needs to be applied to Joe’s Exchange server. However, there are other Exchange servers at Woodgrove Bank that probably also need to be updated. Phil starts his investigation by viewing the service that Garret created for the Exchange service. When any incidents affect a service component, that component is marked with an orange icon resembling a square containing an exclamation point. When a change request affects a service component, the component is marked with a special blue icon resembling a square containing a right\-pointing arrow. Phil uses the map view on the **Service Components** tab to view configuration items and view incidents associated with them. Then, he opens other configuration items and adds them to the open incident.

To further troubleshoot, Phil wants to ping a remote computer that is exhibiting problems. He can use tasks that are part of the [!INCLUDE[smcons](../Token/smcons_md.md)] instead of having to use various other tools.

### Managing Problems
In the scenario that encompasses problem management, Phil has created a change request asking the Exchange Administrators group to apply a service pack that is expected to resolve the problem. When a root cause is found and mitigated or resolved, the change request is completed and Phil is notified. He then uses the prescribed procedures to resolve a problem and automatically resolve incidents associated with the problem.

## See Also
[Managing Incidents and Problems in Service Manager](../Topic/Managing-Incidents-and-Problems-in-Service-Manager.md)

