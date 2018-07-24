---
ms.assetid: 
title:  Overview of HTML5 Web console and dashboards 
description: This article provides an overview of the new HTML5 Web console and dashboards in System Center Operations Manager.  
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 07/18/2018
ms.custom: na
ms.prod: system-center-2016
monikerRange: '>sc-om-2016'
ms.technology: operations-manager
ms.topic: article
---

# Overview of HTML5 Web console and dashboards 

System Center Operations Manager now delivers HTML5 based dashboards, which enhance the authoring and visualization experiences for Web console users. With these improvements you are able to visualize operational data with richer data visualizations, faster performance, and drill-down.  You can access these dashboards from multiple browsers (such as Chrome) and are no longer dependent on Silverlight.

## Supported scenarios
You can take advantage of the following HTML5 dashboard capabilities:

1.	Create HTML 5 dashboards from multiple browsers without a dependency on Silverlight.  

2.	Visualize monitoring data in HTML 5 dashboards with: 
   1. [Alert widget](manage-create-web-dashboard-alerts.md)
   2. [State widget](manage-create-web-dashboard-state.md)
   3. [Performance widget (also works like the Object by performance widget)](manage-create-web-dashboard-perf.md)  
   4. [Topology widget](manage-create-web-dashboard-topology.md)
   5. [Tile widget](manage-create-web-dashboard-tile.md)
   6. [Custom widget](manage-create-web-dashboard-custom.md)
   7. In version 1807, we introduce the [PowerShell widget](manage-create-web-dashboard-posh.md)

3.	Perform create, edit and delete operations on the widgets  

4.	Create or edit these widgets and scope by objects or groups 

5.	Add custom image for topology widgets and place the health of object on top of the image 

6.	Create any number of widgets in the dashboard without any predefined layout selection 

7.	Easily move, reposition and resize the widgets in the dashboard 

8.	View the dashboards in full screen without the monitoring tree view

9.	Define a custom refresh interval rate for each of the dashboard widgets 

10.	Visualize the following dashboards:

   1. Web Application Status
   2. Management Group Health
   3. Management Group Health Trend 
   4. UNIX/Linux Computer Summary
   5. Network Summary Dashboard 
   6. In version 1807, you can view Network Node and Network Interface Dashboard for Network Node/interface from the Monitored Objects page

11.	In version 1807, you can visualize the effective configuration of rules and monitors for a monitored object from the **Monitored objects** drill down page

12.	You can sign out from your current web console session

13. Dashboards can be saved in custom management packs and exported 

14.	The following drill-down capabilities are available within the dashboards:

   1. Analyze the issue by visualizing the relevant data for a monitored object, individual alert, rule, monitor, and class.
   2. Navigate from one object to another 
   3. View the tasks associated with selected object 

15.	 Explore the actions enabled in a widget:

   1. Actions with alert widget - Set resolution state on a single alert or select multiple alerts from within the widget.  View alert details delivering the same experience provided in the Operations console when viewing an alert - modify the alert resolution state and drill down to the monitoring object details page by selecting the alert source.
   2. Export the data visible in the widget to Excel for further analysis
   3. Personalize by adding or removing columns to visualize and group alerts

16. Explore actions with state widget:

   1. Export the data visible in the widget to Excel for further analysis
   2. Personalize by adding or removing columns to visualize and group objects

17. Explore actions with Topology widget:
 
   1. Edit state indicator layout and place object health icons anywhere on image 

18. Explore actions with Performance widget:

   1. Set vertical axis and specify the minimum and maximum values of vertical axis
   2. Export to Excel the legend data to Excel for further analysis. 
   3. Personalize by adding or removing columns for the legend, and enable or disable visualized objects by performance

19. Explore actions with PowerShell widget:

   1. Export to Excel the legend data to Excel for further analysis.

20.	Delete HTML5 dashboards from the Web console and in version 1807, you can create dashboards or views to My workspace.  In version 1801, you add dashboards or views to My Workspace from the monitoring tree.

21.	The IIS web server hosting the Web console role can be setup with network authentication mode and users can access the Web console using network authentication

22.	You can provide feedback on HTML5 dashboards from within the Web console.

## Supported browsers
System Center Operations Manager version 1807 Web console supports Microsoft Edge, Google Chrome, Mozilla Firefox and Internet Explorer.  

>[!NOTE]
>Internet Explorer compatibility mode is not supported.   
> 