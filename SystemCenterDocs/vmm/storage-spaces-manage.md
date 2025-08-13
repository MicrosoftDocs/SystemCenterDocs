---
ms.assetid: 9d758a26-a2dd-42f0-87a6-eafbbb8a2dbf
title: Manage storage deployed with Storage Spaces Direct in the VMM fabric
description: This article describes how to manage storage in Storage Spaces Direct in the VMM fabric
author: jyothisuri
ms.author: jsuri
ms.date: 04/24/2023
ms.topic: concept-article
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: UpdateFrequency2, engagement-fy23
---

# Manage storage in Storage Spaces Direct in the VMM fabric



This article describes how to manage storage deployed with Storage Spaces Direct (S2D) in the System Center - Virtual Manager (VMM) fabric.


## Set up QoS policies

Quality-of-service (QoS) in [Windows Server](/windows-server/storage/storage-qos/storage-qos-overview) provides a way to specify the minimum and maximum resources that can be assigned to Hyper-V VMs using SOFS storage. QoS mitigates **noisy neighbor** issues, and ensure that a single VM doesn't consume all the storage resources. [Learn more](manage-sofs-qos.md) about setting up QoS policies for a file server or for specific virtual disks on the server.

## Add and remove nodes and disks

- You can add a new node on a hyper-converged S2D cluster in VMM in the same way that you [add a node on any cluster](hyper-v-cluster.md#add-a-node-to-the-cluster). The new node can be an existing Hyper-V server or a bare-metal physical server.
- When you add a new node on a hyper-converged cluster, VMM automatically discovers disks on the new node and enables S2D.
- If you [remove a node](hyper-v-cluster.md#remove-a-node-from-the-cluster), VMM removes disks.

## Next steps

Learn about [allocating storage](hyper-v-storage.md) to Hyper-V hosts and clusters.
