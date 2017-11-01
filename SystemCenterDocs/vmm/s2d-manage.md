---
ms.assetid: d0f49f22-f145-4147-b66d-3bf384e2ac08
title: Manage Storage Spaces Direct clusters in VMM 2016
description: This article describes how to set up and manage Storage Spaces Direct in the VMM fabric
author:  rayne-wiselman
ms.author: raynew
manager:  carmonm
ms.date:  11/01/2017
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---

# Manage Storage Spaces Direct clusters

>Applies To: System Center 2016 - Virtual Machine Manager

This article explains how to manage Storage Spaces Direct (S2D) clusters in the System Center - Virtual Machine Manager (VMM) fabric.

## Configure cluster settings

You can [view and configure cluster settings](hyper-v-cluster.md#configure-cluster-properties), including cluster status, failure management, and available storage.

## Add a node to a hyper-converged cluster

-	You can [add a new node](hyper-v-cluster.md#add-a-node-to-the-cluster) on a hyper-converged S2D cluster in the VMM fabric. The new node can be an existing Hyper-V server, or a bare-metal physical server.

> [!NOTE]

> Typically, S2D node requires RDMA, QOS and SET settings. To configure these settings for a node using bare metal computers, you can use the post deployment script capability in PCP. Here is the  [sample PCP post deployment script](hyper-v-bare-metal.md#sample-script).

> You can also use this script to configure RDMA, QoS and SET while adding a new node to an existing S2D deployment from bare metal computers. 

-	When you add a new node on a hyper-converged cluster, VMM automatically discovers disks on the new node, and enables S2D.
-	VMM disables maintenance mode on disks, before adding them.

## Control storage resources with QoS

Quality-of-service (QoS) in [Windows Server 2016](https://technet.microsoft.com/windows-server-docs/storage/storage-qos/storage-qos-overview) provides a way to specify minimum and maximum resources that can be assigned to Hyper-V VMs using SOFS storage. QoS mitigates "noisy neighbor" issues, and ensures that a single VM doesn't consume all storage resources.

[Set up QoS policies](sofs-settings.md#set-a-storage-qos-for-an-sofs) for a file server, or for specific virtual disks on the server.
