---
ms.assetid: 
title:  How create a dashboard with the Alert widget in the Web console
description: This article describes how to create a new HTML5 dashboards in System Center Operations Manager with the Alert widget.  
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

# How create a dashboard with the Alert widget in the Web console
In System Center Operations Manager, the Web console provides a monitoring interface for a management group that can be opened on any computer using any browser that has connectivity to the Web console server. The following steps describe how to create a dashboard in the new HTML5 web console with the Alert widget.

## Add widget to dashboard

1. Open a web browser on any computer and enter `http://<web host>/OperationsManager`, where *web host* is the name of the computer hosting the web console. 
2. From the left pane in the Web console, click **+ New dashboard**.<br><br> ![Select New Dashboard in Web console](./media/create-web-dashboard-alerts/web-console-new-dashboard-01.png)<br>
3. On the **Create New Dashboard** page, provide a name and description for the dashboard you want to create.<br><br> ![Specify name and description for new dashboard](./media/create-web-dashboard-alerts/web-console-new-dashboard-02.png)<br> 
4. You can save the dashboard in an existing unsealed management pack by selecting the management pack from the **Management Pack** drop-down list or you can save the dashboard by creating a new management pack by clicking **New** next to the **Management Pack** drop-down list and provide a name, description and optionally a version number. <br><br>  ![Specify name and description for new MP](./media/create-web-dashboard-alerts/web-console-new-dashboard-03.png)<br> 
5. When you have completed specifying where to save the new dashboard to, click **OK**.
6. Click **Save** after providing a name and description for the new dashboard. 
7. On the blank empty dashboard, you see the dashboard name, **Add Widget**, **Edit Dashboard**, **Delete dashboard** and **View in fullscreen** options on the top of the page.<br><br> ![New dashboard canvas](./media/create-web-dashboard-alerts/web-console-new-dashboard-04.png)<br> 
8. Select **Alert Widget** from the **Select Widget** drop-down list.
9. In the Alert widget pane, select scope for the alert widget by clicking either **Groups** or **Objects**.  For either option selected, you can search by keyword in the list.  As you begin typing, the list filters based on your input.  You can select an individual group or object or multiple from the returned results. 
10. A result set for the desired search query will be returned, select the scope from the returned results.<br><br> ![Set scope for Alert widget](./media/create-web-dashboard-alerts/web-console-new-dashboard-05.png)<br>
11. Set the criteria to identify the alerts to display.  To narrow the results, you can filter by selecting the following:
   * Severity
   * Priority
   * Resolution state
   * Alert age  
   
    Data matching the defined criteria will only be displayed in the widget.<br><br> ![Set criteria for Alert widget](./media/create-web-dashboard-alerts/web-console-new-dashboard-alert.png)<br>
  
12. Select **Display** to choose the columns to be displayed in the dashboard.  You can select or search for the columns from the drop-down list.  
13. Complete the configuration by providing a **Name**, **Description** and **Widget reefresh interval** (default interval is 5 minutes) for the widget.  Click **Save Widget** to save your new dashboard.  

After the widget has been created, it displays alerts based on the scope and criteria defined. You see the name of the alert widget along with the number of alerts in the header of widget. Alerts can also be filtered in the widget by searching for a keyword in the filter box.<br><br> ![Completed example of Alert widget in dashboard](./media/create-web-dashboard-alerts/web-console-new-dashboard-07.png)

## Actions on Alert widget
For one or more alerts selected in the widget, you can perform such actions as:

1. Change resolution state 
2. Export the alerts to Excel for further analysis 
3. Modify how the alerts are presented by included or excluding columns or how to group alerts, customized to your personal needs 

1. Hover your mouse over the widget and click on the ellipse **...** on the top right corner of the widget.  This will display actions available for the widget.
   * Select **Set resolution state** and select one or multiple alerts by clicking on the checkbox in the first column on the left, for each alert resolution state you are going to change. Select the resolution state from the drop-down list and click **Save**.
   * Select **Export to Excel** to export the alert data to an Excel file.
   * Select **Personalize** to change your selection of columns to be displayed or to group alerts.  Click **Save personalization** when you have completed making your changes.  
