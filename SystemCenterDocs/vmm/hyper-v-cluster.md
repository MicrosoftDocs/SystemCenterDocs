---
ms.assetid: 9943f491-c585-4330-ab01-89db435fa1a5
title: Manage Hyper-V clusters in the VMM fabric
description: This article describes how to manage Hyper-V clusters in the VMM fabric
author:  rayne-wiselman
ms.author: raynew
manager:  carmonm
ms.date:  10/16/2016
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---

# Manage Hyper-V clusters in the VMM fabric

>Applies To: System Center 2016 - Virtual Machine Manager

Use this article to manage Hyper-V host clusters in the System Center 2016 - Virtual Machine Manager (VMM) fabric. You can configure cluster properties, and manage cluster nodes.


## Configure cluster properties

1. In **Fabric**, right-click the cluster > **Properties**.
2. Configure the settings summarized in the table.

**Tab** | **Settings**
--- |---
**General** | View the name, host group and description. You can also configure the **Cluster reserve \(nodes\)** setting, and view the cluster reserve state.<br /><br/> The **Cluster reserve \(nodes\)** setting specifies the number of node failures a cluster must be able to sustain while still supporting all virtual machines deployed on the host cluster. If the cluster cannot withstand the specified number of node failures and still keep all of the virtual machines running, the cluster is placed in an over\-committed state. When over\-committed, the clustered hosts receive a zero rating during virtual machine placement. An administrator can override the rating and place a highly\-available virtual machine on an over\-committed cluster during a manual placement.
**Status** | View detailed status information for the host cluster:<br/><br/> Cluster validation test runs and successes. Includes a link to the latest validation report \(if available\). Note that accessing the report requires administrative permissions on the cluster node where the report is located.  For host clusters, you can perform an on\-demand cluster validation through VMM. To do this, in the **Fabric** workspace, locate and click the host cluster. Then, on the **Host Cluster** tab, click **Validate Cluster**. Cluster validation begins immediately.<br/><br/>  Online elements in the cluster: cluster core resources, disk witness in quorum, and the cluster service on each node.
**Available Storage** | Shows available storage, that is, storage logical units that are assigned to the host cluster but are not Cluster Shared Volumes \(CSV\).<br/><br/> You can also do the following:<br/><br/> Add and remove storage logical units that are managed by [VMM.<br/><br/> Convert available storage to shared storage \(CSV\).
**Shared Volumes** | Shows the shared volumes \(CSVs\) that are allocated to the host cluster. You can also do the following:<br/><br/> Add and remove CSVs that are managed by VMM. <br/><br/> Convert CSVs to available \(non\-CSV\) storage.|
**Custom Properties** | Custom properties that you manage.

## Add a node to the cluster

1. If you already used Failover Cluster Manager to add the node, then in **Fabric** > **Servers** > **All Hosts**, right-click the host with a **Pending** status, and click **Add to Host Cluster**.
2. If you didn't add the node with the Failover Cluster Manager, you can add hosts that are already managed by VMM. In **Fabric** > **Servers** > **All Hosts**, right-click the cluster > **Add Cluster Node**. In the Add Nodes Wizard > **Resource Type**, select the RunAs account that will be used to add the nodes. Make sure **Existing servers running a Windows Server operating system** is selected. In **Select Hosts** select the Hyper-V host server that you want to add. Finish the wizard and verify the settings.

## Remove a node from the cluster

1. Click **Fabric** > **Servers** > **All Hosts**.
2. Locate the cluster node you want to remove and view the status in the **Hosts** pane.
3. If the node isn't in maintenance mode click Start Maintenance Mode. Click **Move all virtual machines to other hosts in the cluster** and verify the status.
4. Right-click the host > **Remove Cluster Node** > **Yes**. During the job to remove the node any shared storage is unregistered from the node. If you manage storage outside VMM then you should unregister the storage from the node.

## Uncluster a cluster

Remove a host cluster as follows:

1. Click **Fabric** > **Servers** > **All Hosts**.
2. Make sure the cluster isn't supporting any highly-available VMs or clustered services/apps.
3. Right-click the host cluster > **Uncluster**. Click **Yes** to continue.
4. During the job to remove the cluster any shared storage is unregistered from the cluster nodes. If you manage storage outside VMM, then you should unregister the storage.
