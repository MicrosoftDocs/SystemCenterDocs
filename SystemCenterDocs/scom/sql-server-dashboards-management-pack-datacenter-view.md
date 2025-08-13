---
ms.assetid: 600eb684-a98b-42a6-957b-d43641415b76
title: Datacenter View in Management Pack for SQL Server Dashboards
description: This article explains datacenter view
author: Anastas1ya
manager: evansma
ms.date: 04/21/2025
ms.author: jsuri
ms.topic: concept-article
ms.service: system-center
ms.subservice: operations-manager
---

# Datacenter View

This article explains datacenter view. The **Datacenter** view is the home page of the dashboard. This view provides information about the datacenter health state in an aggregated way.

It's possible to drill down from the **Datacenter** view to the **Instance** view in order to investigate the root cause of the issue.

You can return to the home page from any **Instance** view by selecting **Home** in the navigation pane.

![Screenshot showing the Datacenter view.](./media/sql-server-dashboards-management-pack/datacenter-view.png)

All group tiles on the datacenter view are collapsed by default. A tile consists of two parts:

- The left part displays the number of objects within a group in the worst state and the total number of objects.

- The right part of the widget displays the number of alerts with the highest severity.

![Screenshot showing Datacenter view tiles.](./media/sql-server-dashboards-management-pack/datacenter-view-tiles.png)

Expanded mode shows the number of objects in other states in addition to the data displayed in collapsed mode.

![Screenshot showing Datacenter view expanded tiles.](media/sql-server-dashboards-management-pack/datacenter-view-tiles-expanded.png)

By default, expanded mode displays three Alert widgets: **Critical**, **Warning**, and **Info**. The number of alerts for each alert type is displayed in the corresponding widget.

![Screenshot showing Datacenter view tile mode.](./media/sql-server-dashboards-management-pack/datacenter-view-tiles-expanded-alert-widgets.png)

The Aggregated state monitor tile provides the number of object selected classes per state.

![Screenshot showing Aggregated state monitor.](./media/sql-server-dashboards-management-pack/datacenter-view-tiles-agregated-state-monitor.png)

The Aggregated performance tile shows five columns. Each column represents the number of object selected classes in the current data range.

![Screenshot showing Aggregated performance tile.](./media/sql-server-dashboards-management-pack/datacenter-view-tiles-agregated-performance-tile.png)

>[!NOTE]
>Use the **Datacenter View** menu button or a group to add a new tile or group. It's possible to edit or remove the tile by selecting the corresponding menu item from the right-click context menu. The background color, time interval, and refresh rate settings that are applied to the **Datacenter** view and all the **Instance** views can be set from the Datacenter view menu and Instance view menu.
