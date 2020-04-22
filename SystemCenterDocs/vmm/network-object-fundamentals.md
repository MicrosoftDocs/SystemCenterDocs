---
ms.assetid: 71e6661a-0a00-4817-a5a9-46169bb23e32
title: Virtual Machine Manager Network Object Fundamentals
description: This article describes about network object fundamentals.
author: v-anesh
ms.author: v-anesh
manager: vvithal
ms.date: 04/21/2020
ms.topic: article
ms.prod: system-center
ms.technology: virtual-machine-manager
---

# Virtual Machine Manager network object fundamentals

System Center Virtual Machine Manager (VMM) is an essential tool used to deploy Microsoft private and public clouds. But before you begin building clouds, it is important to understand the fundamental networking objects in VMM. These networking objects form the network infrastructure of your cloud, including the virtual networks that you or your tenants create.

If you're new to VMM, all the new terms and concepts can be a little confusing at first. This topic covers just the basics that you need to understand before you move on to more complex topics, such as advanced VMM features and functions, and planning and designing private and public clouds.

The following VMM networking objects are used to build the basic networking infrastructure of Microsoft's Software Defined Networking (SDN) used in private and public clouds:

- [Hosts and host groups](host-groups.md)

  Hyper-V hosts that VMM manages organized into groups based on location or purpose.

- [Logical networks](network-logical.md)

  Logical objects that mirror your physicals networks.

- [Network sites](network-virtual.md)

  Logical groupings of hosts, IP Subnets and/or VLANs.

- [IP address pools (logical networks)](network-pool.md#create-a-static-address-pool-for-a-logical-network)

  A static pool of IP addresses used for the associated network sites' IP subnet/VLAN pairs.

- [VM networks](network-virtual.md)

  Abstract objects that act as an interface to logical networks.

- [IP address pools (VM Networks)](network-pool.md#set-up-an-ip-address-pool-on-a-vm-network)

  A static pool of IP addresses for the VM network.

- [Logical Switch](network-switch.md)

  A template used to create virtual switches consistently across many hosts.

- [Uplink port profiles](network-port-profile.md)

  Defines the load balancing algorithm for an adapter, and specify how to team multiple network adapters on a host that use the same uplink port profile.

- [Virtual network adapter port profiles](network-port-profile.md#create-a-virtual-network-adapter-port-profile)

  Define the virtual network adapter properties for the virtual network adapters available with the logical switch.

- [Port classifications](network-port-profile.md#create-port-classifications-for-virtual-network-adapter-port-profiles)

  A label to abstract the adapter port profile settings.

- [Gateways](network-gateway.md)

  Used to connect a Hyper-V Network Virtualization (HNV) VM network to an external network.

For more information about Microsoft SDN, see [Software Defined Networking](deploy-sdn.md).


## See Also

- [Build Your Own Cloud: What You Need to Know](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/mt156973(v%3Dws.11))
- [Preparing the Fabric in VMM](plan-compute.md)
