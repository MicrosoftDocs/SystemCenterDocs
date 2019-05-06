---
title: Using My Workspace in the Web Console
description: This article describes how to use My Workspace in the Operations Manager Web console to create personalized views of operational data for your specific needs.
author: JYOTHIRMAISURI
ms.author: magoedte
ms.manager: carmonm
ms.date: 07/20/2018
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
monikerRange: '>sc-om-2016'
ms.topic: article
ms.assetid:
---

# Using My Workspace in the Web console

With System Center Operations Manager version 1801 and higher, in the new HTML5 Web console you can customize how you view monitoring data for your specific needs differently than previous versions of Operations Manager.  

Using My Workspace allows you to create folders to organize dashboards, add existing views and dashboards from the Monitoring workspace, and create custom dashboards only visible to you in the Web console.    

## Add views and dashboards

From the Monitoring workspace, you can add shortcuts to any existing view or dashboard in the Monitoring workspace.  

1. In the **Monitoring** workspace, select a view or dashboard, right-click, and then click **Add to My Workspace**.  

2. Specify a name for the view/dashboard to personalize it for your needs in the **Name** field.

3. Specify an existing folder or create a new one by clicking on **New Folder** and specifying a folder name, and then click **OK** to save the new folder.  Select the new folder where you want the view or dashboard to appear and then click **OK**.  

When you go to My Workspace, you will see the view or dashboard that you added listed in the navigation pane.  

## Create dashboards  

Dashboards that you create in My Workspace are unique, they are not shortcuts to existing dashboards. As an operator, you can create dashboards in Operations Manager version 1807 or later Web console, in My Workspace.    

>[!NOTE]
>The steps to create a dashboard and add a web part are similar to how you create one in the Monitoring workspace, with one difference - you are not prompted to specify a management pack to save it to. Instead you are prompted to specify an existing folder or create a new one in your workspace.     

For detailed steps, review the following articles:

* Create dashboard with [Alert widget](manage-create-web-dashboard-alerts.md)
* Create dashboard with [State widget](manage-create-web-dashboard-state.md)
* Create dashboard with [Performance widget (also works like the Object by performance widget)](manage-create-web-dashboard-perf.md)  
* Create dashboard with [Topology widget](manage-create-web-dashboard-topology.md)
* Create dashboard with [Tile widget](manage-create-web-dashboard-tile.md)
* Create dashboard with [Custom widget](manage-create-web-dashboard-custom.md)
* Create dashboard with the [PowerShell widget](manage-create-web-dashboard-posh.md), available only with version 1807

## Next steps

For more information on using Health Explorer, see [Using Health Explorer to Investigate Problems](manage-health-using-healthexplorer.md).  
