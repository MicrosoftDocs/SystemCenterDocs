---
title: Quick Reference to Operations Manager Tasks
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f270994e-2b88-4e58-945f-f1c7954e0e0c
---
# Quick Reference to Operations Manager Tasks
The following table gives a quick reference for where to perform common tasks and links to relevant information.

|To perform this task|Do this|
|------------------------|-----------|
|Check for problems in a management group|-   Check the **Management Group Health** view in the Operations Manager folder in the **Monitoring** workspace<br />-   See the **State and Alerts** summary on the Monitoring Overview page<br />-   Check **Active Alerts** in the **Monitoring** workspace<br />-   Check **Task Status** in the **Monitoring** workspace|
|Start monitoring a computer|On the Administration Overview page, click **Configure computers and devices to manage**. For more information, see [Managing Discovery and Agents](Managing-Discovery-and-Agents.md).|
|Create or modify a resource pool|In the **Administration** workspace, click **Resource Pools**. For more information, see [How to Create a Resource Pool](How-to-Create-a-Resource-Pool.md) and [Managing Resource Pools for UNIX and Linux Computers](https://technet.microsoft.com/library/hh287152%28v=sc.12%29.aspx).|
|-   Create a group<br />-   View available groups<br />-   View group members<br />-   View state of a group<br />-   View diagram of a group<br />-   Modify a group|Click **Groups** in the **Authoring** workspace<br /><br />For instructions, see [Creating and Managing Groups](https://technet.microsoft.com/library/hh212842%28v=sc.12%29.aspx)|
|Create a view|In the **Monitoring** workspace or **My Workspace**, at the bottom of the navigation pane, click **New View**. For more information, see [Using Views in Operations Manager](https://technet.microsoft.com/library/hh212694.aspx).|
|Customize the settings of a view for your own use|In the **Monitoring** workspace, right-click a view in the navigation pane, and then click **Personalize view**. For more information, see [How to Personalize a View in Operations Manager](https://technet.microsoft.com/library/hh270022%28v=sc.12%29.aspx).|
|Change the interval for heartbeats.|In the **Administration** workspace, click **Settings**, and then under **Agent**, click **Heartbeat**. For more information, see [How Heartbeats Work in Operations Manager](How-Heartbeats-Work-in-Operations-Manager.md).|
|Change the number of missed heartbeats allowed|In the **Administration** workspace, click **Settings**, and then under **Server**, click **Heartbeat**. For more information, see [How Heartbeats Work in Operations Manager](https://technet.microsoft.com/library/hh212798%28v=sc.12%29.aspx).|
|Change a setting for a rule, monitor, or alert.|Make changes to rules, monitors, or alerts by creating an override. Select a rule, monitor, or alert, and then access the overrides options by right-clicking, or clicking **Overrides** on the toolbar, or clicking **Overrides** in the Tasks pane. For more information, see [Tuning Monitoring by Using Targeting and Overrides](https://technet.microsoft.com/library/hh230704%28v=sc.12%29.aspx) and [Creating a Management Pack for Overrides](https://technet.microsoft.com/library/hh212841%28v=sc.12%29.aspx).|
|Change how frequently records are removed from the operational database.|In the **Administration** workspace, click **Settings**, right-click **Database Grooming**, and then click **Properties**. For more information, see [How to Configure Grooming Settings for the Operations Manager Database](https://technet.microsoft.com/library/hh230753%28v=sc.12%29.aspx).|
|Give a user permissions to view Operations Manager information or perform tasks.|In the **Administration** workspace, click **User Roles**, and then right-click a specific role and click **Properties**. For more information, see [Implementing User Roles](https://technet.microsoft.com/library/hh230728%28v=sc.12%29.aspx) and [How to Assign Members to User Roles](https://technet.microsoft.com/library/hh528917%28v=sc.12%29.aspx).|
|Display a dashboard view on a SharePoint site.|You must deploy the Operations Manager Web Part to a SharePoint site, configure the Web Part to connect to a web console, and add the Web Part to a SharePoint page. For more information, see [Using SharePoint to View Operations Manager Data](https://technet.microsoft.com/en-us/library/hh212924%28v=sc.12%29.aspx).|
|Receive notifications of an alert in email, instant message, or text message.|Right-click an alert, point to **Notification subscription**, and then click **Create**. For more information, see [Subscribing to Alert Notifications](https://technet.microsoft.com/library/hh212725%28v=sc.12%29.aspx).|
|Investigate a gray agent.|In the **Monitoring** workspace, in the **Operations Manager\Agent Details\Agent Health State** view, in the **Agent State from Health Service Watcher** section, click the gray agent, and then in the **Tasks** pane, click **Show Gray Agent Connectivity Data**. For more information, see [Not Monitored and Gray Agents](https://technet.microsoft.com/library/hh212723%28v=sc.12%29.aspx).|
|Stop monitoring a computer temporarily.|In the **Monitoring** workspace, click **Windows Computers**, right-click the computer you want to stop monitoring, and click **Maintenance Mode**. For more information, see [How to Suspend Monitoring Temporarily by Using Maintenance Mode](How-to-Suspend-Monitoring-Temporarily-by-Using-Maintenance-Mode.md).|
|||

## See Also
[Operations Guide for System Center 2016 - Operations Manager](System-Center-2016---Operations-Manager-Operations-Guide.md)


