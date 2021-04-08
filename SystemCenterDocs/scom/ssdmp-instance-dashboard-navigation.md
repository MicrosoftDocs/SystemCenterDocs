---
ms.assetid: 1c12cdd4-2601-4abd-aab4-e4e85905291d
title: Instance Dashboard Navigation
description: This article explains how to navigate through the dashboards structure 
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Instance Dashboard Navigation

This article explains how to navigate through the structure provided on the dashboards.

## Drill-Down to Related Objects

Drilling-down can be performed as follows:

1. In the left pane, select an object.

2. In the right pane, double click the **Related Objects State** widget.

![Select objects](./media/ssdmp/selecting-object.png)

## Using Show alerts Function

This function allows seeing an object alert list. To activate this function, select the **Show alerts from all events** checkbox.

![Use Show alerts](./media/ssdmp/show-alerts.png)

## Using Navigation Pane

To move to any location in the path just click it. To move to the parent view click the button.

![Use Navigation Pane](./media/ssdmp/navigation-pane.png)

## SQL Instance Path Property

![Instance path property](./media/ssdmp/instance-path-property.png)

A dashboard object path is shown after switching on the **Show instance path** checkbox in the **Settings** menu.

![Show instance path](./media/ssdmp/show-instance-path-checkbox.png)

The user can search objects in the instance view by the path and name if the **Show instance path** checkbox is switched on. To perform a search, start typing the name of the object in the **Filter** field.

![Filter](./media/ssdmp/performing-search.png)

Note that the user can search objects in the instance view by the name only if the **Show instance path** checkbox is switched off.

![Search by name](./media/ssdmp/search-name-only.png)

The user can search objects in the instance view by any part of the object path and by any part of the object name.

![Object path](./media/ssdmp/object-name.png)

A path line of an object without a path is hidden; path lines of all other instances are displayed.

![Path line](./media/ssdmp/object-path.png)

A tooltip with the object name and object path appears when the user hovers over the dashboard object and the **Show instance path** checkbox is enabled/disabled.

![Hovering over dashboard object](./media/ssdmp/tooltip.png)

A tooltip with the object name appears only when the user hovers over the dashboard object with the empty path line.

![Tooltip](./media/ssdmp/tooltip-empty-line.png)

The **Filter** field is cleared every time the user changes the dashboard level.

A user can use the filter field even if the dashboard group has objects with the empty path line and objects with a path at the path line simultaneously.


