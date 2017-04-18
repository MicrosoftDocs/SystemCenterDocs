---
ms.assetid: 5a960834-3382-437d-a0bf-d09654726ab0
title: Set up the VMM networking fabric
description: This article describes how to set up infrastructure servers in the VMM fabric
author:  rayne-wiselman
ms.author: raynew
manager:  cfreeman
ms.date:  10/16/2016
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---


# Set up the VMM networking fabric

>Applies To: System Center 2016 - Virtual Machine Manager


This article provides an overview of setting up the System Center 2016 - Virtual Machine Manager (VMM) networking fabric.

Here's what you'll typically do to set up networking in the VMM fabric:

1. [Set up logical networks](manage/manage-network-logical-networks.md): Create logical networks that maps to your physical networks. You can create network sites that map to network sites in your physical network. For example IP subnets, VLNS, or subnet/VLAN pairs. Then if you're not using DHCP you create IP address pools for the network sites that exist within your physical networks.
2. [Create VM networks](manage/manage-network-vm-networks.md): Create VM networks that map to network sites that exist within your physical networks.
3. [Set up IP address pools](manage/manage-network-static-address-pools.md): Create address pool to allocate static IP addresses. You'll need to configure pools for logical networks, and in some circumstances for VM networks too.
4. [Add a gateway](manage/manage-network-gateway.md): You might need to set up network virtualization gateways in the VMM networking fabric. By default, if you're using isolated VM networks in your VMM fabric, VMs associated with a network can only connect to machines in the same subnet. If you want to connect VMs further than the subnet you'll need a gateway.
5. [Create port profiles](manage/manage-network-port-profiles.md): Create uplink port profiles that indicates to VMM which networks a host can connect to on a specific network adapter. If required create virtual port profiles to specify settings that should be applied to virtual network adapters. You can create custom port classifications to abstract virtual port profiles.
6. [Configure logical switches](manage/manage-network-logical-switches.md): Create a logical switch, apply it to a host and select the network adapters on the host that you want to bind to the switch. When you apply the switch networking settings will be applied to the host.
