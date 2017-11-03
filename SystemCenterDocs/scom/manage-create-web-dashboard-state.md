---
ms.assetid: 
title:  How create a dashboard with the State widget in the Web console
description: This article describes how to create a new HTML5 dashboards in System Center Operations Manager with the Health State widget.  
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 10/30/2017
ms.custom: na
ms.prod: system-center-2016
monikerRange: 'sc-om-1711'
ms.technology: operations-manager
ms.topic: article
---

# How create a dashboard with the State widget in the Web console
In System Center Operations Manager, the Web console provides a monitoring interface for a management group that can be opened on any computer using any browser that has connectivity to the Web console server. The following steps describe how to create a dashboard in the new HTML5 web console with the Health State widget.

## Add widget to dashboard

1. Open a web browser on any computer and enter `http://<web host>/OperationsManager`, where *web host* is the name of the computer hosting the web console. 
2. From the left pane in the Web console, click **+ New dashboard**.<br><br> ![Select New Dashboard in Web console](./media/create-web-dashboard-alerts/web-console-new-dashboard-01.png)<br>
3. On the **Create New Dashboard** page, provide a name and description for the dashboard you want to create.<br><br> ![Specify name and description for new dashboard](./media/create-web-dashboard-alerts/web-console-new-dashboard-02.png)<br> 
4. You can save the dashboard in an existing unsealed management pack by selecting the management pack from the **Management Pack** drop-down list or you can save the dashboard by creating a new management pack by clicking **New** next to the **Management Pack** drop-down list and provide a name, description and optionally a version number. <br><br>  ![Specify name and description for new MP](./media/create-web-dashboard-alerts/web-console-new-dashboard-03.png)<br> 
5. When you have completed specifying where to save the new dashboard to, click **OK**.
6. Click **Save** after providing a name and description for the new dashboard. 
7. On the blank empty dashboard, you see the dashboard name, **Add Widget**, **Edit Dashboard**, **Delete dashboard** and **View in fullscreen** options on the top of the page.<br><br> ![New dashboard canvas](./media/create-web-dashboard-alerts/web-console-new-dashboard-04.png)<br> 
8. Select **State Widget** from the **Select Widget** drop-down list.
9. In the State widget pane, select scope for the widget by clicking either **Groups** or **Class**.<br><br> ![Select scope for State widget](./media/create-web-dashboard-state/web-console-new-dashboard-state.png)<br>  For either option selected, you can search by keyword in the list.  As you begin typing, the list filters based on your input.  You can select an individual group or class or multiple from the returned results.
11. Set the criteria to identify the health state to display.  To narrow the results, you can filter by selecting the following:
   * By all health states or a specific state
   * Display all objects or only those in maintenance mode  

    Data matching the defined criteria will only be displayed in the widget.<br><br> ![Set criteria for Alert widget](./media/create-web-dashboard-state/web-console-new-dashboard-state-02.png)<br>
  
12. Select **Display** to choose the columns to be displayed in the dashboard.  You can select or search for the columns from the drop-down list.  
13. Complete the configuration by providing a **Name**, **Description** and **Widget reefresh interval** (default interval is 5 minutes) for the widget.  Click **Save Widget** to save your new dashboard.  

After the widget has been created, it displays health state of the objects based on the scope and criteria defined. You see the name of the state widget along with the number of objects in the header of the widget. Objects can also be filtered in the widget by searching for a keyword in the filter box.<br><br> ![Completed example of State widget in dashboard](./media/create-web-dashboard-state/web-console-new-dashboard-state-03.png)

## Actions on State widget
For one or more monitored objects selected in the widget, you can perform such actions as:

1. Export the alerts to Excel for further analysis 
2. Modify how the alerts are presented by included or excluding columns or how to group alerts, customized to your personal needs

1. Hover your mouse over the widget and click on the ellipse **...** on the top right corner of the widget.  This will display actions available for the widget.
   * Select **Export to Excel** to export the alert data to an Excel file.
   * Select **Personalize** to change your selection of columns to be displayed or to group alerts.  Click **Save personalization** when you have completed making your changes.  

