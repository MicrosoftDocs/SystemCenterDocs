---
title: Runbook Designer
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d2872531-d700-4852-a02c-5ffbbaf4144e
---
# Runbook Designer
The **Runbook Designer** is the tool that you use to create, manage, and run runbooks in [!INCLUDE[orchlong](./Token/orchlong_md.md)]. The **Runbook Designer** is intended for users who must create or modify runbooks. Users who only have to run runbooks and view their status should use the Orchestration console which is documented in the [Using the Orchestration Console in System Center 2012 - Orchestrator](./Using-the-Orchestration-Console-in-System-Center-2012---Orchestrator.md).

## Runbook Designer Panes
The Runbook Designer interface is organized into the following four panes.

|Pane|Description|
|--------|---------------|
|**Connections**|The folder structure where you can organize workflows in the [!INCLUDE[orchshort](./Token/orchshort_md.md)] system and edit permissions on folders. Also provides access to **Runbook Servers** and **Global Settings**.|
|**Runbook Designer workspace**|The workspace where you build [!INCLUDE[orchshort](./Token/orchshort_md.md)] runbooks. The runbooks in the folder selection in the **Connections** pane are listed as tabs across the top of the workspace. When you select a tab in a runbook, it is displayed in the Runbook Designer workspace.|
|**Activities**|Contains all the activities available \(either standard activities or activities available from integration packs\) for use in runbooks. You drag activities from the **Activities** pane into the Design workspace, and then link them together to form runbooks.|
|**Log**|Logs showing the activity and history for the current runbook. For more information, see [Orchestrator Logs](./Orchestrator-Logs.md).|

## Sorting Activities by Activity Name and Category Name
[!INCLUDE[orchlong](./Token/orchlong_md.md)] lets you sort activities alphabetically by activity name, or by category name. By default, activities are sorted by category, such as Runbook Control, Email, File Management, Monitoring, Notification, Scheduling, System, Text File Management, and Tools.

Use the following steps to sort activities by their activity name and category name.

#### To sort activities alphabetically by activity name

-   In the **Activities** pane, right\-click a category name to select **All Activities**.

    The activities are sorted alphabetically by activity name.

#### To sort activities alphabetically by category name

-   In the **Activities** pane, right\-click a category name to select **Default**.

    The activities are sorted alphabetically by category name.

## Changing Icons
You can change the default size of each activity icon from small to large.

Use the following steps to change the icon size.

#### To change the icon size

-   In the **Activities** pane, right\-click an activity name to select **Small** or **Large** depending on the size of icon that you want to view.

## See Also
[Tools](./Tools.md)


