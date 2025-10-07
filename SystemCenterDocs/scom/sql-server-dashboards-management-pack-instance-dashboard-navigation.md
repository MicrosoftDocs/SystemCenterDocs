---
ms.assetid: 1c12cdd4-2601-4abd-aab4-e4e85905291d
title: Instance dashboard navigation in Management Pack for SQL Server Dashboards
description: This article explains how to navigate through the dashboards structure
author: Anastas1ya
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.topic: how-to
ms.service: system-center
ms.subservice: operations-manager
ms.custom: sfi-image-nochange
---

# Instance Dashboard Navigation

This article explains how to navigate through the structure provided on the dashboards.

## Drill Down to Related Objects

Drilling down can be performed as follows:

1. In the left pane, select an object.

2. In the right pane, double click the **Related Objects State** widget.

![Screenshot showing the Select objects.](./media/sql-server-dashboards-management-pack/selecting-object.png)

## Using Show alerts Function

This function allows seeing an object alert list. To activate this function, select the **Show alerts from all events** checkbox.

![Screenshot showing the Use Show alerts.](./media/sql-server-dashboards-management-pack/show-alerts.png)

## Using Navigation Pane

To move to any location in the path, just click it. To move to the parent view, click the button.

![Screenshot showing the Use Navigation Pane.](./media/sql-server-dashboards-management-pack/navigation-pane.png)

## SQL Instance Path Property

![Screenshot showing the Instance path property.](./media/sql-server-dashboards-management-pack/instance-path-property.png)

A dashboard object path is shown after switching on the **Show instance path** checkbox in the **Settings** menu.

![Screenshot showing the Show instance path.](./media/sql-server-dashboards-management-pack/show-instance-path-checkbox.png)

The user can search objects in the instance view by the path and name if the **Show instance path** checkbox is switched on. To perform a search, start entering the name of the object in the **Filter** field.

![Screenshot showing the Filter.](./media/sql-server-dashboards-management-pack/performing-search.png)

> [!NOTE]
> The user can search objects in the instance view by the name only if the **Show instance path** checkbox is switched off.

![Screenshot showing the Search by name.](./media/sql-server-dashboards-management-pack/search-name-only.png)

The user can search objects in the instance view by any part of the object path and by any part of the object name.

![Screenshot showing the Object path.](./media/sql-server-dashboards-management-pack/object-name.png)

A path line of an object without a path is hidden; path lines of all other instances are displayed.

![Screenshot showing the Path line](./media/sql-server-dashboards-management-pack/object-path.png)

A tooltip with the object name and object path appears when the user hovers over the dashboard object and the **Show instance path** checkbox is enabled/disabled.

![Screenshot showing the Hovering over dashboard object.](./media/sql-server-dashboards-management-pack/tooltip.png)

A tooltip with the object name appears only when the user hovers over the dashboard object with the empty path line.

![Screenshot showing the Tooltip.](./media/sql-server-dashboards-management-pack/tooltip-empty-line.png)

The **Filter** field is cleared every time the user changes the dashboard level.

A user can use the filter field even if the dashboard group has objects with the empty path line and objects with a path at the path line simultaneously.

## Keyboard Navigation

The SQL Server Dashboard management pack allows you to navigate using the keyboard.

The following keys are available:

|Button|Purpose|
|-|-|
|Tab|Navigate to the next section|
|Shift + Tab|Navigate back to the previous section|
|Enter|Enter into the list or element|
|Up|Navigate to the next element of the list|
|Down|Navigate to the previous element of the list|
|Backspace|Collapse or expand the list|
|Left|Navigate to the next tile|
|Right|Navigate to the previous tile|
|A|Navigate to the next spike on the chart|
|D|Navigate back to the previous spike on the chart|
