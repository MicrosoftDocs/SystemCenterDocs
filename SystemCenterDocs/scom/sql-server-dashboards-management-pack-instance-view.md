---
ms.assetid: 2ad571c2-f460-4b52-bccd-737e0936c5ff
title: Instance view in Management Pack for SQL Server Dashboards
description: This article explains Instance View
author: Anastas1ya
ms.author: jsuri
ms.date: 11/01/2024
ms.topic: concept-article
ms.service: system-center
ms.subservice: operations-manager
ms.custom: sfi-image-nochange
---

# Instance View

The following is an example of an instance view that's displayed after drilling down into a group or an object from the previous view.

![Screenshot showing the Instance view.](./media/sql-server-dashboards-management-pack/instance-view.png)

>[!NOTE]
>Double-click the name of an object in the object widget to drill down to the instance dashboard of related objects (double-click the **Related Objects** tile does the same). The **Back** button is available in the upper-left corner of the navigation pane for navigating back to the previous instance view.

Instance view tiles display information about the current state of the monitors and the latest performance data.

Depending on the current state and configuration, these tiles will have different background colors and layout. Refer to the examples below for illustrations of the tile capabilities.

Related objects tile displays the number of objects that are either hosted on the selected entity or linked by a containment. Double-clicking the tile opens the instance view for the related objects.

![Screenshot showing the Instance tiles.](./media/sql-server-dashboards-management-pack/instance-view-tiles.png)

The monitor is in a critical state.

![Screenshot showing the Critical state.](./media/sql-server-dashboards-management-pack/critical-state.png)

The monitor is in a healthy state.

![Screenshot showing the Healthy state.](./media/sql-server-dashboards-management-pack/healthy-state.png)

The monitor is in a warning state.

![Screenshot showing the Warning state.](./media/sql-server-dashboards-management-pack/warning-state.png)

The monitor is disabled.

![Screenshot showing the Disabled monitor.](./media/sql-server-dashboards-management-pack/disabled-monitor.png)

The monitor is unavailable.

![Screenshot showing the Unavailable monitor.](./media/sql-server-dashboards-management-pack/unavailable-monitor.png)

The monitor is under maintenance.

![Screenshot showing the Monitor is under maintenance.](./media/sql-server-dashboards-management-pack/maintenance-monitor.png)

The monitor is in a critical state. The data for the selected time range is being displayed.

![Screenshot showing Critical state for time range.](./media/sql-server-dashboards-management-pack/critical-time-range.png)

The monitor is in a warning state. The data for the selected time range is being displayed.

![Screenshot showing Warning state with time range.](./media/sql-server-dashboards-management-pack/warning-time-range.png)

The monitor is in a healthy state. The data for the selected time range is being displayed.

![Screenshot showing Healthy state with time range.](./media/sql-server-dashboards-management-pack/healthy-time-range.png)

The monitor is disabled. The data for the selected time range is being displayed.

![Screenshot showing Disable monitor with time range.](./media/sql-server-dashboards-management-pack/disabled-time-range.png)

The performance counter has no correlated monitor (note that there's no icon in the top-right corner). The data for the selected time range is being displayed.

![Screenshot showing the Performance counter.](./media/sql-server-dashboards-management-pack/performance-counter.png)

It's possible to view the exact value of the performance metric by hovering the cursor over the performance chart.

![Screenshot showing Getting performance metrics.](./media/sql-server-dashboards-management-pack/performance-metric-hovering.png)

The monitor is unavailable. The data for the selected time range is being displayed.

![Screenshot showing Unavailable time range.](./media/sql-server-dashboards-management-pack/unavailable-time-range.png)

The monitor is under maintenance. The data for the selected time range is being displayed.

![Screenshot showing Monitor under maintenance with time range.](./media/sql-server-dashboards-management-pack/maintenance-time-range.png)
