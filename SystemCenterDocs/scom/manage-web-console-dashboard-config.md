---
ms.assetid:
title: Manage Dashboard and Widget Configuration in Web Console
description: This article describes how to manage the configuration of the HTML5 Web console dashboards and widgets in System Center Operations Manager.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 04/22/2025
ms.custom: UpdateFrequency2, engagement-fy24
ms.service: system-center
monikerRange: '>sc-om-2016'
ms.subservice: operations-manager
ms.topic: how-to
ms.update-cycle: 1095-days
---

# Manage dashboard and widget configuration in the Web console

This article describes how to manage the configuration of the HTML5 Web console dashboards and widgets in System Center Operations Manager.

## Delete a dashboard

To delete dashboard, select the **Delete dashboard** option available from the top banner of the dashboard.

![Screenshot showing Delete dashboard option on page.](./media/manage-web-console-dashboard-config/dashboard-banner-01.png)  

You're prompted to confirm your wish to proceed with deleting the dashboard. This notification appears at the bottom of the page. Select **Yes** to continue or **No** to cancel the operation.

![Screenshot showing Delete dashboard notification.](./media/manage-web-console-dashboard-config/dashboard-delete-notify.png)

## Add dashboards or views to My workspace

To add dashboards or views to My workspace, follow these steps:

1. Right-click on a dashboard or view in the monitoring tree of the Web console and select **Add to My Workspace** from the context menu.

2. On the **Add to My Workspace** pane on the right side of the page, specify which folder in **My Workspace** this dashboard or view should be added.  You can also choose to create a new folder by selecting **New Folder** to better organize your workspace.

3. After specifying the location where to create the new folder, select **OK** and your dashboard or view will be added to your **My Workspace** view.  


## Modify widget configuration

To edit the widget configuration, follow these steps:

1. Hover your mouse over the widget and select the ellipsis **…** at the top right corner of the widget.

2. The options pane for the widget appears, and it displays all the possible actions available for the selected widget. Select **Edit** to launch the authoring pane for the widget.

3. Perform changes to the available settings for the widget and select **Update Widget**.  

After you update the widget, the changes are saved and the message **updating widget…** is displayed at the bottom of the page.

## Delete a widget from the dashboard

To delete a widget from your dashboard, follow these steps:

1. Hover your mouse over the widget.

2. Select **Delete Widget**

3. You're prompted to confirm **Are you sure you want to delete this widget?** at the bottom of the page. Select **Yes** to continue or **No** to cancel the operation.

## Refresh widget
Each widget is automatically refreshed based on the specified refresh interval.  By default,   widgets update every five minutes. To manually refresh it, select the refresh icon at the upper right-hand corner of the widget.

## Edit a dashboard
You can change the presentation layout of the dashboard by resizing or repositioning the widgets to present the information in a more attractive or meaningful way.

### Reposition widget

To move the widget to a different location on the dashboard, select **Edit Dashboard** and hover your mouse over the widget. You will see the cursor change appearance.  Hold down the left mouse button and drag the widget to the desired location on the dashboard.

### Resize the widget
Move your cursor to the bottom right or right border of the widget. You will see the cursor change appearance. Hold down the left mouse button and drag the window to the size you want.

To save the changes you want to keep, select **Save Changes**. If you want to cancel all your changes, select **Undo changes**.

## Next steps
To understand how to create your own custom views and dashboards in Operations Manager, see [Create and scope views in Operations Manager](manage-console-scope-views.md).
