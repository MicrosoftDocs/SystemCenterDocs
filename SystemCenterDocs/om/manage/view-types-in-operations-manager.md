---
title: View Types in Operations Manager
description: This article describes the different view types available in the Operations Manager consoles.  
author: mgoedtel
ms.author: magoedte
ms.manager: cfreeman
ms.date: 11/28/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
ms.assetid: f36bccfb-e038-4a3a-9999-3195fe738bd3
---

# View types in Operations Manager

>Applies To: System Center 2016 - Operations Manager

Each view type in System Center 2016 - Operations Manager displays a different aspect of monitoring data. Each view type has a different icon as shown in the following image.  
  
![Icons associated with each view type](../media/om2016-operations-console-view-types.png)  
  
## Alert view type  

The alert view displays alerts that meet your specific criteria, such as alert severity, resolution state, or alerts that are assigned to you. For information on creating an alert view, see [How to Create an Alert View](how-to-create-and-scope-views-in-operations-manager.md#how-to-create-an-alert-view).  
  
![Example of an Alerts view](../media/om2016-operations-console-alertview.png)  
  
##Event view type  

The event view queries the event logs and displays events that are based on criteria specified in the event view properties. For information on creating an event view, see [How to Create an Event View](how-to-create-and-scope-views-in-operations-manager.md#how-to-create-an-event-view).  
  
![Example of an Events view](../media/om2016-operations-console-eventview.png)  
  
## State view type  

The state view displays relationships between components, computers, and computer groups. For information on creating a state view, see [How to Create a State View](how-to-create-and-scope-views-in-operations-manager.md#how-to-create-a-state-view).  
  
![Example of a state view of distributed application](../media/om2016-operations-console-stateview.png)  
  
## Performance view type  

The performance view allows you to customize how you want to view performance data collected from performance objects and counters. This includes the ability to view historical and current operational data together. You must select **Show** in the Details pane to display data from a rule in the graph in the Results pane. For information on creating a performance view, see [How to Create a Performance View](how-to-create-and-scope-views-in-operations-manager.md#how-to-create-a-performance-view).  
  
![Example of a performance view](../media/om2016-operations-console-performanceview.png)  
  
## Diagram view type  

The Diagram view displays a graphical view of a set of managed objects and how they relate to one another. For information on creating a diagram view, see [How to Create a Diagram View](how-to-create-and-scope-views-in-operations-manager.md#how-to-create-a-diagram-view).  
  
![Example of a diagram view](../media/om2016-operations-console-diagramview.png)  
  
## Task status view type  

The task status view displays tasks that meet criteria specified in the properties, such as only those tasks that apply to certain object types. For information on creating a task status view, see [How to Create a Task Status View](how-to-create-and-scope-views-in-operations-manager.md#how-to-create-a-task-status-view).  
  
![Selection window for task status view](../media/om2016-operations-console-taskstatus.png)  
  
> [!NOTE]  
> Users that are members of the Read-only Operator role cannot view or run any tasks. For this reason, no tasks appear in a task status view that is opened by a Read-only Operator.  
  
## Web page view type  

The Web page view displays a Web page in a separate window in the Operations console. For information on creating a Web page view, see [How to Create a Web Page View](how-to-create-and-scope-views-in-operations-manager.md#how-to-create-a-web-page-view).  
  
![Example of web page view](../media/om2016-operations-console-webpageview.png)  
  
##Overrides summary view type  

You can only create an overrides summary view in My Workspace.  
  
You can view all rule and monitor overrides in the overrides summary view. The overrides summary view can be used for both sealed and unsealed management packs. You can customize this view by grouping items by multiple column headers. For information on creating an overrides summary view, see [How to Create an Overrides Summary View](how-to-create-and-scope-views-in-operations-manager.md#how-to-create-an-overrides-summary-view).  
  
![Example of overrides summary view](../media/om2016-operations-console-overridesummaryview.png)  
  
## Dashboard view type  

The dashboard view allows you to present multiple types of data in a single view.  
  
> [!IMPORTANT]  
> When a dashboard view uses data from the data warehouse database, operators might be able to view data that they would not otherwise have access to in views that use data from the operational database.  
  
![Sample dashboard view](../media/om2016-operations-console-dashboardview.png)  
  
For information on creating a dashboard view, see [How to Create a Dashboard View](how-to-create-and-scope-views-in-operations-manager.md#how-to-create-a-dashboard-view).  
  
## Next steps
  
- You can use views and dashboards to visualize operational data from different perspectives to make meaningful decisions.  To understand how to do this, see [Using Views and Dashboards in Operations Manager](using-views-and-dashboards-in-operations-manager.md).  

- To understand how to create your own custom views and dashboards in Operations Manager, see [Creating and scoping views in Operations Manager](how-to-create-and-scope-views-in-operations-manager.md). 

- Views included in sealed management packs can be modified to include other monitored object properties.  To customize a view, see [How to personalize a View in Operations Manager](how-to-personalize-a-view-in-operations-manager.md).  

  
