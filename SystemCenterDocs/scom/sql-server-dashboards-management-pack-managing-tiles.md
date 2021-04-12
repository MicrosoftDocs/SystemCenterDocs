---
ms.assetid: 2ad571c2-f460-4b52-bccd-737e0936c5ff
title: Managing Tiles in Management Pack for SQL Server Dashboards
description: This article explains how to manage tiles
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Managing Tiles

The tiles can be moved by means of drag-n-drop. 

Datacenter dashboards allow the following methods of tile moving:

- Moving groups in Datacenter View.
- Moving aggregated tiles within the expanded group in Datacenter View.
- Moving tiles in Instance View.

To open Performance View and Health Explorer, it is necessary to double-click the corresponding tile (performance tile and monitor tile, respectively).

## Adding Tiles in Bulk

The user can use the **Bulk add Tiles** menu to quickly add monitors and performance tiles to the instance view (all object rules and monitors are displayed in the **Chose tiles to be added to the view** list).

![Adding multiple tiles](./media/sql-server-dashboards-management-pack/adding-tiles-bulk.png)

The checkboxes for already added tiles are switched off (monitor tiles that are added as part of 2x1 performance tile are considered already added).

![2x1 performance tile](./media/sql-server-dashboards-management-pack/disabled-chakboxes.png)

Note that checkboxes are switched on for the tiles that have not been added to the instance view.

![Disabled checkboxes](./media/sql-server-dashboards-management-pack/enabled-checkboxes.png)

Performance and monitor have different icons.

![Performance and monitor icons](./media/sql-server-dashboards-management-pack/icons.png)

The same performance and monitor tiles can be added many times by means of the **Bulk add Tiles** menu. The date and time parameters will be added to **DISPLAY NAME** for each subsequent adding of repeated performance\monitor tiles.

![Repeated performance\monitor tiles](./media/sql-server-dashboards-management-pack/date_time.png)