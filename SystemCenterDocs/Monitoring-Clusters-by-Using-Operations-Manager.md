---
title: Monitoring Clusters by Using Operations Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6842cddc-b875-4358-8f00-f4b8ab784739
---
# Monitoring Clusters by Using Operations Manager
The purpose of this topic is to explain how to use [!INCLUDE[om12long](./Token/om12long_md.md)] to monitor computers that are in clustered configurations. For information on monitoring clustering services, see the guide for the management pack you are using, such as [Windows Server 2003 Cluster Management Pack Guide](http://go.microsoft.com/fwlink/p/?LinkID=120674) or [Windows Server Failover Cluster Management Pack Guide](http://go.microsoft.com/fwlink/p/?LinkId=239811).

To begin monitoring computers in a cluster, perform the following steps:

1.  Install an agent on all cluster nodes \(computers\).

2.  Enable agent proxy on all cluster nodes. For more information, see [How to Configure a Proxy for Agentless Monitoring](./How-to-Configure-a-Proxy-for-Agentless-Monitoring.md).

In the **Administration** workspace, cluster nodes will be displayed in **Agent Managed**, and the cluster will be displayed in **Agentless Managed**. The cluster will show as “not monitored” unless a management pack contains monitors that specifically target the cluster object. The agent on the active cluster node will perform all monitoring. If the node fails, the agent on the cluster node that clustering fails over to will begin monitoring, but the agent on the failover node will have no awareness of anything the agent on other node had monitored previously, such as alerts, state changes, and so forth. The agents are independent.

When you are monitoring virtual servers on a cluster, you must deploy agents to the cluster nodes, configure them to be managed as a proxy, and then monitor the virtual servers as you would monitor an agentless\-managed computer.

The Windows Server Operating System Management Pack provides discovery and monitoring of cluster shared volumes.

> [!NOTE]
> You might see alerts from **Cluster discovery connect functionality monitor** and **Cluster state connect functionality monitor** when the Action Account uses low privilege credentials. To resolve this problem, assign higher privilege credentials to the Windows Cluster Action Account. For instructions, see the procedure “To modify Run As account properties” in [How to Create a Run As Account](./How-to-Create-a-Run-As-Account.md).

## See Also
[Operations Manager Monitoring Scenarios](./Operations-Manager-Monitoring-Scenarios.md)
[Integrating Active Directory and Operations Manager](./Integrating-Active-Directory-and-Operations-Manager.md)
[Connecting Operations Manager With Other Management Systems](./Connecting-Operations-Manager-With-Other-Management-Systems.md)
[Collecting Security Events Using Audit Collection Services in Operations Manager](./Collecting-Security-Events-Using-Audit-Collection-Services-in-Operations-Manager.md)
[Monitoring UNIX and Linux Computers by Using Operations Manager](./Monitoring-UNIX-and-Linux-Computers-by-Using-Operations-Manager.md)
[Monitoring .NET Applications](./Monitoring-.NET-Applications.md)
[Monitoring Service Level Objectives by Using Operations Manager](./Monitoring-Service-Level-Objectives-by-Using-Operations-Manager.md)
[Monitoring Networks by Using Operations Manager](./Monitoring-Networks-by-Using-Operations-Manager.md)
[Monitoring Operations Manager from a Second Management Group](./Monitoring-Operations-Manager-from-a-Second-Management-Group.md)
[Client Monitoring Using Agentless Exception Monitoring in Operations Manager](./Client-Monitoring-Using-Agentless-Exception-Monitoring-in-Operations-Manager.md)
[Monitoring Across Untrusted Boundaries in Operations Manager](./Monitoring-Across-Untrusted-Boundaries-in-Operations-Manager.md)
[Agentless Monitoring in Operations Manager](./Agentless-Monitoring-in-Operations-Manager.md)


