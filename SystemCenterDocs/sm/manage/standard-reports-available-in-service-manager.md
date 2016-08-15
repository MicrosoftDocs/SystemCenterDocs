---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bandersmsft
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  Standard Reports Available in Service Manager
ms.technology:  service-manager
ms.assetid:  147b3945-13f8-40fd-851a-5df9e79b08a9
---

# Standard Reports Available in Service Manager

>Applies To: System Center 2016 Technical Preview - Service Manager

The following reports are available in System Center 2016 Technical Preview - Service Manager.

|Report area|Report name|Description|
|---------------|---------------|---------------|
|Activity management|List of Activities|Provides a list of activities within a certain time frame that meet the specified criteria. The data in the report includes the type of activity, the current status, and the priority.|
|Activity management|List of Manual Activities|Provides a list of all the manual activities within a certain time frame that also meet the specified criteria. The data in the report includes the current status, stage, priority, and user to whom the activity is assigned.|
|Activity management|List of Review Activities|Provides a list of all the review activities within a certain time frame that meet the specified criteria. The data in this report includes the current status, stage, approval condition, and approval threshold.|
|Activity management|Manual Activity Detail|Provides detailed information about a specific manual activity, including the title, description, status, and affected customers.|
|Activity management|Review Activity Detail|Provides detailed information about a specific review activity, including the title, description, status, reviewers, and approval condition.|
|Activity management|Activity Distribution|Provides the number of activities during a specified time frame. The data in this report includes the activity status, type, and stage. You can filter the data by status, stage, or type.|
|Change management|Change Management KPI Trend|Provides the number and current state (in progress, completed, failed, or canceled) of change requests during a specified time frame. You can filter the data returned in this report by day, week, month, quarter, or year.|
|Change management|List of Change Requests|Provides a list of change requests within a certain time frame. The data in this report includes the current status, category, and user to whom the request is assigned.|
|Change management|Change Request Detail|Provides detailed information about a specific change request, including the title, description, status, change creator, and template.|
|Configuration management|Computer Detail|Provides detailed configuration information for a specific computer.|
|Configuration management|Computer Inventory|Provides a list of computers available in the management group. **Note:** The Computer Inventory report might contain more total computers than actually exist in a single Service Manager management group. This situation is uncommon but possible when you have more than one management group share a data warehouse. More specifically, if you manually create a computer in one management group and manually create a computer with the same name in another management group, the data warehouse cannot reconcile the two manually-created computers. Because this situation does not occur when computers are discovered by a connector, you can avoid multiple computers appearing in the report by deleting the manually-created computer configuration item and then discover it by using a connector.|
|Configuration Management|Software Update Compliance Trend|Provides detailed information for software update compliance. You can filter this data by classification or category, and by day, week, month, quarter, or year.|
|Incident management|Incident Analyst|Provides key performance metrics for a specified analyst. The data in this report includes the number of incidents assigned to the analyst, the number of incidents resolved by the analyst, the number of incidents worked on by the analyst, and any labor logged against an incident.|
|Incident management|Incident Details|Provides detailed information for a specific incident, including the title, description, classification, affected services, affected configuration items, and related activities.|
|Incident management|Incident KPI Trend|Provides the number of incidents, including the number of incidents past their targeted resolution time, the number of escalated incidents, the average time to resolution, the labor minutes per incident, and the size of the incident backlog. You can filter this data by classification or category, and by day, week, month, quarter, or year.|
|Incident management|Incident Resolution|Provides the number of incidents, including the number of incidents past their targeted resolution time and the average time to resolution. You can filter the data by day, week, month, quarter or year.|
|Incident management|List of Incidents|Provides a list of all incidents within a certain time frame. The data in this report includes the users to whom incidents are assigned, when the incidents were created, and the current status of the incidents.|
|Problem management|Configuration Items (CIs) with Most Incidents|Provides a list of the configuration items that have at least the number of incidents associated with them, as specified by the value you enter for **Incidents per Configuration Item** during the specified time frame. This report also includes the number of change requests and problems associated with the specific configuration item.|
|Problem management|List of Problems|Provides a list of all problems within a certain time frame.|
|Problem management|Problem detail|Provides detailed information for a specific problem.|
|Release management|List of Release Records|Provides a list of all release records within a certain time frame.|
|Release management|Release Record Detail|Provides detailed information for a specific release record.|
|Service Management|Service KPI Trend|Provides key metrics across services, groups and collections for Service Manager, Operations Manager, and Configuration Manager. This report enables trending and flexible grouping.|
|Service Management|Service Summary|Provides a scorecard-like report that includes a comprehensive view of the health of a service, including period-over-period analytic capabilities.|

## See Also
[Using and Managing Standard Reports](Using-and-Managing-Standard-Reports.md)



