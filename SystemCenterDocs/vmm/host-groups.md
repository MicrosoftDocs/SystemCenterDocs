---
ms.assetid: 2d8c7af1-fe96-4901-9d51-90e12bedeaa8
title: Set up host groups in the VMM compute fabric
description: This article describes how to set up host groups in the VMM fabric
author: jyothisuri
ms.author: jsuri
manager: mkluck
ms.date: 11/24/2023
ms.topic: article
ms.prod: system-center
ms.technology: virtual-machine-manager
ms.custom: UpdateFrequency3, engagement-fy24
---

# Set up host groups in the VMM compute fabric

::: moniker range=">= sc-vmm-1801 <= sc-vmm-1807"

[!INCLUDE [eos-notes-virtual-machine-manager.md](../includes/eos-notes-virtual-machine-manager.md)]

::: moniker-end

Read this article to learn about setting up and managing host groups in the System Center - Virtual Machine Manager (VMM) fabric.

A VMM host group is a logical entity that groups fabric resources together. You can group virtual machine hosts or clusters, or create nested host groups. After you've created host groups, you can assign and configure resources at the host group level. Those resources are then applied to all hosts and clusters in the group.

You can create host groups based on different criteria. For example, based on physical location, hardware capabilities, or specific workloads. You can assign permissions for host groups to the VMM admin, delegated administrators, and read-only admin user roles. Members of these user roles can view and manage the fabric resources that are assigned to them at the host group levels. When you create private clouds in VMM, you select which host groups will be included in the cloud, and then allocate resources in the host groups to the cloud.

## Create host groups

1.  Select **Fabric** > **Servers** > **All Hosts** > **Create Host Group**.

2.  Type in a group name. To create a host group at a specific location in the tree, right-click the desired parent node, and then select **Create Host Group**.

After you've created a host group, you can modify the following properties for the group.

**Tab** | **Property**
--- |---
**General** | Configure the host group name, the location in the host group hierarchy, the description, and whether to allow unencrypted BITS file transfers.
**Placement Rules** | VMM automatically identifies the most suitable host to which you can deploy virtual machines. However, you can specify custom placement rules. By default, a host group uses the placement settings from the parent host group.|
**Host Reserves** | Host reserve settings specify the amount of resources that VMM sets aside for the host operating system to use. For a virtual machine to be placed on a host, the host must be able to meet the virtual machine’s resource requirements without using host reserves. You can set host reserves for individual host groups and for individual hosts. The host reserve settings for the root host group, All Hosts, sets the default host reserves for all hosts. You can configure reserve values for the following resources:<br/><br/> CPU<br/><br/> Memory<br/><br/> Disk I/O<br/><br/> Disk space<br/><br/> Network I/O
**Dynamic Optimization** | Configure dynamic optimization and power optimization settings. Dynamic optimization balances the virtual machine's load within a host cluster. Power optimization enables VMM to evacuate hosts of a balanced cluster and turn them off to save power.
**Network** | View inheritance settings, and configure whether to inherit network logical resources from parent host groups. The network logical resources include the following:<br/><br/> IP address pools<br/><br/> Load balancers<br/><br/> Logical networks<br/><br/> MAC address pools
**Storage** | View and allocate storage to a host group.
**Custom Properties** |  Manage custom properties for the following object types:<br/><br/> Virtual machine<br/><br/> Virtual machine template<br/><br/> Host<br/><br/> Host cluster<br/><br/> Host group<br/><br/> Service template<br/><br/> Service instance<br/><br/> Computer tier<br/><br/> Cloud

## Next steps

After you've created host groups, you can deploy [Hyper-V](hyper-v-cluster.md) hosts in the VMM fabric.
