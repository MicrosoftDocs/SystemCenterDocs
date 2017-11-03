---
title: Using the Administration workspace in Operations Manager
description: This article describes the functions you can perform from the Administration workspace in the Operations Manager console.  
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 10/30/2017
ms.custom: na
ms.prod: system-center-2016
ms.assetid: 7b146b6d-d127-4b5c-9008-a4ed5b7ae760
ms.technology: operations-manager
ms.topic: article
---

# Using the Administration workspace in Operations Manager

Applies To: System Center 2016 - Operations Manager

In the System Center 2016 - Operations Manager Operations console, the Administration workspace is the primary workspace for administrators. You use the Administration workspace to configure a management group.  
  
When you first open the Administration workspace or when you click **Administration** in the navigation pane, the Administration Overview opens, which displays task links for any required or optional configuration steps that have not been completed yet.  
  
The sections below describe the different options in the Administration workspace and link to more detailed information about the task or option.  
  
## Connected Management Groups  
You can connect management groups to enable the forwarding of alerts and other monitoring data from a connected management group to the local management group. Tasks can be initiated from a local management group to run on managed objects of a connected management group.  
  
Use **Connected Management Groups** in the Administration workspace to connect a management group or to edit the properties of a connected management group.  
  
For more information, see [Connecting Management Groups in Operations Manager](manage-connecting-mgmtgroups.md).  
  
## Device Management  
You can use **Device Management** to perform configuration of specific management servers, agent-managed computers, agentless-managed computers, UNIX servers, and Linux servers. The following table summarizes the uses of the items in Device Management and provides links to more detailed information.  
  
|Item|Use|For more information|  
|--------|-------|------------------------|  
|Agent Managed|To modify the configuration of agent-managed computers, such as:<br><br>-   Change the primary management server for agent-managed computers.<br>-   Repair the agent installation.<br>-   Uninstall an agent.<br>-   Override the management group agent heartbeat settings on a specific agent. A heartbeat is a periodic pulse from an agent to its management server.<br>-   Configure an agent-managed computer as a proxy for agentless-managed computers.|-   [Discover and install agent on Windows](manage-deploy-windows-agent-console.md)<br>-   [Discover and install agent on UNIX/Linux](manage-deploy-crossplat-agent-console.md))<br>-   [Install agent on Nano Server](manage-deploy-windows-agent-nano.md)<br>-   [Upgrade and uninstall Windows agent](manage-uninstall-windows-agent.md)<br>-   [Upgrade and uninstall UNIX/Linux agent](manage-upgrade-uninstall-crossplat-agent.md)<br>-   [Agentless Monitoring in Operations Manager](manage-agentless-monitoring.md)|  
|Agentless Managed|To change the proxy agent for an agentless-managed computer. The proxy agent can be any agent-managed computer in the management group configured to be a proxy.|[Agentless Monitoring in Operations Manager](manage-agentless-monitoring.md)|  
|Management Servers|To modify the configuration of management servers, such as:<br><br>-   Override the management group heartbeat failure setting and configure the number of missed heartbeats a management server will allow for an agent before it changes the state of the respective computer to critical.<br>-   Override the Management Group Manual Agent Installs setting and configure a management server to reject or put in Pending Management agents installed with MOMAgent.msi.<br>-   Configure a management server as a proxy for agentless managed computers.<br>-   Configure the Internet proxy settings for a management server.|-   [How Heartbeats Work in Operations Manager](manage-agent-heartbeat-overview.md)<br>-   [Manage manual agent installs](manage-process-manual-agent-install.md)<br>-   [Agentless Monitoring in Operations Manager](manage-agentless-monitoring.md)<br>-   [How to Configure the Internet Proxy Settings for a Management server](http://go.microsoft.com/fwlink/?LinkId=207768) |  
|Pending Management|To approve or reject an agent that was installed with MOMagent.msi if the management group for the agent is configured to **Review new manual agent installations in pending management view** but not **Auto-approve new manually installed agents**. Agents pending approval are displayed for this item.|[Process Manual Agent Installations](manage-process-manual-agent-install.md)|  
|UNIX/Linux Servers|To modify the configuration of agent-managed UNIX and Linux servers.|-   [Managing Discovery and Agents](../Topic/Managing%20Discovery%20and%20Agents.md)<br />-   [Monitoring UNIX and Linux Computers by Using Operations Manager](../../om/manage/Monitoring-UNIX-and-Linux-Computers-by-Using-Operations-Manager.md)|  
  
## Management Packs  
When you select **Management Packs** in the Administration workspace, you see a list of all management packs imported into your management group. When you right-click an individual management pack in the results pane, you can view its properties, delete it, or export any customizations to another management group. You can use links in the tasks pane to create, import, and download management packs.  
  
For more information, see [Management pack overview](manage-overview-management-pack.md).  
  
## Network Management  
You can use **Network Management** in the Administration workspace to discover network devices and managed discovered network devices. The following table summarizes the uses of the items in Network Management and provides links to more detailed information.  
  
|Item|Use|For more information|  
|--------|-------|------------------------|  
|Discovery Rules|-   To create rules for discovering network devices<br>-   To modify existing discovery rules|[How to Discover Network Devices in Operations Manager](manage-monitor-networkdevice-discover.md)|  
|Network Devices|To view properties of discovered network devices|[Monitoring Networks by Using Operations Manager](manage-monitor-networkdevice-overview.md)|  
|Network Devices Pending Management|To retry or reject discovered network devices that are pending management|[How to Discover Network Devices in Operations Manager](manage-monitor-networkdevice-discover.md)|  
  
## Notifications  
Notifications generate messages or run commands automatically when an alert is raised on a monitored system. By default, notifications for alerts are not configured. For Operations Manager users to be notified immediately when an alert is generated, you need to configure a channel for notifications, add subscribers, and then create a notification.  
  
In **Notifications** in the Administration workspace, you can create channels, subscribers, subscriptions, and modify the channels, subscribers, and subscriptions that you create. For more information, see [Subscribing to Alert Notifications](manage-notifications-alert-notifications.md).  
  
## Product Connectors  
Product connectors are used to synchronize Operations Manager data with other management systems such as those that monitor non\-Windows computers or create trouble\-tickets. Product connectors can integrate a deployment of Operations Manager&nbsp;into another management platform or connect other management systems into a full Operations Manager management solution. Any product connectors that you integrate with Operations Manager will be displayed in this section of the Administration workspace.  
  
When you install Operations Manager, two internal product connectors are installed. These are used by Operations Manager.  
  
For more information, see [Connecting Operations Manager With Other Management Systems](manage-integration-thirdparty-overview.md).  
  
## Run As Configuration  
You can use **Run As Configuration** in the Administration workspace to manage Run As accounts and profiles. For more information, see [Managing Run As accounts in Operations Manager](manage-security-maintain-runas-profiles.md).
  
## Security  
In Operations Manager, operations such as resolving alerts, running tasks, overriding monitors, viewing alerts, viewing events, and so on have been grouped into user roles, with each user role representing a particular job function. Role\-based security allows you to limit privileges that users have for various aspects of Operations Manager. In **Security** in the Administration workspace, you can add and remove users to specific user roles. You can also modify the properties of user roles that you create.  
  
For more information, see [Implementing User Roles](manage-security-overview.md).  
  
## Settings  
The following table summarizes the settings you can manage in **Settings** in the Administration workspace.  
  
|Item|Use|For more information|  
|--------|-------|------------------------|  
|Agent Heartbeat|Agents generate a heartbeat at specific intervals to ensure they are operating properly. You can adjust the interval.|[How Heartbeats Work in Operations Manager](manage-agent-heartbeat-overview.md)|  
|Alerts|-   To configure alert resolution states.<br>-   To configure automatic alert resolution.|-   [How to Set Alert Resolution States](manage-alert-set-resolution-states.md)<br>-   [How to Configure Automatic Alert Resolution](manage-alert-configure-auto-resolution.md)|  
|Database Grooming|To configure how long different types of data should be retained in the operational database.|[Maintenance of Operations Manager](manage-omdb-grooming-settings.md)|  
|Privacy|To modify the settings for the following programs:<br><br>-   Customer Experience Improvement Program (CEIP)<br>-   Operational Data Reporting<br>-   Error Reporting|[Sending Data to Microsoft](manage-client-monitoring-using-aem.md) in the Deployment Guide|  
|Reporting|Configure the path for the reporting server.|[Using the Reporting Workspace in Operations Manager](manage-reports-run-save-export.md)|  
|Web Addresses|Designate web addresses for the Web console and online company knowledge.|[How to Connect to the Web Console](manage-consoles-how-to-connect.md#how-to-connect-to-the-web-console)|  
|Server Heartbeat|Configure the number of missed heartbeats before the management server pings the agent-managed computer.|[How Heartbeats Work in Operations Manager](manage-agent-heartbeat-overview.md)|  
|Server Security|Specify how the management server should handle manually-installed agents.|[Process Manual Agent Installations](manage-process-manual-agent-install.md)|  
  
