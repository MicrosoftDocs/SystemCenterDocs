---
title: Use the Operations Manager Operations Console
description: This article describes how to use the Operations Manager Operations console to view operational data from monitored objects in the environment.
author: jyothisuri
ms.author: jsuri
manager: jsuri
ms.date: 11/01/2024
ms.custom: UpdateFrequency2
ms.service: system-center
ms.subservice: operations-manager
ms.topic: concept-article
ms.assetid: 83921ac3-655e-4279-8f16-88818c88349f
---  

# Use the Operations Manager Operations console



In System Center Operations Manager, the Monitoring workspace is the primary workspace for operators, network and system engineers, and service desk. The Monitoring workspace is basically the same in both the Operations and Web consoles.  

When you open the Monitoring workspace, you see an overview that summarizes the health of distributed applications and computers, as well as the objects that are in maintenance mode, as shown in the following image.  

![Screenshot showing Monitoring overview summarizes alert status.](./media/manage-using-monitoring-workspace/summarize-alert-status.png)  

In the **State and Alerts** overview, select any of the numbers to see a detailed view. For example, if you select the number shown for **Maintenance Mode**, a state view of all computers in maintenance mode opens.  

The health states that are summarized in the overview only tell you part of what is going on in your environment. You'll also want to review the alerts that have been generated. In the navigation pane, select **Active Alerts** to see all alerts. For more information about dealing with alerts, see [Manage Alerts](manage-alert-generation-overview.md).  

There are many views and dashboards in the **Monitoring** workspace that allow you to view the status of your environment. For information on each view, see [Standard Views in Operations Manager](manage-console-standard-views.md). Dashboards allow you to consolidate and visualize operational data from different perspectives to make meaningful decisions. For more information, see [Dashboards in Operations Manager](manage-dashboards-overview.md).  You can also change the display options of a view and save it as a personalized view. For more information, see [Personalize a view in Operations Manager](manage-console-personalize-views.md).  

As you work with Operations Manager, you may discover that there are specific views that you frequently access. You can create a customized workspace that displays your favorite views and searches. For more information, see [Use My Workspace in Operations Manager](manage-consoles-my-workspace.md).  

## Next steps

- To filter your view of monitoring data so that you can find the exact monitoring object or group of objects that you need, see [Find data and objects in the Operations Manager Consoles](manage-console-finding-data.md).

- To learn how to use Health Explorer to understand the state of monitored objects in your environment, review [Use Health Explorer to Investigate Problems](manage-consoles-overview-healthexplorer.md).
