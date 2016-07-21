---
title: View Types in Operations Manager
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f36bccfb-e038-4a3a-9999-3195fe738bd3
author:mgoedtel
manager:cfreemanwa
---
# View Types in Operations Manager
Each view type in [!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)] displays a different aspect of monitoring data. Each view type has a different icon as shown in the following image.  
  
![Icons associated with each view type](../../om/manage/media/ViewTypesOM12.jpg "ViewTypesOM12")  
  
For more information on specific view types, see:  
  
-   [Alert View Type](../../om/manage/View-Types-in-Operations-Manager.md#bkmk_alertviewtype)  
  
-   [Event View Type](../../om/manage/View-Types-in-Operations-Manager.md#bkmk_eventviewtype)  
  
-   [State View Type](../../om/manage/View-Types-in-Operations-Manager.md#bkmk_stateviewtype)  
  
-   [Performance View Type](../../om/manage/View-Types-in-Operations-Manager.md#bkmk_performanceviewtype)  
  
-   [Diagram View Type](../../om/manage/View-Types-in-Operations-Manager.md#bkmk_diagramviewtype)  
  
-   [Task Status View Type](../../om/manage/View-Types-in-Operations-Manager.md#bkmk_taskstatusviewtype)  
  
-   [Web Page View Type](../../om/manage/View-Types-in-Operations-Manager.md#bkmk_webpageviewtype)  
  
-   [Overrides Summary View Type](../../om/manage/View-Types-in-Operations-Manager.md#bkmk_overridessummaryviewtype)  
  
-   [Dashboard View Type](../../om/manage/View-Types-in-Operations-Manager.md#bkmk_dashboardviewtype)  
  
## <a name="bkmk_alertviewtype"></a>Alert View Type  
The alert view displays alerts that meet your specific criteria, such as alert severity, resolution state, or alerts that are assigned to you. For information on creating an alert view, see [How to Create an Alert View](../../om/manage/Creating-Views-in-Operations-Manager.md#bkmk_howtocreateanalertview).  
  
![A blank Alerts view window](../../om/manage/media/Alertsview.gif "Alertsview")  
  
## <a name="bkmk_eventviewtype"></a>Event View Type  
The event view queries the event logs and displays events that are based on criteria specified in the event view properties. For information on creating an event view, see [How to Create an Event View](../../om/manage/Creating-Views-in-Operations-Manager.md#bkmk_howtocreateaneventview).  
  
![Example of Events view window](../../om/manage/media/neweventsview.gif "neweventsview")  
  
## <a name="bkmk_stateviewtype"></a>State View Type  
The state view displays relationships between components, computers, and computer groups. For information on creating a state view, see [How to Create a State View](../../om/manage/Creating-Views-in-Operations-Manager.md#bkmk_howtocreateastateview).  
  
![Example of state view of distributed application](../../om/manage/media/Stateview.gif "Stateview")  
  
## <a name="bkmk_performanceviewtype"></a>Performance View Type  
The performance view allows you to customize how you want to view performance data collected from performance objects and counters. This includes the ability to view historical and current operational data together. You must select **Show** in the Details pane to display data from a rule in the graph in the Results pane. For information on creating a performance view, see [How to Create a Performance View](../../om/manage/Creating-Views-in-Operations-Manager.md#bkmk_howtocreateaperformanceview).  
  
![Example of performance view](../../om/manage/media/Performanceview.gif "Performanceview")  
  
## <a name="bkmk_diagramviewtype"></a>Diagram View Type  
The Diagram view displays a graphical view of a set of managed objects and how they relate to one another. For information on creating a diagram view, see [How to Create a Diagram View](../../om/manage/Creating-Views-in-Operations-Manager.md#bkmk_howtocreateadiagramview).  
  
![Example of diagram view](../../om/manage/media/Diagramview.gif "Diagramview")  
  
## <a name="bkmk_taskstatusviewtype"></a>Task Status View Type  
The task status view displays tasks that meet criteria specified in the properties, such as only those tasks that apply to certain object types. For information on creating a task status view, see [How to Create a Task Status View](../../om/manage/Creating-Views-in-Operations-Manager.md#bkmk_howtocreateataskstatusview).  
  
![Selection window for task status view](../../om/manage/media/Taskstatusview.gif "Taskstatusview")  
  
> [!NOTE]  
> Users that are members of the Read\-only Operator role cannot view or run any tasks. For this reason, no tasks appear in a task status view that is opened by a Read\-only Operator.  
  
## <a name="bkmk_webpageviewtype"></a>Web Page View Type  
The Web page view displays a Web page in a separate window in the Operations console. For information on creating a Web page view, see [How to Create a Web Page View](../../om/manage/Creating-Views-in-Operations-Manager.md#bkmk_howtocreateawebpageview).  
  
![Example of web page view](../../om/manage/media/Webpageview.gif "Webpageview")  
  
## <a name="bkmk_overridessummaryviewtype"></a>Overrides Summary View Type  
You can only create an overrides summary view in My Workspace.  
  
You can view all rule and monitor overrides in the overrides summary view. The overrides summary view can be used for both sealed and unsealed management packs. You can customize this view by grouping items by multiple column headers. For information on creating an overrides summary view, see [How to Create an Overrides Summary View](../../om/manage/Creating-Views-in-Operations-Manager.md#bkmk_howtocreateanoverridessummaryview).  
  
![Example of overrides summary view](../../om/manage/media/OverridesSummaryView.gif "OverridesSummaryView")  
  
## <a name="bkmk_dashboardviewtype"></a>Dashboard View Type  
The dashboard view allows you to present multiple types of data in a single view.  
  
> [!IMPORTANT]  
> When a dashboard view uses data from the data warehouse database, operators might be able to view data that they would not otherwise have access to in views that use data from the operational database.  
  
![Sample dashboard view](../../om/manage/media/OM12_SampleDashboard.gif "OM12_SampleDashboard")  
  
For information on creating a dashboard view, see [How to Create a Dashboard View](../../om/manage/Creating-Views-in-Operations-Manager.md#bkmk_howtocreateadashboardview).  
  
## See Also  
[Using Views in Operations Manager](../../om/manage/Using-Views-in-Operations-Manager.md)  
[Creating Views in Operations Manager](../../om/manage/Creating-Views-in-Operations-Manager.md)  
[How to Personalize a View in Operations Manager](../../om/manage/How-to-Personalize-a-View-in-Operations-Manager.md)  
[Guidance for Scoping and Targeting Views](../../om/manage/Guidance-for-Scoping-and-Targeting-Views.md)  
  
