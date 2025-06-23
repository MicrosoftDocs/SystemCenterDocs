---
ms.assetid:
title: Create a dashboard with the Performance widget in the Web console
description: This article describes how to create a new HTML5 dashboard in System Center Operations Manager with the Performance widget.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.custom: UpdateFrequency2, engagement-fy24
ms.service: system-center
monikerRange: '>sc-om-2016'
ms.subservice: operations-manager
ms.topic: article
---

# Create a dashboard with the Performance widget in the Web console



In System Center Operations Manager version 2019 and later, the Web console provides a monitoring interface for a management group that can be opened on any computer using any browser that has connectivity to the Web console server. The following steps describe how to create a dashboard in the new HTML5 Web console with the Performance widget.

## Add widget to dashboard

1. Open a web browser on any computer and enter `http://<web host>/OperationsManager`, where *web host* is the name of the computer hosting the web console.
2. From the left pane in the Web console, select **+ New dashboard**.

    :::image type="content" source="./media/create-web-dashboard-alerts/web-console-new-dashboard-01-inline.png" alt-text="Screenshot showing select New Dashboard in Web console." lightbox="./media/create-web-dashboard-alerts/web-console-new-dashboard-01-expanded.png":::

3. On the **Create New Dashboard** page, provide a name and description for the dashboard you want to create.

    :::image type="content" source="./media/create-web-dashboard-alerts/web-console-new-dashboard-02-inline.png" alt-text="Screenshot showing specify name and description for new dashboard." lightbox="./media/create-web-dashboard-alerts/web-console-new-dashboard-02-expanded.png":::

4. You can save the dashboard in an existing unsealed management pack by selecting the management pack from the **Management Pack** dropdown list or you can save the dashboard by creating a new management pack by selecting **New** next to the **Management Pack** dropdown list and provide a name, description, and optionally a version number.

    ![Screenshot showing specify name and description for new MP.](./media/create-web-dashboard-alerts/web-console-new-dashboard-03.png)

5. When you have completed specifying where to save the new dashboard to, select **OK**.

6. Select **Save** after providing a name and description for the new dashboard.

7. On the blank empty dashboard, you see the dashboard name, **Add Widget**, **Edit Dashboard**, **Delete dashboard**, and **View in fullscreen** options on the top of the page.

    :::image type="content" source="./media/create-web-dashboard-alerts/web-console-new-dashboard-04-inline.png" alt-text="Screenshot showing New dashboard canvas." lightbox="./media/create-web-dashboard-alerts/web-console-new-dashboard-04-expanded.png":::

8. Select **Performance Widget** from the **Select Widget** dropdown list.

9. In the Performance widget pane, select scope for the widget by selecting either **Groups** or **Class**.

    ![Screenshot showing Select scope for Performance widget.](./media/create-web-dashboard-perf/web-console-new-dashboard-perf.png)

    For either option selected, you can search by keyword in the list.  As you begin typing, the list filters based on your input.  You can select an individual group or class or multiple from the returned results.

10. Under **Metrics**, search for the performance objects and counters in the search box.  For the results returned, select the object and counter.  If there are multiple instances for the counter, you can select the counter instances from the dropdown list.  This will only be visible if there are multiple instances for the selected counter.

    ![Screenshot showing Select performance counter and instance.](./media/create-web-dashboard-perf/web-console-new-dashboard-perf-02.png)

11. Set the criteria to identify the widget to display.  To narrow the results, you can filter by selecting a time range.

    Data matching the defined criteria will only be displayed in the widget.

    ![Screenshot showing Set criteria for Alert widget.](./media/create-web-dashboard-perf/web-console-new-dashboard-perf-03.png)

12. Select **Display** to choose the columns to be displayed in the dashboard. You can select or search for the columns from the dropdown list.

13. The widget can also be visualized as **Objects by performance widget**.  If you wish to visualize object by performance widget, then select **Visualize objects by performance**.

14. Complete the configuration by providing a **Name**, **Description**, and **Widget refresh interval** (default interval is 5 minutes) for the widget. Select **Save Widget** to save your new dashboard.  

After the widget has been created, it displays a performance graph with the selected objects based on the scope and criteria defined. You see the name of the performance widget along with the number of objects in the header of the widget.

![Screenshot showing Completed example of Performance widget in dashboard.](./media/create-web-dashboard-perf/web-console-new-dashboard-perf-04.png)

## Actions on Performance widget

With a performance widget, you can perform such actions as:

- Specify the minimum and maximum vertical axis values
- Export the alerts to Excel for further analysis
- Modify your selection of legend or enable/disable **Visualize objects by performance**, customized to your personal needs

To perform these actions, hover your mouse over the widget and select the ellipsis **...** at the top right corner of the widget. This will display actions available for the widget.

- Select **Set vertical axis** to modify the scale values of the y axis and select **Save**.  
- Select **Export to Excel** to export the alert data to an Excel file.  
- Select **Personalize** to change your selection of columns to be displayed or to group alerts. Select **Save personalization** when you've completed making your changes.

## Next steps

To learn how to create a dashboard in the new web console with the State widget, see [How create a dashboard with the State widget in the Web console](manage-create-web-dashboard-state.md).
