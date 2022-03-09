---
ms.assetid: 2ad571c2-f460-4b52-bccd-737e0936c5ff
title: Instance view in Management Pack for SQL Server Dashboards
description: This article explains Instance View
author: TDzakhov
ms.author: v-tdzakhov
manager: evansma
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Instance View

The following is an example of an instance view that is displayed after drilling down into a group or an object from the previous view.

![Instance view](./media/sql-server-dashboards-management-pack/instance-view.png)

>[!NOTE]
>Double-click the name of an object in the object widget to drill down to the instance dashboard of related objects (double-click the **Related Objects** tile does the same). The **Back** button is available in the upper-left corner of the navigation pane for navigating back to the previous instance view.

Instance view tiles display information about the current state of the monitors as well as the latest performance data.

Depending on the current state and configuration, these tiles will have different background colors and layout. Refer to examples below for illustrations of the tile capabilities.

Related objects tile displays the number of objects that are either hosted on the selected entity or linked by a containment. Double-clicking the tile opens the instance view for the related objects.

![Instance tiles](./media/sql-server-dashboards-management-pack/instance-view-tiles.png)

The monitor is in a critical state.

![Critical state](./media/sql-server-dashboards-management-pack/critical-state.png)

The monitor is in a healthy state.

![Healthy state](./media/sql-server-dashboards-management-pack/healthy-state.png)

The monitor is in a warning state.

![Warning state](./media/sql-server-dashboards-management-pack/warning-state.png)

The monitor is disabled.

![Disabled monitor](./media/sql-server-dashboards-management-pack/disabled-monitor.png)

The monitor is unavailable.

![Unavailable monitor](./media/sql-server-dashboards-management-pack/unavailable-monitor.png)

The monitor is under maintenance.

![Monitor is under maintenance](./media/sql-server-dashboards-management-pack/maintenance-monitor.png)

The monitor is in a critical state. The data for the selected time range is being displayed.

![Critical state for time range](./media/sql-server-dashboards-management-pack/critical-time-range.png)

The monitor is in a warning state. The data for the selected time range is being displayed.

![Warning state with time range](./media/sql-server-dashboards-management-pack/warning-time-range.png)

The monitor is in a healthy state. The data for the selected time range is being displayed.

![Healthy state with time range](./media/sql-server-dashboards-management-pack/healthy-time-range.png)

The monitor is disabled. The data for the selected time range is being displayed.

![Disable monitor with time range](./media/sql-server-dashboards-management-pack/disabled-time-range.png)

The performance counter has no correlated monitor (note that there is no icon in the top-right corner). The data for the selected time range is being displayed.

![Performance counter](./media/sql-server-dashboards-management-pack/performance-counter.png)

It is possible to view the exact value of the performance metric by hovering the cursor over the performance chart.

![Getting performance metrics](./media/sql-server-dashboards-management-pack/performance-metric-hovering.png)

The monitor is unavailable. The data for the selected time range is being displayed.

![Unavailable time range](./media/sql-server-dashboards-management-pack/unavailable-time-range.png)

The monitor is under maintenance. The data for the selected time range is being displayed.

![Monitor under maintenance with time range](./media/sql-server-dashboards-management-pack/maintenance-time-range.png)