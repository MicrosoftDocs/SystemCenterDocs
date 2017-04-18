---
title: Dashboards in Operations Manager
description: This article provides an overview of dashboards in Operations Manager to visualize operational data from monitored services and their components.  
author: mgoedtel
ms.author: magoedte
ms.manager: cfreeman
ms.date: 12/05/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Dashboards in Operations Manager

>Applies To: System Center 2016 - Operations Manager

A dashboard has a particular layout, which specifies the arrangement of the cells that actually host content.  Each cell in a dashboard can contain a single widget.  A widget accesses a particular set of data or performs a particular function and presents its information in the dashboard.  Each widget provides a specific set of customizations that you can modify according to your particular requirements.  Depending on the Dashboard Layout that you select, the dashboard may have a fixed set of widgets or may allow you to define a number of configuration of cells that can each contain a widget of your choice. 

Dashboards in Operations Manager deliver the following benefits:
 
* A dashboard is defined and shared in a management pack.  
* Authoring a dashboard is a simple process for an Operations Manager user.  A new dashboard can be created or an existing dashboard modified in both the Operations console and the Web console with the **New Dashboard and Widget** wizard.  However, if the default dashboard templates do not meet your requirements, you can [author custom dashboards](http://social.technet.microsoft.com/wiki/contents/articles/24639.aspx) and create [custom widgets](http://social.technet.microsoft.com/wiki/contents/articles/24641.operations-manager-management-pack-authoring-custom-widgets.aspx) with Visual Studio using the [Visual Studio Authoring Extensions](https://www.microsoft.com/download/details.aspx?id=30169).   
* Once created, a dashboard is available from the Operations console, the Web console and the SharePoint Web Part.   

## Dashboard templates

The first thing that you must specify when you create a dashboard is its template, which will define the widgets that will be included in the dashboard and their layout.  You cannot change the dashboard's template once it has been created.  The following sections provide details on the available templates.  Additional templates may be provided with subsequent versions of Operations Manager or from third parties.

### Service Level dashboard

A Service Level Dashboard displays information on one or more Service Level Agreements and their included Service Level Objectives.  You cannot configure the individual components but can edit the configuration of the dashboard to define the SLAs and time period to include.

- Service Levels component that lists the SLAs that you selected for the dashboard.  
- Service Level Objectives component which lists the SLOs for the SLA that is selected in the Service Level cell.  
- Service Level Details component that displays a speedometer visualization for the current measure of the selected SLO and a line chart showing the history of the measure. 

### Summary dashboard

A Summary Dashboard includes a fixed set of widgets displaying a combination of state, performance, and alert information.  The widgets are independent of on another and do not display information based on the objects selected in another widget.   You do not provide any configuration when you create the dashboard other than the name but instead configure each widget independently after the dashboard is created.
Summary Dashboards include the following widgets.  

- Object by Performance Widget (Top N)   
- Performance Widget (Performance) 
- State Widget (State) 
- Alert Widget (Alert) 

### Object State 

An Object State dashboard includes multiple widgets showing information about a particular object or group.  You cannot configure the individual widgets but can edit the configuration of the dashboard to define the target object or group that all the widgets will include in addition to the criteria for included alerts.  

Object State dashboards include the following widgets.  

- Object Health Widget (Health) showing the monitors for the target object or group.  If a group is selected only monitors targeted at the group itself are included, not the monitors of the group's members.  
- State Tiles Widget (Host) showing the health state and open alert count for the target object's host.  Note that if you selected an unhosted target such as a group or a distributed application for the dashboard, this widget will be empty.  
- State Widget (Contained objects) showing the health state of any objects contained by the target.  If the target is a group, then this will be the members of the group.  If the target has no contained objects, then this widget will be empty.   
Instance Details Widget (Object Details) that displays the details of the target object or group.  
- Alert Widget (Alerts) showing the active alerts for the target and any of its contained objects.  If the target is a group, then alerts from the members of the group are included.  You set the criteria for which alerts are included in the configuration for the dashboard itself instead of for this individual widget. 

### Column Layout

A Column Layout is an empty dashboard that allows you to set your own layout and add and configure your own set of widgets.  When you create the dashboard, you specify the number of columns that it will have.  The dashboard will start with one cell in each column.  You can add additional cells by clicking the gear icon at the top right of the dashboard and selecting Add Cell.

### Grid Layout

A Grid Layout is an empty dashboard that allows you to set your own layout and add and configure your own set of widgets.  When you create the dashboard, you specify the number of cells that it will have and select a layout for the cells.  You can change the layout of the cells after the dashboard has been created, but you can't change the number of cells.

## Dashboard widgets

The following table describes each dashboard widget and where they pull their information from.  

Widget | Description | Data Source | Aggregated Data |
-------|-------------|-------------|-----------------|
**Performance Widgets** ||||
Object by Performance | Displays a list of objects sorted according to the value of a particular performance counter. An average is calculated from the collected data for each object, and then that average value is used for the ranking. | Data Warehouse DB | Yes|
Performance Chart | Displays a line chart and a table with a list of objects and their current health state. | Data Warehouse DB | Yes|
**Alert Widgets** ||||
Alert List | Displays a table with alerts related to an object or group of objects and that match a specified criteria.| Operational DB | No|
Contextual Alert | Displays a table with alerts related to an object selected in another control in the dashboard and that match a specified criteria. | Operational DB | No|
**Object Widgets** ||||
Instance Details | Displays the health and the values of all properties of a specific object.  | Operational DB | N/A|
Contextual Health | Displays a table that includes monitors directly targeted at an object selected in another control in the dashboard and that match a specified criteria. | Operational DB | No|
Details | Displays the health and the values of all properties of an object selected in another control in the dashboard. | Operational DB | N/A|
Object Detail Tiles | Displays the following set of tiles for an object or the members of a group.<br>- Summary tile showing the health and number of alerts for the object that match a criteria.<br>- SLA tiles for each Service Level Agreements that the object is included in.<br>- Performance tiles for one or more performance counters associated with the object or members of the group.| Operational DB | N/A|
Object Health | Displays a table with a list of monitors for the selected object and its contained objects. | Operational DB | No|
State | Displays a table with a list of objects with their properties and current health state. | Operational DB | No |
State Tiles | Displays a summary tile showing the health and number of alerts for the object that match a criteria. | Operational DB | No|
**PowerShell Widgets** ||||
PowerShell Grid | Displays the results of a Windows PowerShell script in a grid. | N/A | N/A|
PowerShell Web Browser | Displays the output of a web page retrieved by a PowerShell script.| N/A | N/A|
**SLA Widgets** ||||
Object SLA | Graphically displays the last measured value each Service Level Objective in one ore more Service Level Agreements. |Data Warehouse DB | N/A|
SLA | Graphically displays the last measured value of each Service Level Objective in one more Service Level Agreements. | Data Warehouse DB | N/A|
SLA Tiles | Displays an SLA tile showing the last Service Level Objective value for the object. If there are multiple Service Level Objectives, then the tile cycles through the different values. | Data Warehouse DB | N/A|
**Miscellaneous Widgets** ||||
Topology | Displays an icon for one or more objects on a selected image. | Operations DB | N/A|
Web Browser | Displays a web, optionally sending the ID of the management group, the ID of an object selected in another widget in the dashboard, and the ID of an alert selected in another widget in the dashboard.  This allows you to create a web page that could use the Operations Manager SDK to retrieve information or perform some other action dynamically in response to a user selection in the dashboard. | Operational DB | N/A|

For additional details of each widget and the configurable properties available, please see [Operations Manager Dashboard Widgets](http://social.technet.microsoft.com/wiki/contents/articles/24133.operations-manager-dashboard-widgets.aspx) from the Management Pack Authoring Guide.   

## Next steps

- To understand how to create your own custom views and dashboards in Operations Manager,  as well as how to scope them, see [Creating and Scoping Views in Operations Manager](manage-console-scope-views.md).  