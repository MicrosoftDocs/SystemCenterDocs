---
ms.assetid: 5cd69170-bfb6-4f02-a1a7-da8ab2a83ceb
title: Adjusting instance dashboard in Management Pack for SQL Server Dashboards
description: This article explains how to adjust instance dashboard
author: Anastas1ya
ms.author: jsuri
ms.date: 11/01/2024
ms.topic: concept-article
ms.service: system-center
ms.subservice: operations-manager
---

# Adjusting Instance Dashboard

By double-clicking a group of a group widget or virtual group, the user drills down to the instance dashboard. The object tree is displayed at the top of the instance dashboard view.

>[!NOTE]
>Instance tiles are available in the instance view only.

![Screenshot showing Adjusting Instance Dashboard.](./media/sql-server-dashboards-management-pack/object-tree.png)

The user will see the list of group objects in the first level of the group or virtual group.

![Screenshot showing First level.](./media/sql-server-dashboards-management-pack/first-group-level.png)

If the user drills down into the group object, the list of group object child elements will be displayed.

![Screenshot showing Child elements.](./media/sql-server-dashboards-management-pack/child-objects.png)

>[!NOTE]
>If the group object or its child doesn't have any child, the user can't drill down into it.

The **Back** button opens the previous instance dashboard. The user can select any element to navigate directly to its dashboard. All objects of the group or children of the object are sorted by their state; the most critical ones are placed at the top of the list.

The **Details** widget lists all the properties of the selected entity. When the user opens the dashboard, the first element is selected automatically, but if the user selects another object, the selection remains even if a refresh event occurs.

By selecting the icon in the header of the dashboard, all data is copied into the clipboard. If the user hovers over a property in the details widget, a similar button is displayed to allow copying the property data.

The Filter searches through the entity name and entity path, or thought entity name only.

![Screenshot showing Filtering data.](./media/sql-server-dashboards-management-pack/filter.png)

It depends on the configuration of the **Show instance path** checkbox in the **Settings** view.

![Screenshot showing Instance path.](./media/sql-server-dashboards-management-pack/show-instance-path.png)

**Active alerts** displays all object alerts excluding the closed ones. Custom alerts are displayed as well.

![Screenshot showing Alerts.](./media/sql-server-dashboards-management-pack/active-alerts.png)

The number of active alerts is displayed in brackets next to the **Active Alerts** title.

![Screenshot showing Active alerts.](./media/sql-server-dashboards-management-pack/active-alerts-brackets.png)

Object alerts and its child alerts are displayed if the **Show alerts from all levels** checkbox is switched on.

![Screenshot showing Alerts from all levels.](./media/sql-server-dashboards-management-pack/show-alerts-from-all-levels.png)

Alerts can be filtered by their names using the **Filter** field.

![Screenshot showing Filter field.](./media/sql-server-dashboards-management-pack/filter-field.png)

The **Related objects** and **Alerts** tiles are displayed by default and can't be deleted. The tile has logic similar to the aggregated state tile. By double-clicking the tile, the user drills down further to the child elements of the selected object.

![Screenshot showing related objects.](./media/sql-server-dashboards-management-pack/related-objects-tile.png)

The **Related objects** tile shows the next level of the object children. The color of the tile complies the worst state color of its children. Under the name of the tile, the user can see the amount of object children in the worst state and the total number of children. The state name and state icon of the worst object children state is displayed under the number of the object children.

![Screenshot showing Object details.](./media/sql-server-dashboards-management-pack/related-obejct-details.png)

The **Alerts** tile displays the amount of its children worst alerts plus its children`s children worst alerts. The color of the tile complies with the color of its children's worst alerts. The severity name and severity icon of its worst children’s alerts is displayed under the number of alerts.

![Screenshot showing Alerts tile.](./media/sql-server-dashboards-management-pack/alerts-tile.png)

From the menu of the **Monitoring** section, the user can add a performance tile, monitor tile, performance and monitor tile by using the **Bulk add tiles** view, customize dashboard view settings by using the **Settings** menu, and refresh the dashboard view.

![Screenshot showing Adding tiles in bulk.](./media/sql-server-dashboards-management-pack/bulk-add-tiles.png)

Double-clicking the performance tile opens a performance view. Double-clicking the monitor tile opens Health Explorer.

## Adding Performance Tile

Double-click the group to drill down from the Datacenter to lnstance level. Click the menu button to add a performance tile.

![Screenshot showing Performance tile.](./media/sql-server-dashboards-management-pack/adding-performance-tile.png)

In the **Add Performance Tile** dialog, select a performance tile.

![Screenshot showing Select a tile.](./media/sql-server-dashboards-management-pack/selecting-performance-tile.png)

There are three types of performance tiles:
- 2x1 without a linked monitor
- 2x1 with a linked monitor
- 1x1 tile

![Screenshot showing Types of tiles](./media/sql-server-dashboards-management-pack/tile-types.png)

The display name is populated automatically when a user selects the rule for the first time. The dropdown supports advanced filtering options based on the entered text.

If the user adds the same tile twice and uses automatic display name population, the date and time value is added automatically to the rule\monitor name in the **DISPLAY NAME** field.

![Screenshot showing Display name](./media/sql-server-dashboards-management-pack/display-name-field.png)

If all rules have a similar prefix, the prefix isn't displayed in the alike rules.

The circle with a cross removes all data from the field.

When a rule is selected, validation messages disappear and the **Add** button becomes enabled. When the user tries to add performance tile with the existing **DISPLAY NAME**, the corresponding error tooltip message appears.

![Screenshot showing the Error.](./media/sql-server-dashboards-management-pack/error-tooltip.png)

If the user selects a monitor, the tile would have a linked monitor, and the tile color will depend on the monitor state. If the user selects a monitor, but sets the 1x1 size right after, the data in the monitor field becomes disabled and is not saved in the configuration if the user added the tile, but becomes enabled again if the user sets the 2x1 size.

![Screenshot showing Select monitor.](./media/sql-server-dashboards-management-pack/selecting-monitor.png)

Upon hovering over the graph, a tooltip with the date and value is displayed.

![Screenshot showing Hover over graph.](./media/sql-server-dashboards-management-pack/hovering-over-graph.png)

The widget has a kind of trend line, which is represented by the arrow. Near the arrow, a user can see the last value of the index.

![Screenshot showing the Index.](./media/sql-server-dashboards-management-pack/index-value.png)

If the rule value hasn't been changed during the displayed period, the trend arrow isn't displayed.

![Screenshot showing the trend arrow.](./media/sql-server-dashboards-management-pack/trend-arrow.png)

>[!NOTE]
>If the index last value is too long to be fully displayed in the tile, it's displayed in the tooltip.

![Screenshot showing the Long values.](./media/sql-server-dashboards-management-pack/value-too-long.png)

The minimum, maximum, and average rule value is displayed near the chart. Measurement units are displayed if the rule has them in its name in brackets. The user can select a period to be displayed in the 2x1 tile chart of the dashboard view **Settings** menu.

![Screenshot showing the Settings.](./media/sql-server-dashboards-management-pack/settings-menu.png)

The 1x1 tile displays only the last value. The same data is displayed in the 2x1 version right under the widget name.

![Screenshot showing the Other tiles.](./media/sql-server-dashboards-management-pack/short-tiles.png)

The last value of date and time is displayed under the rule last value in the 1x1 performance tile. If there's no data in the System Center Operations Manager database for the set period, the widget returns **No Data** message.

![Screenshot showing the No data available.](./media/sql-server-dashboards-management-pack/no-data-message.png)

Two options are available by right-clicking the tile: **Edit** and **Remove**.

![Screenshot showing the Edit.](./media/sql-server-dashboards-management-pack/remove-edit-options.png)

## Adding Monitor Tile

Double-click the Group to drill down from Datacenter to the Instance level. Select the menu button to add a monitor tile.

![Screenshot showing the Adding monitor.](./media/sql-server-dashboards-management-pack/adding-monitor-tile.png)

In the **Add Monitor Tile** dialog, select a monitor.

![Screenshot showing the Monitor dialog.](./media/sql-server-dashboards-management-pack/selecting-monitor-dialog.png)

The control has the logic similar to the performance dialog.

![Screenshot showing the Performance dialog.](./media/sql-server-dashboards-management-pack/performance-dialog.png)

The monitor has a name, state indicator, and the date when the state has been changed for the last time. Two options are available by right-clicking the tile: **Edit** and **Remove**:

![Screenshot showing the Edit options.](./media/sql-server-dashboards-management-pack/remove-edit-options-tiles.png)
