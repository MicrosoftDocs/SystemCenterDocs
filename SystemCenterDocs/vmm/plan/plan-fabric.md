---
ms.assetid: 9fe8955d-cf4b-483f-b037-494c41207a77
title: Plan the VMM fabric
description: This article provides planning information for the VMM fabric
author:  rayne-wiselman
ms.author: raynew
manager:  cfreemanwa
ms.date:  10/16/2016
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---


# Plan the VMM fabric

>Applies To: System Center 2016 - Virtual Machine Manager

The System Center 2016 - Virtual Machine Manager (VMM) fabric is an abstracted collection of resources that can be discovered, identified, and managed.  

-   **Compute**: Resources in the compute fabric include virtualization servers (Hyper-V and VMware), VMs, and infrastructure services such as  pre-boot execution environment (PXE) servers to handle bare-metal deployment of Hyper-V host servers, and update servers.
-   **Network**: The network fabric includes VMM networks, load balancers, and gateways.
-   **Storage**: The storage fabric includes storage arrays, file servers, and storage pools.


This article summarizes planning steps you should perform before you set up components in VMM fabric.

## Plan the compute fabric

In the compute fabric you set up all the servers and computers that will be managed in the VMM fabric. It includes the VMM library, virtualization hosts and VMs, and infrastructure servers, including update servers, IPAM servers, and PXE servers used for bare metal deployment.

[Learn more](../plan-compute.md) about planning the compute fabric.


## Plan the networking fabric

In the networking fabric you:

1. **Set up logical networks and IP addressing**: Create logical networks that maps to your physical networks. You can create network sites that map to network sites in your physical network. For example IP subnets, VLNS, or subnet/VLAN pairs. Then if you're not using DHCP you create IP address pools for the network sites that exist within your physical networks.
2. **Create VM networks**: Create VM networks that map to network sites that exist within your physical networks.
4. **Create port profiles**: Create uplink port profiles that indicates to VMM which networks a host can connect to on a specific network adapter. If required create virtual port profiles to specify settings that should be applied to virtual network adapters.
5. **Create custom port classifications**: If you created a custom virtual port profile you'll probably want to create a custom port classification to abstract it.
6. **Configure logical switches**: Create a logical switch, apply it to a host and select the network adapters on the host that you want to bind to the switch. When you apply the switch networking settings will be applied to the host.

[Learn more](../plan-network.md) about planning the networking fabric

## Plan the storage fabric

VMM supports block and file-based storage. In the VMM storage fabric you discover, configure, and assign storage. You can use storage as a factor in VM placement, so that when a user deploys a VM, VMM checks the VM template or cloud settings for an assigned storage classification. When VMM rates potential VM hosts, it prioritizes hosts that have available storage with the appropriate classification. VMM also identifies the most efficient process for transferring a VM VHD file from the library to an appropriate storage resource, based on the technologies that the storage type uses. For example if a SAN supports Windows Offloaded Data Transfers (ODX) then VMM will use ODX for the transfer.

When planning the storage fabric consider the following:

-   Decide how you  want to provision storage in the fabric? You can add existing storage devices and servers, create a scale-out file server from existing Windows servers, or deploy file storage from bare metal computers.
-   Plan storage classifications. You can create storage classifications before you add storage, or during the add process. When you plan your classification you'll know which classification to add to each storage pool.
-   You can plan classifications based around storage type, or location. For example you could create the following classifications:

    -   Bldg1Gold: A set of solid-state drives (SSDs) that you will make available to users in building 1.
    -   Bldg1Silver: A set of SSDs and hard disk drives (HDDs) that you will make available to users in building 1
    -   Bldg2Gold: A set of SSDs that you will make available to users in building 2.
    -   Bldg2Silver: A set of SSDs and HDDs that you will make available to users in building 2.

-   You can map storage classifications to block storage and file shares.

## Next steps

- [Manage Hyper-V hosts and clusters](../hyper-v-hosts.md)
- [Manage the networking fabric](../manage-networks.md)
- [Manage the storage fabric](../manage-storage.md)
