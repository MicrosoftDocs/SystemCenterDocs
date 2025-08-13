---
ms.assetid: 0faa4dae-5d87-4e43-bc68-dfe3c6ffe0f4
title: Manage SOFS in the VMM Fabric
description: This article describes how to manage SOFS in the VMM fabric
author: jyothisuri
ms.author: jsuri
ms.date: 04/09/2025
ms.topic: concept-article
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: UpdateFrequency2, engagement-fy24
---

# Manage scale-out file server (SOFS) in the VMM fabric



Scale-out file server (SOFS) is a file server deployed as an active/active cluster based on SMB 3.0. Using a SOFS cluster provides apps with the bandwidth of all nodes in the cluster. All nodes in the cluster accept SMB requests, providing continuous availability and transparent failover if a node goes down.

You can add and manage SOFS clusters in the System Center Virtual Machine Manager (VMM) fabric. There are many ways you can add a SOFS cluster. You can add an existing SOFS cluster to the fabric, provision a SOFS cluster from the existing Windows machines in the fabric, or provision a cluster from bare metal computers.

- [Perform a rolling upgrade of an SOFS cluster](sofs-rolling-upgrade.md).
- [Add an existing SOFS to the VMM storage fabric](sofs-existing.md).
- [Create an SOFS cluster from standalone servers in the VMM fabric](sofs-cluster.md).
- [Provision SOFS from bare-metal computers](sofs-bare-metal.md).
