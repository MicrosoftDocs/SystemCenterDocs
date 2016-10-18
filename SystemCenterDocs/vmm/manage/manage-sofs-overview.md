---
ms.assetid: 0faa4dae-5d87-4e43-bc68-dfe3c6ffe0f4
title: Manage SOFS in the VMM fabric
description: This article describes how to manage SOFS in the VMM fabric
author:  rayne-wiselman
ms.author: raynew
manager:  cfreeman
ms.date:  10/16/2016
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---

# Manage scale-out file server (SOFS) in the VMM fabric

>Applies To: System Center 2016 - Virtual Machine Manager

Scale-out file server (SOFS) is a file server deployed as an active/active cluster based on SMB 3.0. Using an SOFS cluster provides supplies apps with the bandwidth of all nodes in the cluster. All nodes in the cluster accept SMB requests, providing continuous availability and transparent failover if a node goes down.

You can add and manage SOFS clusters in the System Center 2016 - Virtual Machine Manager (VMM) fabric. There are a number of ways you can add an SOFS cluster. You can add an existing SOFS cluster to the fabric,  provision an SOFS cluster from existing Windows machines in the fabric, or provision a cluster from bare metal computers.

- [Perform a rolling upgrade of an SOFS cluster](manage-sofs-rolling-upgrade.md)
- [Add an existing SOFS to the VMM storage fabric](manage-sofs-add-existing.md)
- [Create an SOFS cluster from standalone servers in the VMM fabric](manage-sofs-standalone-server.md)
- [Provision SOFS from bare-metal computers](manage-sofs-bare-metal.md)
