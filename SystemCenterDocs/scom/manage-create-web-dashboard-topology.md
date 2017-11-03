---
ms.assetid: 
title:  How create a dashboard with the Topology widget in the Web console
description: This article describes how to create a new HTML5 dashboards in System Center Operations Manager with the Topology widget.  
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

# How create a dashboard with the Topology widget in the Web console
In System Center Operations Manager, the Web console provides a monitoring interface for a management group that can be opened on any computer using any browser that has connectivity to the Web console server. The following steps describe how to create dashboard in the new HTML5 Web console with the Topology widget.

## Add widget to dashboard

1. Open a web browser on any computer and enter `http://<web host>/OperationsManager`, where *web host* is the name of the computer hosting the web console. 
2. From the left pane in the Web console, click **+ New dashboard**.<br><br> ![Select New Dashboard in Web console](./media/create-web-dashboard-alerts/web-console-new-dashboard-01.png)<br>
3. On the **Create New Dashboard** page, provide a name and description for the dashboard you want to create.<br><br> ![Specify name and description for new dashboard](./media/create-web-dashboard-alerts/web-console-new-dashboard-02.png)<br> 
4. You can save the dashboard in an existing unsealed management pack by selecting the management pack from the **Management Pack** drop-down list or you can save the dashboard by creating a new management pack by clicking **New** next to the **Management Pack** drop-down list and provide a name, description and optionally a version number. <br><br>  ![Specify name and description for new MP](./media/create-web-dashboard-alerts/web-console-new-dashboard-03.png)<br> 
5. When you have completed specifying where to save the new dashboard to, click **OK**.
6. Click **Save** after providing a name and description for the new dashboard. 
7. On the blank empty dashboard, you see the dashboard name, **Add Widget**, **Edit Dashboard**, **Delete dashboard** and **View in fullscreen** options on the top of the page.<br><br> ![New dashboard canvas](./media/create-web-dashboard-alerts/web-console-new-dashboard-04.png)<br> 
8. Select **Topology Widget** from the **Select Widget** drop-down list.
9. In the Topology widget pane, select scope for the widget by clicking either **Groups** or **Class**.<br><br> ![Select scope for Topology widget](./media/create-web-dashboard-topology/web-console-new-dashboard-topology.png)<br>  For either option selected, you can search by keyword in the list.  As you begin typing, the list filters based on your input.  You can select an individual group or class or multiple from the returned results.
11. Select **Display** to choose an image for the topology widget to display in the authoring pane.  Click **Select Image** and on the **Select Image** pane if you already added a custom image by performing these steps earlier, then select an image from the list.<br><br> ![Add custom image to Topology widget](./media/create-web-dashboard-topology/web-console-new-dashboard-topology-01.png)<br>  Otherwise, click **Add custom image** and navigate to where the file is located.<br><br> ![Select new image for Topology widget](./media/create-web-dashboard-topology/web-console-new-dashboard-topology-02.png)<br>   
12. After selecting the file, click **Open** and the image will be uploaded and presented in the **Select Image** pane.  Click **Done** to complete 
13. Complete the configuration by providing a **Name**, **Description** and **Widget reefresh interval** (default interval is 5 minutes) for the widget.  Click **Save Widget** to save your new dashboard.  

When created for the first time, the health state icons for the selected objects are displayed at the left-top section of the topology widget. These icons have to be placed manually in the appropriate position on the image by performing the following steps:

1. Click on the ellipse **…** next to the **X** on the right most side of the widget crown, which is displayed when you hover over the widget.
2. Click **Edit icons layout** action to re-position the health state icons for the selected objects on the selected image. While editing the icon layout, the health state icons will also display the object name of the specific object.
3. Once the selected object icons have been re-positioned appropriately, click **Go** under **Save icons layout** to save reconfigured positioning of the icons.

Now your topology dashboard visualizes the health of objects positioned on the selected image.<br><br> ![Completed example of Performance widget in dashboard](./media/create-web-dashboard-topology/web-console-new-dashboard-topology-03.png)

## Actions on Topology widget
For a topology diagram which includes monitored object health state in the widget, you can re-position the icons of the selected objects on the selected image.

1. Hover your mouse over the widget and click on the ellipse **...** on the top right corner of the widget.  This will display actions available for the widget. 
2. Select the **Edit state indicator layout** action.
3. In the **Edit state indicator layout** mode, the health state icons will also display the object name of the specific object.
4. After moving the object ictons to their new position on the image, click **Save** to save the updated layout.


