---
title: Using My Workspace in the Web Console
description: This article describes how to use My Workspace in the Operations Manager Web console to create personalized views of operational data for your specific needs.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.custom: UpdateFrequency2, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
monikerRange: '>sc-om-2016'
ms.topic: how-to
ms.update-cycle: 1095-days
ms.assetid:
---

# Using My Workspace in the Web console



Using System Center Operations Manager HTML5 Web console, you can customize how you view monitoring data for your specific needs differently than the previous versions of Operations Manager.  

Using My Workspace allows you to create folders to organize dashboards, add existing views and dashboards from the Monitoring workspace, and create custom dashboards only visible to you in the Web console.

## Add views and dashboards

From the Monitoring workspace, you can add shortcuts to any existing view or dashboard in the Monitoring workspace.  

1. In the **Monitoring** workspace, select a view or dashboard, right-click, and select **Add to My Workspace**.  

2. Specify a name for the view/dashboard to personalize it for your needs in the **Name** field.

3. Specify an existing folder or create a new one by selecting **New Folder** and specifying a folder name, and select **OK** to save the new folder.  Select the new folder where you want the view or dashboard to appear and select **OK**.  

When you go to My Workspace, you'll see the view or dashboard that you added listed in the navigation pane.  

## Create dashboards  

Dashboards that you create in My Workspace are unique; they aren't shortcuts to the existing dashboards. As an operator, you can create dashboards in Operations Manager Web console, in **My Workspace**.

>[!NOTE]
>The steps to create a dashboard and add a web part are similar to how you create one in the Monitoring workspace, with one difference—you aren't prompted to specify a management pack to save it to. Instead, you're prompted to specify an existing folder or create a new one in your workspace.

For detailed steps, review the following articles:

* Create dashboard with [Alert widget](manage-create-web-dashboard-alerts.md)
* Create dashboard with [State widget](manage-create-web-dashboard-state.md)
* Create dashboard with [Performance widget (also works like the Object by performance widget)](manage-create-web-dashboard-perf.md)  
* Create dashboard with [Topology widget](manage-create-web-dashboard-topology.md)
* Create dashboard with [Tile widget](manage-create-web-dashboard-tile.md)
* Create dashboard with [Custom widget](manage-create-web-dashboard-custom.md)
* Create dashboard with the [PowerShell widget](manage-create-web-dashboard-posh.md)




::: moniker range="sc-om-2019"
>[!NOTE]
>Operations Manager 2019 UR2 supports folders' creation in web console, inside which you can place dashboards. For more information, see [create a folder in web console](support-folders-monitoring-view-web-console.md)

::: moniker-end

::: moniker range="sc-om-2022"
>[!NOTE]
>Operations Manager supports folders' creation in web console, inside which you can place dashboards. For more information, see [create a folder in web console](support-folders-monitoring-view-web-console.md)

::: moniker-end

## Next steps

For more information on using Health Explorer, see [Using Health Explorer to Investigate Problems](manage-health-using-healthexplorer.md).  
