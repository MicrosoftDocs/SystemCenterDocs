---
ms.assetid: d0f49f22-f145-4147-b66d-3bf384e2ac08
title: Manage Storage Spaces Direct clusters in VMM
description: This article describes how to set up and manage Storage Spaces Direct in the VMM fabric.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 08/22/2024
ms.topic: concept-article
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: UpdateFrequency2, engagement-fy24
ms.update-cycle: 1095-days
---

# Manage Storage Spaces Direct clusters



This article explains how to manage Storage Spaces Direct (S2D) clusters in the System Center Virtual Machine Manager (VMM) fabric.

## Configure cluster settings

You can [view and configure cluster settings](hyper-v-cluster.md#configure-cluster-properties), which include cluster status, failure management, and available storage.

## Add a node to a hyper-converged cluster

You can [add a new node](hyper-v-cluster.md#add-a-node-to-the-cluster) on a hyper-converged S2D cluster in the VMM fabric. The new node can be an existing Hyper-V server or a bare-metal physical server.

> [!NOTE]
> Typically, S2D node requires Remote Direct Memory Access (RDMA), Quality of Service (QoS), and switch embedded teaming (SET) settings. To configure these settings for a node using bare-metal computers, you can use the post-deployment script capability in the physical computer profile (PCP). Here's the [sample PCP post-deployment script](hyper-v-bare-metal.md#sample-script).
> You can also use this script to configure RDMA, QoS, and SET when you add a new node to an existing S2D deployment from bare-metal computers.

-    When you add a new node on a hyper-converged cluster, VMM automatically discovers disks on the new node and enables S2D.
-    VMM disables maintenance mode on disks before adding them.

## Control storage resources with QoS

Quality of Service in [Windows Server](/windows-server/storage/storage-qos/storage-qos-overview) provides a way to specify minimum and maximum resources that can be assigned to Hyper-V VMs using scale-out file share storage. QoS mitigates *noisy neighbor* issues and ensures that a single VM doesn't consume all storage resources.

[Set up QoS policies](sofs-settings.md#set-a-storage-qos-for-a-sofs) for a file server or for specific virtual disks on the server.


::: moniker range="sc-vmm-2019"

>[!NOTE]
>The following feature is applicable from VMM 2019 UR1.

::: moniker-end

::: moniker range=">=sc-vmm-2019"

## Configure DCB settings on S2D clusters

With the advent of converged networking, organizations are using Ethernet as a converged network for their management and storage traffic. It's important for Ethernet networks to support a similar level for performance and losslessness compared to that of dedicated fiber channel networks. This similar level of support becomes more important when the use of S2D clusters is considered.

RDMA, in conjunction with data center bridging (DCB), helps to achieve a similar level of performance and losslessness in an Ethernet network compared to fiber channel networks.

The DCB settings must be consistent across all the hosts and the fabric network (switches). A misconfigured DCB setting in any one of the host or fabric devices is detrimental to the S2D performance.

To configure a DCB setting, use [this procedure](s2d-hyper-converged.md#step-3-configure-dcb-settings-on-the-s2d-cluster).

::: moniker-end

## Next steps

[Set storag3 QoS for clusters](./qos-storage-clusters.md)
