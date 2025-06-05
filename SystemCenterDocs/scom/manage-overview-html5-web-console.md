---
ms.assetid:
title: Overview of HTML5 Web console and dashboards
description: This article provides an overview of the new HTML5 Web console and dashboards in System Center Operations Manager.
author: jyothisuri
ms.author: jsuri
ms.date: 12/13/2024
ms.custom: UpdateFrequency2
ms.service: system-center
monikerRange: '>sc-om-2016'
ms.subservice: operations-manager
ms.topic: article
---

# Overview of HTML5 Web console and dashboards

System Center Operations Manager now delivers HTML5-based dashboards, which enhance the authoring and visualization experiences for Web console users. With these improvements, you can visualize operational data with richer data visualizations, faster performance, and drill-down.  You can access these dashboards from multiple browsers (such as Chrome) and are no longer dependent on Silverlight.

## Supported scenarios

You can take advantage of the following HTML5 dashboard capabilities:

::: moniker range="sc-om-2019"

   Additional view options are included in Alert and State widget from 2019 UR3. For more information, see [Support for Sort by option](manage-create-web-dashboard-alerts.md#support-for-sort-by-option).

::: moniker-end

::: moniker range="sc-om-2022"

 Additional view options are available in Alert and State widget. For more information, see [Support for Sort by option](manage-create-web-dashboard-alerts.md#support-for-sort-by-option).

::: moniker-end

1. Create HTML5 dashboards from multiple browsers without a dependency on Silverlight.  

2. Visualize monitoring data in HTML5 dashboards with:

    - [Alert widget](manage-create-web-dashboard-alerts.md)

    - [State widget](manage-create-web-dashboard-state.md)

    - [Performance widget (also works like the Object by performance widget)](manage-create-web-dashboard-perf.md)  

    - [Topology widget](manage-create-web-dashboard-topology.md)

    - [Tile widget](manage-create-web-dashboard-tile.md)

    - [Custom widget](manage-create-web-dashboard-custom.md)

    - [PowerShell widget](manage-create-web-dashboard-posh.md)


3. Perform create, edit, and delete operations on the widgets.  

4. Create or edit these widgets and scope by objects or groups.

5. Add custom image for **Topology** widgets and place the health of object on top of the image.

6. Create any number of widgets in the dashboard without any predefined layout selection.

7. Easily move, reposition, and resize the widgets in the dashboard.

8. View the dashboards in full screen without the monitoring tree view.

9. Define a custom refresh interval rate for each of the dashboard widgets.

10.	Visualize the following dashboards:

    - Web Application Status.

    - Management Group Health.

    - Management Group Health Trend.

    - UNIX/Linux Computer Summary.

    - Network Summary dashboard.

    - You can view Network Node and Network Interface Dashboard for Network Node/interface from the **Monitored Objects** page.

11. You can visualize the effective configuration of rules and monitors for a monitored object from the **Monitored objects** drill-down page.

12.	You can sign out from your current web console session.

13. Dashboards can be saved in custom management packs and exported.

14.	The following drill-down capabilities are available within the dashboards:

    - Analyze the issue by visualizing the relevant data for a monitored object, individual alert, rule, monitor, and class.

    - Navigate from one object to another.

    - View the tasks associated with selected object.

15. Explore the actions enabled in a widget:

    - Actions with **Alert** widget - Set resolution state on a single alert or select multiple alerts from within the widget.  View alert details delivering the same experience provided in the Operations console when viewing an alert - modify the alert resolution state and drill down to the monitoring object details page by selecting the alert source.

    - Export the data visible in the widget to Excel for further analysis.

    - Personalize by adding or removing columns to visualize and group alerts.

16. Explore actions with **state** widget:

    - Export the data visible in the widget to an Excel format for further analysis.

    - Personalize by adding or removing columns to visualize and group objects.

17. Explore actions with **Topology** widget:

    - Edit state indicator layout and place object health icons anywhere on image.

18. Explore actions with **Performance** widget:

    - Set vertical axis and specify the minimum and maximum values of vertical axis.

    - Export to Excel the legend data to Excel for further analysis.

    - Personalize by adding or removing columns for the legend, and enable or disable visualized objects by performance.

19. Explore actions with **PowerShell** widget:

    - Export to Excel the legend data to Excel for further analysis.

20.	Delete HTML5 dashboards from the Web console; you can create dashboards or views to My workspace.  

21.	The IIS web server hosting the Web console role can be set up with network authentication mode and users can access the Web console using network authentication.

22.	You can provide feedback on HTML5 dashboards from within the Web console.

## Supported browsers

::: moniker range="sc-om-2019"

System Center Operations Manager Web console supports Microsoft Edge 40 and later, Google Chrome 67 and later, and Internet Explorer 11.

::: moniker-end

::: moniker range="sc-om-2022"

System Center Operations Manager Web console supports Microsoft Edge 88 and later, Google Chrome 88 and later, and Internet Explorer 11.

::: moniker-end

::: moniker range="sc-om-2025"

System Center Operations Manager Web console supports Microsoft Edge 121.0.2277.4 and later, and Google Chrome 121 and later.

::: moniker-end

>[!NOTE]
>Internet Explorer compatibility mode isn't supported.
