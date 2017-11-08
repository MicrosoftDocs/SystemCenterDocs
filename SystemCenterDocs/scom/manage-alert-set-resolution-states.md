---
title: How to Set Alert Resolution States
description: This article describes how to set custom resolution states for alerts generated in Operations Manager to support your incident management process.  
author: mgoedtel
ms.author: magoedte
ms.manager: cfreeman
ms.date: 12/05/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
ms.assetid: d2717f98-84fc-43d7-8c06-bdd5aaf386c0
---

# How to set alert resolution states

In System Center 2016- Operations Manager there are seven default resolution states for alerts: 

   | Resolution State | ID | 
   |------------------|----|
   | New | 0 |
   | Closed | 255 |
   | Acknowledge | 249 | 
   | Assigned to Engineering | 248 |
   | Awaiting Evidence | 247 | 
   | Resolved | 254 | 
   | Scheduled | 250 | 
  
When an alert is generated, its resolution state is **New**. Operators can change the resolution state for a new alert to Closed or to a custom resolution state that an administrator has created for the management group.  
  
Custom alert resolution states can used any descriptor you want, such as "Assigned to support" or "Requires investigation". The default resolution states cannot be changed or deleted.  
  
Each resolution state is assigned an ID, a number which uniquely identifies that resolution state. You can assign custom resolution states any that is not already used, and you cannot use a value higher than 255.  
  
## To set the resolution state for an alert  
  
1.  In the Operations console, click **Monitoring**.  
  
2.  Click any view that displays alerts, such as **Active Alerts**.  
  
3.  Right-click an alert, point to **Set Resolution State**, and then click the desired resolution state.  
  
## To create an alert resolution state  
  
1.  In the Operations console, click **Administration**.  
  
2.  Click **Settings**.  
  
3.  Double-click **Alerts**.  
  
4.  On the **Alert Resolution States** tab, click **New**.  
  
5.  In **Add Alert Resolution State**, type a name for the resolution state and select a value in the **Unique ID** box, and then click **OK**.  
  
6.  In **Global Management Group Settings - Alerts**, click **OK**.  
  
## Next steps
 
- Before changing the number of missed heartbeats allowed, first review [How Heartbeats Work in Operations Manager](manage-agent-heartbeat-overview.md).  

- To learn more about how to investigate an agent heartbeat failure and ways to resolve them, review [Resolving Heartbeat Alerts](manage-agent-resolve-heartbeat.md).  

- When an alert is generated, you can [View Active Alerts and Details](manage-alert-view-alerts-details.md) in the Operations and Web console to identify possible issues and help identify next steps towards resolving them. 
  
