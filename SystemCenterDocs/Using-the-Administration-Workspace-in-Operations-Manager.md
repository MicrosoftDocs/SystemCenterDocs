---
title: Using the Administration Workspace in Operations Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b146b6d-d127-4b5c-9008-a4ed5b7ae760
---
# Using the Administration Workspace in Operations Manager
In the [!INCLUDE[om12long](../Token/om12long_md.md)] Operations console, the Administration workspace is the primary workspace for administrators. You use the Administration workspace to configure a management group and its managed objects.

When you first open the Administration workspace or when you click **Administration** in the navigation pane, the Administration Overview opens, which displays task links for any required or optional configuration steps that have not been completed yet.

The sections below describe the different options in the Administration workspace and link to more detailed information about the task or option.

## <a name="BKMK_connectedmanagementgroups"></a>Connected Management Groups
You can connect management groups to enable the forwarding of alerts and other monitoring data from a connected management group to the local management group. Tasks can be initiated from a local management group to run on managed objects of a connected management group.

Use **Connected Management Groups** in the Administration workspace to connect a management group or to edit the properties of a connected management group.

For more information, see [Connecting Management Groups in Operations Manager](../Topic/Connecting-Management-Groups-in-Operations-Manager.md).

## <a name="BKMK_devicemanagement"></a>Device Management
You can use **Device Management** in the Administration workspace to perform configuration of specific management servers, agent\-managed computers, agentless\-managed computers, UNIX servers, and Linux servers. The following table summarizes the uses of the items in Device Management and provides links to more detailed information.

|Item|Use|For more information|
|--------|-------|------------------------|
|Agent Managed|To modify the configuration of agent\-managed computers, such as:<br /><br />-   Change the primary management server for agent\-managed computers.<br />-   Repair the agent installation.<br />-   Uninstall an agent.<br />-   Override the management group agent heartbeat settings on a specific agent. A heartbeat is a periodic pulse from an agent to its management server.<br />-   Configure an agent\-managed computer as a proxy for agentless\-managed computers.|-   [Managing Discovery and Agents](../Topic/Managing-Discovery-and-Agents.md)<br />-   [Agentless Monitoring in Operations Manager](../Topic/Agentless-Monitoring-in-Operations-Manager.md)|
|Agentless Managed|To change the proxy agent for an agentless\-managed computer. The proxy agent can be any agent\-managed computer in the management group configured to be a proxy.|[Agentless Monitoring in Operations Manager](../Topic/Agentless-Monitoring-in-Operations-Manager.md)|
|Management Servers|To modify the configuration of management servers, such as:<br /><br />-   Override the management group heartbeat failure setting and configure the number of missed heartbeats a management server will allow for an agent before it changes the state of the respective computer to critical.<br />-   Override the Management Group Manual Agent Installs setting and configure a management server to reject or put in Pending Management agents installed with MOMAgent.msi.<br />-   Configure a management server as a proxy for agentless managed computers.<br />-   Configure the Internet proxy settings for a management server.|-   [How Heartbeats Work in Operations Manager](../Topic/How-Heartbeats-Work-in-Operations-Manager.md)<br />-   [Managing Discovery and Agents](../Topic/Managing-Discovery-and-Agents.md)<br />-   [Agentless Monitoring in Operations Manager](../Topic/Agentless-Monitoring-in-Operations-Manager.md)<br />-   [How to Configure the Internet Proxy Settings for an Operations Manager 2012 Management Server](http://go.microsoft.com/fwlink/?LinkId=207768) in the Deployment Guide|
|Pending Management|To approve or reject an agent that was installed with MOMagent.msi if the management group for the agent is configured to **Review new manual agent installations in pending management view** but not **Auto\-approve new manually installed agents**. Agents pending approval are displayed for this item.|[Process Manual Agent Installations](../Topic/Process-Manual-Agent-Installations.md)|
|UNIX\/Linux Servers|To modify the configuration of agent\-managed UNIX and Linux servers.|-   [Managing Discovery and Agents](../Topic/Managing-Discovery-and-Agents.md)<br />-   [Monitoring UNIX and Linux Computers by Using Operations Manager](../Topic/Monitoring-UNIX-and-Linux-Computers-by-Using-Operations-Manager.md)|

## <a name="BKMK_managementpacks"></a>Management Packs
When you select **Management Packs** in the Administration workspace, you see a list of all management packs imported into your management group. When you right\-click an individual management pack in the results pane, you can view its properties, delete it, or export any customizations to another management group. You can use links in the tasks pane to create, import, and download management packs.

For more information, see [Using Management Packs](../Topic/Using-Management-Packs.md).

## <a name="BKMK_networkmanagement"></a>Network Management
You can use **Network Management** in the Administration workspace to discover network devices and managed discovered network devices. The following table summarizes the uses of the items in Network Management and provides links to more detailed information.

|Item|Use|For more information|
|--------|-------|------------------------|
|Discovery Rules|-   To create rules for discovering network devices<br />-   To modify existing discovery rules|[How to Discover Network Devices in Operations Manager](../Topic/How-to-Discover-Network-Devices-in-Operations-Manager.md)|
|Network Devices|To view properties of discovered network devices|[Monitoring Networks by Using Operations Manager](../Topic/Monitoring-Networks-by-Using-Operations-Manager.md)|
|Network Devices Pending Management|To retry or reject discovered network devices that are pending management|[How to Discover Network Devices in Operations Manager](../Topic/How-to-Discover-Network-Devices-in-Operations-Manager.md)|

## <a name="BKMK_notifications"></a>Notifications
Notifications generate messages or run commands automatically when an alert is raised on a monitored system. By default, notifications for alerts are not configured. For Operations Manager users to be notified immediately when an alert is generated, you need to configure a channel for notifications, add subscribers, and then create a notification.

In **Notifications** in the Administration workspace, you can create channels, subscribers, subscriptions, and modify the channels, subscribers, and subscriptions that you create. For more information, see [Subscribing to Alert Notifications](../Topic/Subscribing-to-Alert-Notifications.md).

## <a name="BKMK_productconnectors"></a>Product Connectors
Product connectors are used to synchronize Operations Manager data with other management systems such as those that monitor non\-Windows computers or create trouble\-tickets. Product connectors can integrate a deployment of Operations Manager into another management platform or connect other management systems into a full Operations Manager management solution. Any product connectors that you integrate with Operations Manager will be displayed in this section of the Administration workspace.

When you install Operations Manager, two internal product connectors are installed. These are used by Operations Manager.

For more information, see [Connecting Operations Manager With Other Management Systems](../Topic/Connecting-Operations-Manager-With-Other-Management-Systems.md).

## <a name="BKMK_runasconfiguration"></a>Run As Configuration
You can use **Run As Configuration** in the Administration workspace to manage Run As accounts and profiles. The following table summarizes the uses of the items in **Run As Configuration** and provides links to more detailed information.

|Item|Use|For more information|
|--------|-------|------------------------|
|Accounts|To modify the credentials and distribution for Run As accounts.|[Managing Access in Operations Manager](../Topic/Managing-Access-in-Operations-Manager.md)|
|Profiles|To add, edit, and remove Run As accounts associated with a Run As profile.|[Managing Access in Operations Manager](../Topic/Managing-Access-in-Operations-Manager.md)|

## <a name="BKMK_security"></a>Security
In [!INCLUDE[om12short](../Token/om12short_md.md)], operations such as resolving alerts, running tasks, overriding monitors, viewing alerts, viewing events, and so on have been grouped into user roles, with each user role representing a particular job function. Role\-based security allows you to limit privileges that users have for various aspects of [!INCLUDE[om12short](../Token/om12short_md.md)]. In **Security** in the Administration workspace, you can add and remove users to specific user roles. You can also modify the properties of user roles that you create.

For more information, see [Implementing User Roles](../Topic/Implementing-User-Roles.md).

## <a name="BKMK_settings"></a>Settings
The following table summarizes the settings you can manage in **Settings** in the Administration workspace.

|Item|Use|For more information|
|--------|-------|------------------------|
|Agent Heartbeat|Agents generate a heartbeat at specific intervals to ensure they are operating properly. You can adjust the interval.|[How Heartbeats Work in Operations Manager](../Topic/How-Heartbeats-Work-in-Operations-Manager.md)|
|Alerts|-   To configure alert resolution states.<br />-   To configure automatic alert resolution.|-   [How to Set Alert Resolution States](../Topic/How-to-Set-Alert-Resolution-States.md)<br />-   [How to Configure Automatic Alert Resolution](../Topic/How-to-Configure-Automatic-Alert-Resolution.md)|
|Database Grooming|To configure how long different types of data should be retained in the operational database.|[Maintenance of Operations Manager](../Topic/Maintenance-of-Operations-Manager.md)|
|Privacy|To modify the settings for the following programs:<br /><br />-   Customer Experience Improvement Program \(CEIP\)<br />-   Operational Data Reporting<br />-   Error Reporting|[Sending Data to Microsoft](http://go.microsoft.com/fwlink/?LinkID=207782) in the Deployment Guide|
|Reporting|Configure the path for the reporting server.|[Using the Reporting Workspace in Operations Manager](../Topic/Using-the-Reporting-Workspace-in-Operations-Manager.md)|
|Web Addresses|Designate web addresses for the Web console and online company knowledge.|[How to Connect to the Web Console](../Topic/How-to-Connect-to-the-Web-Console.md)|
|Server Heartbeat|Configure the number of missed heartbeats before the management server pings the agent\-managed computer.|[How Heartbeats Work in Operations Manager](../Topic/How-Heartbeats-Work-in-Operations-Manager.md)|
|Server Security|Specify how the management server should handle manually\-installed agents.|[Process Manual Agent Installations](../Topic/Process-Manual-Agent-Installations.md)|

## See Also
[Using the Reporting Workspace in Operations Manager](../Topic/Using-the-Reporting-Workspace-in-Operations-Manager.md)
[Using the Authoring Workspace in Operations Manager](../Topic/Using-the-Authoring-Workspace-in-Operations-Manager.md)
[Using My Workspace in Operations Manager](../Topic/Using-My-Workspace-in-Operations-Manager.md)
[Using Health Explorer in Operations Manager](../Topic/Using-Health-Explorer-in-Operations-Manager.md)
[Using the Monitoring Workspace in Operations Manager](../Topic/Using-the-Monitoring-Workspace-in-Operations-Manager.md)
[How to Connect to the Web Console](../Topic/How-to-Connect-to-the-Web-Console.md)
[How to Connect to the Operations Console](../Topic/How-to-Connect-to-the-Operations-Console.md)
[Using the Operations Manager Consoles](../Topic/Using-the-Operations-Manager-Consoles.md)

