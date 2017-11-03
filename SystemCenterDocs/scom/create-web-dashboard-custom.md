---
ms.assetid: 
title:  How create a dashboard with the Custom widget in the Web console 
description: This article describes how to create a new HTML5 dashboards in System Center Operations Manager with the Custom widget.  
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

# How create a dashboard with the Custom widget in the Web console
In System Center Operations Manager, the Web console provides a monitoring interface for a management group that can be opened on any computer using any browser that has connectivity to the Web console server. The following steps describe how to add a Custom widget to a  dashboard in the new HTML5 Web console.  It executes the HTML code specified and visualizes the desired output. 

## Add widget to dashboard

1. Open a web browser on any computer and enter `http://<web host>/OperationsManager`, where *web host* is the name of the computer hosting the web console. 
2. From the left pane in the Web console, click **+ New dashboard**.<br><br> ![Select New Dashboard in Web console](./media/create-web-dashboard-alerts/web-console-new-dashboard-01.png)<br>
3. On the **Create New Dashboard** page, provide a name and description for the dashboard you want to create.<br><br> ![Specify name and description for new dashboard](./media/create-web-dashboard-alerts/web-console-new-dashboard-02.png)<br> 
4. You can save the dashboard in an existing unsealed management pack by selecting the management pack from the **Management Pack** drop-down list or you can save the dashboard by creating a new management pack by clicking **New** next to the **Management Pack** drop-down list and provide a name, description and optionally a version number. <br><br>  ![Specify name and description for new MP](./media/create-web-dashboard-alerts/web-console-new-dashboard-03.png)<br> 
5. When you have completed specifying where to save the new dashboard to, click **OK**.
6. Click **Save** after providing a name and description for the new dashboard. 
7. On the blank empty dashboard, you see the dashboard name, **Add Widget**, **Edit Dashboard**, **Delete dashboard** and **View in fullscreen** options on the top of the page.<br><br> ![New dashboard canvas](./media/create-web-dashboard-alerts/web-console-new-dashboard-04.png)<br> 
8. Select **Custom Widget** from the **Select Widget** drop-down list.
9. In the Custom widget pane, select criteria for the widget adding the HTML code that needs to be visualized.<br><br> ![Configure the Custom widget for dashboard](./media/create-web-dashboard-custom/web-console-new-dashboard-custom.png)<br>
10. Complete the configuration by providing a **Name**, **Description** and **Widget reefresh interval** (default interval is 5 minutes) for the widget.  Click **Save Widget** to save your new dashboard.  

After the widget has been created, it displays the output of the HTLM code.<br><br> ![Completed example of Tile widget in dashboard](./media/create-web-dashboard-custom/web-console-new-dashboard-custom-01.png)

 