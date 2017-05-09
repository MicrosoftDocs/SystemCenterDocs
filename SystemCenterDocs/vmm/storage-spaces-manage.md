---
ms.assetid: 9d758a26-a2dd-42f0-87a6-eafbbb8a2dbf
title: Manage storage deployed with Storage Spaces Direct in the VMM 2016 fabric
description: This article describes how to manage storage in Storage Spaces Direct in the VMM fabric
author:  rayne-wiselman
ms.author: raynew
manager:  cfreeman
ms.date:  05/07/2017
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---

# Manage storage in Storage Spaces Direct in the VMM fabric

>Applies To: System Center 2016 - Virtual Machine Manager

This article describes how to manage storage deployed with Storage Spaces Direct (S2D) in the System Center 2016 - Virtual Manager (VMM) fabric.


## Set up QoS policies

Quality-of-service (QoS) in [Windows Server 2016](https://technet.microsoft.com/en-us/windows-server-docs/storage/storage-qos/storage-qos-overview) provides a way to specify minimum and maximum resources that can be assigned to Hyper-V VMs using SOFS storage. QoS mitigates "noisy neighbor" issues, and ensure that a single VM doesn't consume all storage resources. [Learn more](manage-sofs-qos.md) about setting up QoS policies for a file server, or for specific virtual disks on the server.

## Add and remove nodes and disks

- You can add a new node on a hyper-converged S2D cluster in VMM, in the same way that you [add a node on any cluster](hyper-v-cluster.md#add-a-node-to-the-cluster). The new node can be an existing Hyper-V server, or a bare-metal physical server.
- When you add a new node on a hyper-converged cluster, VMM automatically discovers disks on the new node, and enables S2D.
- If you [remove a node](hyper-v-cluster.md#remove-a-node-from-the-cluster), VMM removes disks.

## Next steps

Learn about [allocating storage](hyper-v-storage.md) to Hyper-V hosts and clusters
