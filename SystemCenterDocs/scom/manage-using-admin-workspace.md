---
title: Use the Administration workspace in Operations Manager
description: This article describes the functions you can perform from the Administration workspace in the Operations Manager console.
author: jyothisuri
ms.author: jsuri
ms.date: 03/26/2025
ms.custom: UpdateFrequency2, engagement-fy24
ms.service: system-center
ms.assetid: 7b146b6d-d127-4b5c-9008-a4ed5b7ae760
ms.subservice: operations-manager
ms.topic: article
---

# Use the Administration workspace in Operations Manager



In the System Center - Operations Manager Operations console, the Administration workspace is the primary workspace for administrators. You use the Administration workspace to configure a management group.  

When you first open the Administration workspace or when you select **Administration** in the navigation pane, the Administration Overview opens, which displays task links for any required or optional configuration steps that haven't been completed yet.  

The sections below describe the different options in the Administration workspace and link to more detailed information about the task or option.  

## Connected Management Groups  
You can connect management groups to enable the forwarding of alerts and other monitoring data from a connected management group to the local management group. Tasks can be initiated from a local management group to run on managed objects of a connected management group.  

Use **Connected Management Groups** in the Administration workspace to connect a management group or to edit the properties of a connected management group.  

For more information, see [Connect management groups in Operations Manager](manage-connecting-mgmtgroups.md).  

## Device Management  
You can use **Device Management** to perform the configuration of specific management servers, agent-managed computers, agentless-managed computers, UNIX servers, and Linux servers. The following table summarizes the uses of the items in Device Management and provides links to more detailed information.  

|Item|Use|For more information|  
|--------|-------|------------------------|  
|Agent Managed|Change the primary management server for agent-managed computers.<br>   Repair the agent installation.<br>   Uninstall an agent.<br>   Override the management group agent heartbeat settings on a specific agent. A heartbeat is a periodic pulse from an agent to its management server.<br>   Configure an agent-managed computer as a proxy for agentless-managed computers.|   [Configure agent on Windows computers](manage-deploy-config-windows-agent.md)<br>   [Upgrade and uninstall Windows agent](manage-uninstall-windows-agent.md)<br>   [Upgrade and uninstall UNIX/Linux agent](manage-upgrade-uninstall-crossplat-agent.md)<br>   [Agentless monitoring in Operations Manager](manage-agentless-monitoring.md)|  
|Agentless Managed|Change the proxy agent for an agentless-managed computer. The proxy agent can be any agent-managed computer in the management group configured to be a proxy.|[Agentless monitoring in Operations Manager](manage-agentless-monitoring.md)|  
|Management Servers|Override the management group heartbeat failure setting and configure the number of missed heartbeats a management server will allow for an agent before it changes the state of the respective computer to critical.<br>   Override the Management Group Manual Agent Installs setting and configure a management server to reject or put in Pending Management agents installed with MOMAgent.msi.<br>   Configure a management server as a proxy for agentless managed computers.<br>   Configure the Internet proxy settings for a management server.|   [How heartbeats work in Operations Manager](manage-agent-heartbeat-overview.md)<br>   [Manage manual agent installs](manage-process-manual-agent-install.md)<br>   [Agentless monitoring in Operations Manager](manage-agentless-monitoring.md)<br>   [Configure the Internet proxy settings for a Management server](/previous-versions/system-center/system-center-2012-R2/hh456443(v=sc.12)) |  
|Pending Management|Approve or reject an agent that was installed with MOMagent.msi if the management group for the agent is configured to **Review new manual agent installations in pending management view** but not **Auto-approve new manually installed agents**. Agents pending approval are displayed for this item.|[Process manual agent installations](manage-process-manual-agent-install.md)|  
|UNIX/Linux Servers|Modify the configuration of agent-managed UNIX and Linux servers.|[Agent deployment planning](plan-planning-agent-deployment.md)<br>   [Discover and install agent on UNIX/Linux](manage-deploy-crossplat-agent-console.md)|  

## Management Packs  
Under the  **Management Packs** node in the Administration workspace, you can perform several tasks related to the management of the management packs imported into your management group.  The following table summarizes the uses of the items under Management Packs and provides links to more detailed information.

|Item|Use|For more information|  
|--------|-------|------------------------|  
|Installed Management Packs |Lists all management packs imported into your management group.|[Import, export, remove management packs](manage-mp-import-remove-delete.md)|
|Tune Management Packs| Highlight the management packs and its workflows that generate a high volume of alerts.| [Data driven alert management](manage-alert-data-driven-management.md)|
|Updates and Recommendations | Identify new technologies or workloads that aren't monitored by Operations Manager or not monitored with the latest version of a management pack.| [MP updates and recommendations](manage-mp-mpassessment.md)

For more information, see [Management pack overview](manage-overview-management-pack.md).  

## Network Management  
You can use **Network Management** in the Administration workspace to discover network devices and managed discovered network devices. The following table summarizes the uses of the items in Network Management and provides links to more detailed information.  

|Item|Use|For more information|  
|--------|-------|------------------------|  
|Discovery Rules|Create rules for discovering network devices.<br>Modify existing discovery rules.|[Discover network devices in Operations Manager](manage-monitor-networkdevice-discover.md)|  
|Network Devices|View properties of discovered network devices.|[Monitoring networks by using Operations Manager](manage-monitor-networkdevice-overview.md)|  
|Network Devices Pending Management|Retry or reject discovered network devices that are pending management.|[Discover network devices in Operations Manager](manage-monitor-networkdevice-discover.md)|  

## Notifications  
Notifications generate messages or run commands automatically when an alert is raised on a monitored system. By default, notifications for alerts aren't configured. For Operations Manager users to be notified immediately when an alert is generated, you need to configure a channel for notifications, add subscribers, and then create a notification.  

In **Notifications** in the Administration workspace, you can create channels, subscribers, subscriptions, and modify the channels, subscribers, and subscriptions that you create. For more information, see [Subscribe to alert notifications](manage-notifications-alert-notifications.md).  

## Product Connectors  
Product connectors are used to synchronize Operations Manager data with other management systems such as those that monitor non\-Windows computers or create trouble\-tickets. Product connectors can integrate a deployment of Operations Manager&nbsp;into another management platform or connect other management systems into a full Operations Manager management solution. Any product connectors that you integrate with Operations Manager are displayed in this section of the Administration workspace.  

When you install Operations Manager, two internal product connectors are installed that are used by Operations Manager.  

For more information, see [Connect Operations Manager with other management systems](manage-integration-thirdparty-overview.md).  

## Run As Configuration  
You can use **Run As Configuration** in the Administration workspace to manage Run As accounts and profiles. For more information, see [Manage Run As accounts in Operations Manager](manage-security-maintain-runas-profiles.md).

## Security  
In Operations Manager, operations such as resolving alerts, running tasks, overriding monitors, viewing alerts, viewing events, and so on, are grouped into user roles, with each user role representing a particular job function. Role-based security allows you to limit privileges that users have for various aspects of Operations Manager. In **Security** in the Administration workspace, you can add and remove users to specific user roles. You can also modify the properties of user roles that you create.  

For more information, see [Implement User Roles](manage-security-overview.md).  

## Settings  
The following table summarizes the settings you can manage in **Settings** in the Administration workspace.  

|Item|Use|For more information|  
|--------|-------|------------------------|  
|Agent Heartbeat|Agents generate a heartbeat at specific intervals to ensure they're operating properly. You can adjust the interval.|[How heartbeats work in Operations Manager](manage-agent-heartbeat-overview.md)|  
|Alerts|Configure alert resolution states.<br>Configure automatic alert resolution.|   [Set alert resolution states](manage-alert-set-resolution-states.md)<br>   [Configure automatic alert resolution](manage-alert-configure-auto-resolution.md)|  
|Database Grooming|Configure how long different types of data should be retained in the operational database.|[Maintenance of Operations Manager](manage-omdb-grooming-settings.md)|  
|Privacy|Customer Experience Improvement Program (CEIP) Operational Data Reporting<br>   Error Reporting|[Send data to Microsoft](manage-client-monitoring-using-aem.md)|  
|Reporting|Configure the path for the reporting server.|[Use the reporting workspace in Operations Manager](manage-reports-run-save-export.md)|  
|Web Addresses|Designate web addresses for the Web console and online company knowledge.|[Connect to the Web Console](manage-consoles-how-to-connect.md#connect-to-the-web-console)|  
|Server Heartbeat|Configure the number of missed heartbeats before the management server pings the agent-managed computer.|[How heartbeats work in Operations Manager](manage-agent-heartbeat-overview.md)|  
|Server Security|Specify how the management server should handle manually installed agents.|[Process manual agent installations](manage-process-manual-agent-install.md)|


## Next steps
- To use the Operations Manager Operations console to perform authoring tasks, see [Use the Authoring workspace in Operations Manager](manage-using-authoring-workspace.md).
- To use the Operations Manager Operations console to view and administer reports, see [Use the Reporting workspace in Operations Manager](manage-using-reporting-workspace.md).