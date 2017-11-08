---
title: Using Health Explorer to Investigate Problems
description: This article describes how to use the Operations Manager Health Explorer to investigate state change events for when monitors are in an unhealthy state.  
author: mgoedtel
ms.author: magoedte
ms.manager: carmonm
ms.date: 11/28/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
ms.assetid: 61005760-0977-4cd8-b76d-05558160f78f
---

# Using Health Explorer to investigate problems

Use Health Explorer to find out which monitor is reacting and to review knowledge about the monitor and possible causes for actions related to it. In the **Active Alerts** view, click the alert to highlight it. The Health Explorer link under **Alert Actions** in the **Tasks** pane becomes active.  
  
By default, when the Health Explorer window opens, all monitors in a failed state are expanded. If a monitor contains other monitors, as in the case of a roll-up monitor, Health Explorer shows all child monitors in a hierarchical layout, displaying monitoring data for all dependent services and applications. To view more information about any dependent monitor, you can right-click that monitor, and then click **Monitor Properties** to open another Health Explorer window.  

## Monitor health states

The following illustration shows monitors in a healthy state:  
  
![Health explorer showing healthy states](./media/manage-health-using-healthexplorer/om2016-healthexplorer.png)  
  
The following illustration shows some monitors in a critical state:  
  
![Critical monitors in Health Explorer](./media/manage-health-using-healthexplorer/om2016-healthexplorer-criticalmonitors.png)  
  
Click a monitor to view more information about the monitor in the **Details** pane. The **State Change Events** tab in the **Details** pane shows you when the state for the monitor changed, and the details give you information for the context of the state change:  
  
![Details on State Change Events tab](./media/manage-health-using-healthexplorer/om2016-healthexplorer-statechangeevents.png)  
  
## Next steps
 
- Before changing the number of missed heartbeats allowed, first review [How Heartbeats Work in Operations Manager](manage-agent-heartbeat-overview.md).  

- To learn more about how to investigate an agent heartbeat failure and ways to resolve them, review [Resolving Heartbeat Alerts](manage-agent-resolve-heartbeat.md).  

- When an alert is generated, you can [View Active Alerts and Details](manage-alert-view-alerts-details.md) in the Operations and Web console to identify possible issues and help identify next steps towards resolving them.        
