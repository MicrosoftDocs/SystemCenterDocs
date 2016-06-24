---
title: Upgrading Windows Server 2012 R2 host clusters to Windows Server 2016 Technical Preview in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1385aaea-b6cc-408a-9bbc-fbd9a251e48d
---
# Upgrading Windows Server 2012 R2 host clusters to Windows Server 2016 Technical Preview in VMM
VMM can manage the upgrade of Hyper-V host clusters in the VMM fabric to Windows Server Technical Preview. You can upgrade the entire cluster, or select specific nodes to upgrade.

Here's what upgrade does:

1.  Creates a template of the node's configuration by combining the appropriate physical computer profile with the node's configuration details and other settings configured in the upgrade wizard.

2.  Migrates the virtual machine workloads off of the node. As a result, the upgrade process does not interrupt the workloads.

3.  Puts the node into maintenance mode, then evicts it from the cluster.

4.  Removes the node from the VMM console. This removes all VMM agents, virtual switch extensions, and so forth from the node.

5.  Provisions the node as a Windows Server Technical Preview server, and configures it according to the saved template.

6.  Brings the node back under VMM management, installing the appropriate agents.

7.  Adds the node back into the cluster, brings it out of maintenance mode, and returns the virtual machine workloads.

    > [!NOTE]
    > As soon as VMM upgrades one node, the cluster enters mixed mode. It continues to function as a Windows Server 2012 R2 cluster.

When all of the nodes are running Windows Server Technical Preview, VMM updates the cluster to a Windows Server Technical Preview cluster.

## Before you start 
Before you start the cluster upgrade, make sure of the following:

-   The cluster must be managed by VMM.

-   The cluster must meet the requirements for bare-metal deployment , except that the physical computer profile does not need to include network or disk configuration details. During the upgrade process, VMM records the node's actual network and disk configuration, and uses that information instead of the corresponding settings in the physical computer profile.
-   You can use this process to upgrade nodes that were not originally provisioned using VMM's bare-metal deployment process, as long as those nodes meet the requirements (such as having a baseboard management controller, or BMC). You must provide the BMC configuration information to the Cluster Upgrade wizard.
-   The VMM library must contain a VHD configured with Windows Server Technical Preview.



