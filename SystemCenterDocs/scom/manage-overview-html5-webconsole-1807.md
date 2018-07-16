---
ms.assetid: 
title:  Overview of HTML5 Web console and dashboards 
description: This article provides an overview of the new HTML5 Web console and dashboards in System Center Operations Manager.  
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 07/09/2018
ms.custom: na
ms.prod: system-center-2016
monikerRange: 'sc-om-1807'
ms.technology: operations-manager
ms.topic: article
---

# Overview of HTML5 Web console and dashboards 

This topic applies to System Center Operations Manager version 1807.

System Center Operations Manager now delivers HTML5 based dashboards, which enhance the authoring and visualization experiences for Web console users. With these improvements you are able to visualize operational data with richer data visualizations, faster performance, and drill-down.  You can access these dashboards from multiple browsers (such as Chrome) and are no longer dependent on Silverlight.

## Supported scenarios
You can take advantage of the following HTML5 dashboard capabilities:

1.	You can create HTML 5 dashboards from multiple browsers without a dependency on Silverlight.  
2.	User can visualize their environment data in HTML 5 dashboards with 
   1. Alert widget
   2. State widget
   3. Performance widget (also works like the Object by performance widget)  
   4. Topology widget
   5. Tile widget
   6. Custom widget
   7. PowerShell widget
3.	Perform create, edit and delete operations on the widgets  
4.	Create or edit these widgets and scope by objects or groups 
5.	Add custom image for topology widgets and place the health of object on top of the image 
6.	Create any number of widgets in the dashboard without any predefined layout selection 
10.	Easily move, reposition and resize the widgets in the dashboard 
11.	View the dashboards in full screen without the monitoring tree view
12.	Define a custom refresh interval rate for each of the dashboard widgets 
14.	Visualize the following dashboards:
   1. Web Application Status
   2. Management Group Health
   3. Management Group Health Trend 
   4. UNIX/Linux Computer Summary
   5. Network Summary Dashboard 
15.	You can sign out from your current web console session
16. Dashboards can be saved in custom management packs and exported 
17.	The following drill-down capabilities are available within the dashboards:
   1. Analyze the issue by visualizing the relevant data for a monitoring object, individual alert, rule, monitor, and class.
   2. Navigate from one object to another 
   3. View the tasks associated with selected object 
18.	 Explore the actions enabled in a widget:
   1. Actions with alert widget - Set resolution state on a single alert or select multiple alerts from within the widget
   2. Export the data visible in the widget to Excel for further analysis
   3. Personalize by adding or removing columns to visualize and group alerts
19. Explore actions with state widget:
   1. Export the data visible in the widget to Excel for further analysis
   2. Personalize by adding or removing columns to visualize and group objects
20. Explore actions with Topology widget: 
   1. Edit state indicator layout and place object health icons anywhere on image 
21. Explore actions with Performance widget:
   1. Set vertical axis and specify the minimum and maximum values of vertical axis
   2. Export to Excel the legend data to Excel for further analysis. 
   3. Personalize by adding or removing columns for the legend, and enable or disable visualized objects by performance
22. Explore results of a Windows PowerShell script.  
23.	You can delete HTML5 dashboards from the Web console and create dashboards or views to My workspace.
24.	The IIS web server hosting the Web console role can be setup with network authentication mode and users can access the Web console using network authentication
25.	You can provide feedback on HTML5 dashboards from within the Web console.

## Supported browsers
System Center Operations Manager version 1807 Web console supports Microsoft Edge, Google Chrome, Mozilla Firefox and Internet Explorer.