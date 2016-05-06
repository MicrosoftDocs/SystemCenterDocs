---
title: Determining the Health of Gateway Servers
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed74aa35-54e0-47bb-ab85-38f5b67d4533
---
# Determining the Health of Gateway Servers
To determine the health of a gateway server, you must examine it from two perspectives. The first, most direct method is to examine the health status in the Operations console and in Health Explorer.  This examination will tell you the status of the monitored components, indicate whether or not there are any open alerts, and show you performance data.  The second, indirect method is to be sure that data from the agents that are being monitored through the gateway server is being reported in a timely fashion.

## Direct Method
Gateway servers are a type of management server, and therefore they are included in **Management Servers** under **Device Management** in the **Administration** workspace of the Operations console. In the details pane of this view, you can immediately see the **Health State** of any of management servers in the management group. By selecting any gateway server \(or any server for that matter\) and opening the context menu, you can view the properties of the server or any of the views that are available. Typically, you can directly access the **Event View**, **Alert View**, **Performance View**, **Diagram View**, and **State View** for the selected object.

For a more comprehensive understanding of the health of a gateway server, open the **Monitoring** view and navigate to the **Operations Manager**, **Management Server** folder and select the **Management Server State** view object in the navigation pane. This displays the state of all management servers in the management group, with gateway servers displayed next to the bottom by default. In the **Gateway Management Server State** pane, select the health status icon for the server you are interested in under the **Gateway** column to bring up the health state of the gateway servers component monitors in the details pane. Typically, you will get details on the **Health Service Availability**, **Audit Collection Availability**, **Configuration**, **Performance**, and **Security**.

## Indirect Method
Gateway servers relay monitoring data from agents to collection management servers in the management group across trust boundaries. They also relay configuration information from the collection management server to the agents that they serve. Therefore, if agents that have a gateway server as their primary management server are reporting their data and are showing a heartbeat, you can be sure that their gateway server is performing satisfactorily.

## Viewing Agents by Gateway
Use the following procedure to view the primary management server for an agent.

#### How to view an agent’s primary management server

1.  Open the Operations console, and then click **Administration**.

2.  In the **Administration** workspace, click **Agent Managed**.

3.  Displayed in the results pane are all the agent\-managed devices grouped by their **Primary Management Server**.

4.  Look for the gateway server of interest. Grouped under it are all the agents that are currently using the gateway server.

## See Also
[Monitoring Across Untrusted Boundaries in Operations Manager](./Monitoring-Across-Untrusted-Boundaries-in-Operations-Manager.md)
[About Gateway Servers in Operations Manager](./About-Gateway-Servers-in-Operations-Manager.md)
[How to Configure Agent Failover to Multiple Gateway Servers](./How-to-Configure-Agent-Failover-to-Multiple-Gateway-Servers.md)
[How to Configure a Gateway Server to Failover Between Multiple Management Servers](./How-to-Configure-a-Gateway-Server-to-Failover-Between-Multiple-Management-Servers.md)
[Certificate Renewal for Gateway Servers and Management Servers](./Certificate-Renewal-for-Gateway-Servers-and-Management-Servers.md)


