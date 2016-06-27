---
title: Upgrading Windows Server 2012 R2 Scale-Out File Servers to Windows Server 2016 Technical Preview in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b19bb05-8657-41d4-b355-6d48c3c2d255
---
# Upgrading Windows Server 2012 R2 Scale-Out File Servers to Windows Server 2016 Technical Preview in VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

When you use VMM to manage Windows Server 2012 R2 Scale-Out File Servers, you can use VMM to upgrade the cluster operating systems to Windows Server Technical Preview. VMM uses its capabilities to live-migrate virtual machines, manage and maintain nodes, and provision nodes from bare metal to automate the process of upgrading a Scale-Out File Server. You can upgrade the entire Scale-Out File Server, or select specific nodes to upgrade.

During the upgrade process, VMM performs the following operations on each selected node:

1.  Creates a template of the node's configuration by combining the appropriate physical computer profile with the node's configuration details and other settings configured in the upgrade wizard.

2.  Migrates the virtual machine workloads off of the node. As a result, the upgrade process does not interrupt the workloads.

3.  Puts the node into maintenance mode, then evicts it from the cluster.

4.  Removes the node from VMM management (this step removes all VMM agents, virtual switch extensions, and so forth from the node).

5.  Provisions the node as a Windows Server Technical Preview server, and configures it according to the saved template.

6.  Brings the node back under VMM management, installing the appropriate agents.

7.  Adds the node back into the cluster, brings it out of maintenance mode, and returns the virtual machine workloads.

    > [!NOTE]
    > As soon as VMM upgrades one node, the Scale-Out File Server enters mixed mode. It continues to function as a Windows Server 2012 R2 Scale-Out File Server.

When all of the nodes are running Windows Server Technical Preview, VMM updates the Scale-Out File Server to a Windows Server Technical Preview Scale-Out File Server.

## Prerequisites
Before you use the cluster upgrade process, make sure of the following:

-   The Scale-Out File Server must be managed by VMM.

-   The Scale-Out File Server must meet the requirements for bare-metal deployment as listed in [Prerequisites: creating Scale-Out File Servers from bare metal with VMM](Prerequisites--creating-Scale-Out-File-Servers-from-bare-metal-with-VMM.md), except that the physical computer profile does not need to include network or disk configuration details.

    During the upgrade process, VMM records the node's actual network and disk configuration, and uses that information instead of the corresponding settings in the physical computer profile.

    > [!NOTE]
    > You can use this process to upgrade nodes that were not originally provisioned using VMM's bare-metal deployment process, as long as those nodes meet the requirements (such as having a baseboard management controller, or BMC). You must provide the BMC configuration information to the Cluster Upgrade wizard.

-   The VMM library must contain a VHD configured with Windows Server Technical Preview.

## In this section
To upgrade all nodes in a Scale-Out File Server and update the Scale-Out File Server's functional level, see [How to upgrade a Scale-Out File Server to Windows Server Technical Preview](How-to-upgrade-a-Scale-Out-File-Server-to-Windows-Server-Technical-Preview.md).

To update the functional level of an existing Scale-Out File Server of upgraded nodes (for example, if you upgraded the Scale-Out File Server nodes outside of VMM), see [How to update the cluster functional level of a Scale-Out File Server that was upgraded outside of VMM](How-to-update-the-cluster-functional-level-of-a-Scale-Out-File-Server-that-was-upgraded-outside-of-VMM.md).

## See Also
[Managing Scale-Out File Servers with VMM](Managing-Scale-Out-File-Servers-with-VMM.md)
[Managing storage resources and capacity with VMM](Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)



