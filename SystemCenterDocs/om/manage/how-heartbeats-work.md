---
title: How Heartbeats Work in Operations Manager
author: mgoedtel
manager: cfreemanwa
ms.date: 2016-09-25
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# How Heartbeats Work in Operations Manager

>Applies To: System Center 2016 - Operations Manager

System Center 2016 - Operations Manager uses *heartbeats* to monitor communication channels between an agent and the agent's primary management server. A heartbeat is a packet of data sent from the agent to the management server on a regular basis, by default every 60 seconds, using port 5723 \(UDP\).  
  
When an agent fails to send a heartbeat 4 times, a **Health Service Heartbeat Failure** alert is generated and the management server attempts to contact the computer by using ping. If the computer does not respond to the ping, a **Failed to Connect to Computer** alert is generated. The following illustration shows this process.<br> ![Agent to MS Heartbeat](../media/om2016-agent-heartbeat.png) 

When you see both alerts, you know the computer cannot be contacted by the management server. When you see only the heartbeat failure alert, you know the computer can be contacted but there is a problem with the agent. Both alerts are closed automatically when heartbeats resume.  
  
> [!NOTE]  
> By default, alerts for missed heartbeats and response to ping are disabled for client operating systems. To receive alerts for client operating systems, override the **Health Service Heartbeat Failure** and **Computer Not Reachable** monitors for the class **Windows Client Operating System** to set the **Generates Alert** parameter to **True**.  
  
The health state for the agent\-managed computer will change to critical \(red\) when the **Health Service Heartbeat Failure** alert is generated. To view details for the health state, right\-click the computer in **Active Alerts**, point to **Open**, and click **Health Explorer**. The Availability node will be expanded to display the critical item. Click **Health Service Heartbeat Failure**, and then click the **State Change Events** tab. You will see a list of state changes with the date and time of occurrence. Select any occurrence to display information in the **Details** pane. The health state will change to healthy \(green\) when heartbeats resume.  
  
You can change the heartbeat interval for all agents and number of missed heartbeats for all management servers in **Settings** in the **Administration** workspace, as shown in the following illustration.<br> ![Configure Global Heartbeat Settings](../media/om2016-settings-heartbeat.png)  
 
You can also override the global heartbeat interval for individual agents and the number of missed heartbeats for individual management servers by opening the properties for the computer in **Agent Managed** or **Management Servers** in the **Administration** workspace. For example, you might increase the heartbeat interval for a computer that has a slow connection to the network.  
  
## Next steps  

- To learn more about how to investigate an agent heartbeat failure and ways to resolve them, review [Resolving Heartbeat Alerts](resolving-heartbeat-alerts.md)  

  
