---
ms.assetid: 0d6b7084-67fb-4612-8270-68d3de89f79d
title: Manage VMM
description: This article provides an overview of working with VMM after you've finished installation.
author:  rayne-wiselman
ms.author: raynew
manager:  cfreeman
ms.date:  10/16/2016
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---


# Manage VMM

>Applies To: System Center 2016 - Virtual Machine Manager

After you've finished installing System Center 2016 - Virtual Machine Manager (VMM) you can start setting up your management infrastructure.


## Manage the VMM compute fabric

- **Manage the VMM library**: The VMM library consists of one or more file shares that contain VMM resources. You interact with the library by adding file-based resources such as virtual hard disks, configuring templates and profiles that are used to provision VMs and services, setting up private cloud shares, storing VMs, and providing a location for self-service users to upload their own resources. [Get started](../manage-library-server.md).
- **Manage VMM host groups**: You set up VMM host groups as logical entities to group virtualization hosts together. You then assign and configuring resources at the host group level. [Get started](../host-groups.md).
- **Manage Hyper-V hosts and clusters**: You can manage your Hyper-V infastructure in the VMM compute fabric. You can add existing servers (including Nano server) and provision them with the Hyper-V role if required. You can create a Hyper-V cluster from existing standalone Hyper-V hosts, or provision a Hyper-V host or cluster from bare metal. You can also keep your Hyper-V clusters up-to-date with rolling upgrades. [Get started](../hyper-v-hosts.md).
- **Manage VMware servers**: You can add and manage VMware vCenter servers and vSphere hosts in the VMM compute fabric. You can manage day-to-day operations, including the host discovery and management, and VM provisioning. [Get started](../manage-vmware-hosts.md).
- **Manage infrastructure servers**: You can add infrastructure servers that are used by VMM for provisioning and networking. For example PXE servers and IPAM servers. You can also add other servers such as Active Directory, DNS, and DHCP, so that you can manage and update all of these servers from the same location. [Get started](../infrastructure-server.md).

## Manage the VMM networking fabric

 - **Manage logical networks**: You create logical networks that map to, and represent, your physical networks. You assign logical network settings that match the mapped physical network, including the network type, the associated network sites, and [static address pools](../network-pool.md) if relevant. [Get started](../network-logical.md).
 - **Manage VM networks**: VM networks are abstract objects that act as an interface to logical networks. A logical network that's isolated can have multiple VM networks associated with it, thus allowing you to use each VM network for a different purpose. [Get started](../network-virtual.md).
 - **Manage network virtualization gateways**: If you're using isolated VM networks, the VMs in that network can only connect to machines in the same subnet. If you want to connect further you set up network virtualization gateways. [Learn more](../network-gateway.md).
 - **Manage port profiles**: You set up uplink port profiles that define load balancing and teaming, and apply them to physical network adapters. You configure virtual network adapter port profiles with capabilities such as bandwidth limitations and priority, and apply them to virtual network adapters. [Get started](../network-port-profile.md).
 - **Manage logical switches**: Logical switches bring together network settings that can be applied to network adapters, so that you have consistent adapter settings across multiple hosts. You set up virtual switch extensions, port profiles, and port classifications, and define them in a logical switch. [Get started](../network-switch.md).
 - **Manage SDN**: You can define a Software Defined Network (SDN) infrastructure in the VMM networking fabric. As part of the infrastructure you set up a Network Controller, Software Load Balancer, and RAS Gateway.

## Manage the VMM storage fabric

 VMM can manage storage that you assign to virtual hosts, clusters, and virtual machines. [Learn more](../manage-storage.md).

 - **Manage storage classifications**: Storage classifications abstract storage devices, so that you can group together devices with similar characteristics. You can then assign classifications rather than specific storage devices to hosts and clusters. [Get started](../storage-classification.md).
 - **Add storage devices**: To manage storage you need to discover and add it to the VMM storage fabric. [Get started](../storage-device.md).
 - **Allocate storage to host groups**: After storage has been discovered and classified you can assign it to a host groups. You can assign an entire storage pool, or a specific logical unit (LUN). [Get started](../storage-host-group.md).
 - **Set up a Microsoft iSCSI Target server**: Microsoft iSCSI Target Server is a server role that enables a Windows server machine to function as a storage device. You can add and manage this server as storage in the VMM fabric. [Get started](../storage-iscsi.md).
 - **Set up Virtual fibre channel**: Virtual fibre channel provides Hyper-V VMs with direct access to Fibre Channel SAN storage, so that you can virtualize applications and workloads that require direct access to SAN logical unit numbers (LUNs). VM failover clusters can also access fibre channel SAN arrays. You can add virtual fibre channel storage to the VMM fabric. [Get started](../storage-fibre-channel.md).
 - **Set up file storage**: VMM can use file storage that supports SMB 3.0. To use file shares for storage, you add file shares to the VMM fabric, and assign them to Hyper-V hosts and clusters. [Get started](../storage-file.md).
 - **Set up SOFS**: Scale-out file server (SOFS) is a file server deployed as an active/active cluster based on SMB 3.0ת, and providing continuous availability and transparent failover if a node goes down. You can add and manage SOFS clusters in the VMM fabric. [Get started](manage-sofs-overview.md).
 - **Set up Storage Spaces Direct**:  Storage Spaces Direct enables you to build highly available storage systems with local storage. Storage can be leveraged by VMs on the same cluster, or exported as a file share. [Get started](../s2d.md).
 - **Set up Storage Replica**: Storage Replica enables storage-agnostic, block-level, synchronous replication between clusters or servers for disaster preparedness and recovery. You can leverage Storage Replica to replicate Hyper-V cluster data or file data in the VMM fabric. [Get started](manage-storage-replica.md).
