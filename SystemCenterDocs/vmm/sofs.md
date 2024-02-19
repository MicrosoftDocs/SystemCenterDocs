---
ms.assetid: 0faa4dae-5d87-4e43-bc68-dfe3c6ffe0f4
title: Manage SOFS in the VMM fabric
description: This article describes how to manage SOFS in the VMM fabric
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 02/19/2024
ms.topic: article
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: UpdateFrequency2, engagement-fy24
---

# Manage scale-out file server (SOFS) in the VMM fabric

::: moniker range=">= sc-vmm-1801 <= sc-vmm-1807"

[!INCLUDE [eos-notes-virtual-machine-manager.md](../includes/eos-notes-virtual-machine-manager.md)]

::: moniker-end

Scale-out file server (SOFS) is a file server deployed as an active/active cluster based on SMB 3.0. Using an SOFS cluster provides apps with the bandwidth of all nodes in the cluster. All nodes in the cluster accept SMB requests, providing continuous availability and transparent failover if a node goes down.

You can add and manage SOFS clusters in the System Center - Virtual Machine Manager (VMM) fabric. There are many ways you can add an SOFS cluster. You can add an existing SOFS cluster to the fabric, provision an SOFS cluster from the existing Windows machines in the fabric, or provision a cluster from bare metal computers.

- [Perform a rolling upgrade of an SOFS cluster](sofs-rolling-upgrade.md).
- [Add an existing SOFS to the VMM storage fabric](sofs-existing.md).
- [Create an SOFS cluster from standalone servers in the VMM fabric](sofs-cluster.md).
- [Provision SOFS from bare-metal computers](sofs-bare-metal.md).
