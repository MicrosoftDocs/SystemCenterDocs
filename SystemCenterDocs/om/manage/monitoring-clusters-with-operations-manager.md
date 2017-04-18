---
title: Monitoring Clusters with Operations Manager
description: This article describes how to monitor clustered computers and components in Operations Manager 2016.
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 04/10/2017
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
ms.assetid: 6842cddc-b875-4358-8f00-f4b8ab784739
---

# Monitoring clusters with Operations Manager
System Center - 2016 Operations Manager can monitor computers, disks, and shared volumes that are in clustered configurations running on the Windows Server operating system. Operations Manager can also monitor cluster-aware applications running on a Windows Failover Cluster deployments such as database applications, transaction processing applications, hypervisors, file and print server applications, and other applications.  

Operations Manager discovers an instance of Windows Cluster and basic details of it, but it doesn't provide detailed monitoring of components and overall health of the cluster.  This requires the Windows Server Failover Cluster management pack to proactively monitor availability and performance of cluster nodes, resource groups, and resources supporting the cluster.     

For information on monitoring clustered components or services, please review the following:

* [System Center 2016 Management Pack for Windows Server Operating System](https://www.microsoft.com/download/details.aspx?id=54303) - monitors the availability, health, and performance of the Windows Server 2016 operating system.  It includes discovery and monitoring of clustered shared volumes and disks.

* [System Center Management Pack for Windows Server Operating System](https://www.microsoft.com/download/details.aspx?id=9296) - monitors the availability, health, and performance of the Windows Server operating system from version 2003 to 2012 R2.  It includes discovery and monitoring of clustered shared volumes and disks.  

* [Windows Server Failover Cluster](https://www.microsoft.com/download/details.aspx?id=54701) - provides both proactive and reactive monitoring of your Windows Server Failover Cluster deployments hosted on the following versions of the Windows Server operating system:

   * Windows Server 2003 with SP2
   * Windows Server 2003 R2 with SP2
   * Windows 2008 Enterprise and Datacenter edition
   * Windows Server 2008 R2 Enterprise and Datacenter edition
   * Windows Server 2012 and 2012 R2
   * Windows Server 2016. 
  
    It monitors Cluster services components—such as nodes, networks, resources, and resource groups—to report issues that can cause downtime or poor performance. 

As a best practice, you should import the latest version of the Windows Server Management Pack for the operating system you are using. Windows Server Management Packs monitor aspects of the operating system that influence the performance of the computer, such as disk capacity, disk performance, memory utilization, network adapter utilization, and processor performance.

## Configure monitoring of clustered computers 
To begin monitoring computers in a cluster, perform the following steps:  
  
1.  Install an agent on each physical node in the cluster.  This allows Operations Manager to discover all nodes in the cluster and the cluster itself.  
  
2.  Enable agent proxy on all cluster nodes. For more information, see [How to Configure a Proxy for Agentless Monitoring](../../scom/agentless-monitoring-in-operations-manager.md#how-to-configure-a-proxy-for-agentless-monitoring).  
  
When discovery occurs, each physical node of the cluster is displayed in the Operations Manager console in the **Agent Managed** pane; the cluster is displayed in the **Agentless Managed** pane. The cluster may show as "not monitored" if you have not imported the Windows Failover Cluster management pack at a minimum, or depending on what cluster-aware application is deployed in the cluster, such as Microsoft Hyper-V, Exchange Server, or SQL Server.  Once you install the management pack for that workload, you will be able to view additional monitoring information which contains monitors that specifically target the cluster object.  Review the management pack deployment guide to understand what configuration steps are required and what monitoring information is discovered and reported.    

The agent on the active cluster node will perform all monitoring. If the node fails, the agent on the cluster node that clustering fails over to will begin monitoring, but the agent on the failover node will have no awareness of anything the agent on other node had monitored previously, such as alerts, state changes, and so forth. The agents are independent.  
  
> [!NOTE]  
> You might see alerts from **Cluster discovery connect functionality monitor** and **Cluster state connect functionality monitor** when the Action Account uses low privilege credentials. To resolve this problem, assign higher privilege credentials to the Windows Cluster Action Account. For instructions, see the procedure "To modify Run As account properties" in [Managing run as accounts and profiles](../../scom/manage-security-maintain-runas-profiles.md).  
  
