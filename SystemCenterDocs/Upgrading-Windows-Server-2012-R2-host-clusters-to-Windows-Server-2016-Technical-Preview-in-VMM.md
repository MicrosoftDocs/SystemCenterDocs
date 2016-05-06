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
VMM can manage the upgrade of Hyper\-V host clusters in the VMM fabric to [!INCLUDE[winthreshold_server_2](./Token/winthreshold_server_2_md.md)]. You can upgrade the entire cluster, or select specific nodes to upgrade.

Here's what upgrade does:

1.  Creates a template of the node's configuration by combining the appropriate physical computer profile with the node's configuration details and other settings configured in the upgrade wizard.

2.  Migrates the virtual machine workloads off of the node. As a result, the upgrade process does not interrupt the workloads.

3.  Puts the node into maintenance mode, then evicts it from the cluster.

4.  Removes the node from the VMM console. This removes all [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] agents, virtual switch extensions, and so forth from the node.

5.  Provisions the node as a [!INCLUDE[winthreshold_server_2](./Token/winthreshold_server_2_md.md)] server, and configures it according to the saved template.

6.  Brings the node back under [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] management, installing the appropriate agents.

7.  Adds the node back into the cluster, brings it out of maintenance mode, and returns the virtual machine workloads.

    > [!NOTE]
    > As soon as [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] upgrades one node, the cluster enters mixed mode. It continues to function as a [!INCLUDE[winblue_server_2](./Token/winblue_server_2_md.md)] cluster.

When all of the nodes are running [!INCLUDE[winthreshold_server_2](./Token/winthreshold_server_2_md.md)], [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] updates the cluster to a [!INCLUDE[winthreshold_server_2](./Token/winthreshold_server_2_md.md)] cluster.

## Before you start 
Before you start the cluster upgrade, make sure of the following:

-   The cluster must be managed by [!INCLUDE[vmm12short](./Token/vmm12short_md.md)].

-   The cluster must meet the requirements for bare\-metal deployment , except that the physical computer profile does not need to include network or disk configuration details. During the upgrade process, [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] records the node's actual network and disk configuration, and uses that information instead of the corresponding settings in the physical computer profile.
-   You can use this process to upgrade nodes that were not originally provisioned using [!INCLUDE[vmm12short](./Token/vmm12short_md.md)]'s bare\-metal deployment process, as long as those nodes meet the requirements \(such as having a baseboard management controller, or BMC\). You must provide the BMC configuration information to the Cluster Upgrade wizard.
-   The [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] library must contain a VHD configured with [!INCLUDE[winthreshold_server_2](./Token/winthreshold_server_2_md.md)].



