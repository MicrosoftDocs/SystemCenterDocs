---
ms.assetid: dd7742fd-dcec-4546-b0f3-59ddaf94459a
title: Quick Reference to Operations Manager Tasks
description: This article summarizes the common tasks to perform after installing Operations Manager in your environment.
author: JYOTHIRMAISURI
ms.author: magoedte
manager: carmonm
ms.date: 07/09/2019
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
---

# Quick reference to Operations Manager tasks

The following table gives a quick reference for where to perform common tasks and links to relevant information.

|To perform this task|Do this|
|------------------------|-----------|
|Check for problems in a management group|-  Check the **Management Group Health** view in the Operations Manager folder in the **Monitoring** workspace<br> - See the **State and Alerts** summary on the Monitoring Overview page<br>-  Check **Active Alerts** in the **Monitoring** workspace<br> - Check **Task Status** in the **Monitoring** workspace|
|Start monitoring a computer|On the Administration Overview page, click **Configure computers and devices to manage**. For more information, see [Operations Manager agents](plan-planning-agent-deployment.md).|
|Start monitoring a network device| On the Administration overview page, click **Configure computers and devices to manage**. For more information, see [Monitor network devices](manage-monitor-networkdevice-overview.md).|
|Create or modify a resource pool|In the **Administration** workspace, click **Resource Pools**. For more information, see [How to Create a Resource Pool](manage-resource-pools-manage.md#to-create-a-resource-pool) and [Managing Resource Pools for UNIX and Linux Computers](manage-resource-pools-manage.md#configure-certificates-for-unix-and-linux-dedicated-resource-pools).|
|-   Create a group<br>-   View available groups<br>-   View group members<br>-   View state of a group<br>-   View diagram of a group<br>-   Modify a group|Click **Groups** in the **Authoring** workspace<br><br>For instructions, see [Creating and Managing Groups](manage-create-manage-groups.md)|
|Create a view|In the **Monitoring** workspace or **My Workspace**, at the bottom of the navigation pane, click **New View**. For more information, see [Using Views in Operations Manager](https://technet.microsoft.com/library/hh212694.aspx).|
|Customize the settings of a view for your own use|In the **Monitoring** workspace, right-click a view in the navigation pane, and then click **Personalize view**. For more information, see [How to Personalize a View in Operations Manager](https://technet.microsoft.com/library/hh270022%28v=sc.12%29.aspx).|
|Change the interval for heartbeats.|In the **Administration** workspace, click **Settings**, and then under **Agent**, click **Heartbeat**. For more information, see [How Heartbeats Work in Operations Manager](manage-agent-heartbeat-overview.md).|
|Change the number of missed heartbeats allowed|In the **Administration** workspace, click **Settings**, and then under **Server**, click **Heartbeat**. For more information, see [How Heartbeats Work in Operations Manager](manage-agent-heartbeat-overview.md).|
|Change a setting for a rule, monitor, or alert.|Make changes to rules, monitors, or alerts by creating an override. Select a rule, monitor, or alert, and then access the overrides options by right-clicking, or clicking **Overrides** on the toolbar, or clicking **Overrides** in the Tasks pane. For more information, see [How to Override a Rule or Monitor](~/scom/manage-mp-override-rule-monitor.md) and [Creating a Management Pack for Overrides](~/scom/manage-mp-create-unsealed-mp.md).|
|Change how frequently records are removed from the operational database.|In the **Administration** workspace, click **Settings**, right-click **Database Grooming**, and then click **Properties**. For more information, see [How to Configure Grooming Settings for the Operations Manager Database](https://technet.microsoft.com/library/hh230753%28v=sc.12%29.aspx).|
|Give a user permissions to view Operations Manager information or perform tasks.|In the **Administration** workspace, click **User Roles**, and then right-click a specific role and click **Properties**. For more information, see [Implementing User Roles](~/scom/manage-security-overview.md)|
|Display a dashboard view on a SharePoint site.|You must deploy the Operations Manager Web Part to a SharePoint site, configure the Web Part to connect to a web console, and add the Web Part to a SharePoint page. For more information, see [Using SharePoint to View Operations Manager Data](https://technet.microsoft.com/library/hh212924%28v=sc.12%29.aspx).|
|Receive notifications of an alert in email, instant message, or text message.|Right-click an alert, point to **Notification subscription**, and then click **Create**. For more information, see [Subscribing to Alert Notifications](https://technet.microsoft.com/library/hh212725%28v=sc.12%29.aspx).|
|Investigate a gray agent.|In the **Monitoring** workspace, in the **Operations Manager\Agent Details\Agent Health State** view, in the **Agent State from Health Service Watcher** section, click the gray agent, and then in the **Tasks** pane, click **Show Gray Agent Connectivity Data**. For more information, see [Not Monitored and Gray Agents](https://support.microsoft.com/help/10129/troubleshooting-gray-agent-states-in-operations-manager-2012).|
|Stop monitoring a computer temporarily.|In the **Monitoring** workspace, click **Windows Computers**, right-click the computer you want to stop monitoring, and click **Maintenance Mode**. For more information, see [How to Suspend Monitoring Temporarily by Using Maintenance Mode](manage-maintenance-mode-overview.md).|
|Monitor health of management group|In the **Monitoring** workspace, navigate to **Operations Manager\Management Group Health** to see important health status information for components and agents in the management group. For more information, see [Monitor health of the management group](manage-monitor-health-mg.md).|
|Migrate the Operations Manager databases|If you need to upgrade your SQL Server or move to a server on new hardware, perform the steps described in the following articles to move the operational or data warehouse database<br>-  [How to move the Operational database](manage-move-opsdb.md)<br>-  [How to move the Reporting DW database](manage-move-omdwdb.md).|
|Configure data retention of Operations Manager databases|To maintain data for a set period of time and maintain optimal performance, you can configure data retention in the Operations Manager and data warehouse database.  Perform the steps described in the following articles<br>-  [How to configure grooming for the Operational database](manage-omdb-grooming-settings.md)<br>-  [How to configure grooming for the Reporting DW database](manage-omdwdb-grooming-settings.md).| 
|How and when to clear the cache|Understand how and when to clear the cache when troubleshooting console or agent issues by performing the steps described in<br>- [How and when to clear the cache](manage-clear-healthservice-cache.md)|
|Configure communication from Operations Manager to SQL Server|If you need to move the Operations Manager databases to a different SQL Server, reconfigure the SQL Server instance, or implement SQL Always On, perform the steps described in [How to configure Operations Manager to communicate with SQL Server](manage-sqlserver-communication.md).|
|Integrate with Azure Monitor|[Integration with Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/platform/om-agents) logs provides an analytics platform that compliments the Data Warehouse to deliver improved analytics, query performance across large data volumes, correlate log data from Azure resources, and longer retention of monitoring data.| 
||

## Next steps

To learn more about what to manage, how to manage, or how to support an Operations Manager management group, see the [Operations Guide for System Center - Operations Manager](manage-operations-guide-overview.md)



