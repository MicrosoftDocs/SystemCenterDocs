---
ms.assetid: 71e6661a-0a00-4817-a5a9-46169bb23e32
title: Virtual Machine Manager Network Object Fundamentals
description: This article describes about network object fundamentals.
author: v-anesh
ms.author: v-anesh
manager: vvithal
ms.date: 04/22/2020
ms.topic: article
ms.prod: system-center
ms.technology: virtual-machine-manager
---

# Virtual Machine Manager network object fundamentals

System Center Virtual Machine Manager (VMM) is part of the System Center suite, used to configure, manage and transform traditional datacenters, and helping to provide a unified management experience across on-premises, service provider, and the Azure cloud.

This topic covers the basics that you need to understand before you move on to more complex topics, such as advanced VMM features and functions, and planning and designing private and public clouds.

The following VMM networking objects are used to build the basic networking infrastructure of Microsoft's Software Defined Networking (SDN) used in private and public clouds:

- [Hosts and host group](host-groups.md)

  Hyper-V hosts that VMM manages, organized into groups based on location or purpose.

- [Logical network](network-logical.md)

  Logical objects that mirror your physicals networks.

  >[!NOTE]
  > The logical network type terminologies (One connected, Independent and Virtualized) are changed for VMM 2019 UR1.

   - [One connected logical network](network-logical-ur1.md)

     A single VM network is created on top of this logical network, and this VM network provides access to all the underlying VLAN-subnet pairs.

     ![Connected network](media/network-logical/connected-network.png)

   - [Independent logical network](network-logical-ur1.md)

     Multiple VM networks can be created on top of this logical network. Each VM network created provides access to a specific VLAN-subnet pair. The VM networks are independent of each other.

     ![Independent network](media/network-logical/independent-network.png)

   - [Virtualized network](network-logical-ur1.md)

     This is the fabric network. Multiple virtualized VM networks can be created on top of this logical network. Each VM network has its own virtualized address space.

     ![Virtualized network](media/network-logical/virtualized-network.png)

- [Network sites](network-virtual.md)

  Logical groupings of hosts, IP Subnets and/or VLANs.

- [IP address pools (logical networks)](network-pool.md#create-a-static-address-pool-for-a-logical-network)

  A static pool of IP addresses used for the associated network sites' IP subnet/VLAN pairs.

- [VM networks](network-virtual.md)

  Abstract objects that act as an interface to logical networks.

- [IP address pools (VM Networks)](network-pool.md#set-up-an-ip-address-pool-on-a-vm-network)

  A static pool of IP addresses for the VM network.

- [Uplink port profile](network-port-profile.md#define-uplink-port-profiles)

  Defines the load balancing algorithm and teaming mode for physical adapters. Uplink port profiles can be applied to physical network adapters when you deploy switches.

- [Virtual network adapter port profile](network-port-profile.md#create-a-virtual-network-adapter-port-profile)

  Defines the virtual network adapter properties for the virtual network adapters available with the logical switch.

- [Port classification](network-port-profile.md#create-port-classifications-for-virtual-network-adapter-port-profiles)

  A label to abstract the virtual network adapter port profile settings.

- [Logical Switch](network-switch.md)

  Brings virtual switch extensions, port profiles, and port classifications together.

- [Gateway](network-gateway.md)

  Used to connect a Hyper-V Network Virtualization (HNV) VM network to an external network.

For more information about Microsoft SDN, see [Software Defined Networking](deploy-sdn.md).


## Next steps

To get started with VMM, see [What's New](whats-new-in-vmm.md) and [Install](install.md).
