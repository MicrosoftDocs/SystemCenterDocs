---
title: Set up logical networks in the VMM fabric
description: This article describes how to set up logical networks in the VMM fabric
author:  rayne-wiselman
ms.author: raynew
manager:  cfreemanwa
ms.date:  2016-09-22
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---

# Set up logical networks in the VMM fabric

>Applies To: System Center 2016  - Virtual Machine Manager

Read this article to learn how to create System Center 2016 - Virtual Machine Manager (VMM) logical networks.

## Overview

There are different types of networks in most organizations, including corporate networks, management networks, and others. These networks might be isolated physically or virtually using network virtualization and virtual LANs (VLANs). In VMM each of these networks is defined as a logical network. Logical networks are logical objects that mirror your physicals networks and are used to model your VMM network fabric.

When you create logical networks to model your environment you assign them properties that match your physical environment. You specify the type of network, the network sites associated with the logical network, and static address pools if you're not using DCHP to assign IP addresses to VMs you create in the network sites.

When you provision virtualization hosts in the VMM fabric, you associate physical adapters on those hosts with logical networks.

## Before you start

- **Automatic logical networks**: By default, VMM creates logical networks automatically. When you provision a host in the VMM fabric and there's no VMM logical network associated with a physical network adapter on that host, VMM automatically creates a logical network and associates it with an adapter. By default for the logical network VMM first DNS suffix label of the connection-specific DNS suffix. By default VMM also creates a VM network configured with **No isolation**.
- **Manual logical networks**: When you create a logical network manually you specify:
	- **Network type**: You specify whether the network is isolated or not, and if it is how it's isolated. Then when you create VM networks based on the logical network they'll be created with the type of network you specified.
		- **No isolation**: This is the simplest type of network model that specifies there's just a single network within which machines can connect to each other with no need to isolate these machines from each other. VM networks in VMM provide an interface through which VMs connect to a logical network, and in a no isolation model you'll have a single VM network mapped to a logical network.
	 	- **Isolation**: More often you'll want to isolate networks from each other. For example you might want to isolate networks that have different purposes, or you might be a provider who wants to host workloads for multiple tenants on a single logical network, with isolation for each tenant. In this case you'll have multiple VM networks mapped to a logical network. VM networks mapped to a logical network can be  isolated using VLANs/private VLANs, or network virtualization. Note that:
	 	 	- A typical setup might be an infrastructure network with no isolation or VLAN isolation, a load balancer backend and internet facing network with PVLAN, and tenant networks with isolation using network virtualization.
		 	- You can only use one type of isolation on a single logical network. If you do need this you'll need multiple logical networks.
		  	- There's a practical limit of ~2000 tenants and ~4000 VM networks for a single VMM server.

	- **Network sites**: If your organization has different locations and datacenters you can include information about those sites in your logical network settings. For example you could specify a New York site with and IP subnet and/or VLAN settings, and then a London site with different IP/VLAN settings. You can then assign IP address to VMs based on network, location, and VLAN settings. Note that:

		- You need to assign an IP subnet to a site if VMM is going to distribute static IP addresses to VMs in the site. If you're using DHCP you don't need a subnet.
		- You need to configure a VLAN if one's used in your physical site. If you're not using VLANs and you're using DHCP you don't need to define network sites in your logical network.


## Create logical networks automatically

If you want VMM to automatically create logical and VM networks you can specify how VMM determines the logical network name.

1. Click **Settings** > **General**. Double-click **Network Settings**.
2. Configure the **Logical network matching** setting. Note that:

	- For Hyper-V hosts you can use the entire DNS suffix label, or the first one. For example if the DNS suffix is corp.contoso.com the logical network will be corp-contoso.com or just corp. This isn't supported for VMware hosts.
	- For Hyper-V and VMware hosts you can select the network connection name or the virtual network switch name (the name of the virtual network switch to which the physical adapter of the host is bound).
	- By default VMware hosts use the virtual network switch option.
	- You can also specify a fallback option if the first logical matching fails.

If you don't want VMM to create logical and VM networks automatically you can disable the global setting.

1. Click **Settings** > **General** and double-click **Network Settings**.
2. Clear **Create logical networks automatically**.


## Create logical networks manually

1.  **Fabric** > **Home **> **Show** > **Fabric Resources**. In **Fabric** expand **Networking** > **Logical Networks** > **Home** > **Create** > **Create Logical Network**.
2.  In **Create Logical Network Wizard** > **Name** specify a name and description.
3.  Specify how you want to isolate VM networks associated with this logical network:

	- If you want to have multiple VM networks associated with the logical network and isolate them using network virtualization click **One connected network** > **Allow new VM networks created on this logical network to use network virtualization**.
	- If you want to have multiple VM networks associated with the logical network and isolate them using a VLAN/PVLAN select **VLAN-based independent networks** or **Private VLAN (PVLAN) networks**.
	- If you don't want to isolate networks in the logical network, click **One connected network** > **Create a VM network with the same name to allow virtual machines to access this logical network directly**. With this setting you'll have a single VM network associated with your logical network.
	- If you've deployed a Microsoft network Controller in the VMM fabric you can select to have the logical network managed by the network controller.

4. In **Network Site** add network sites to the logical network. If you don't need to create network sites click **Next**.

	- **DHCP no VLAN**: If you're using DHCP to allocate IP addresses and you don't have VLANs you don't need a network site. Note that VMM automatically suggests a site name. Any network name shouldn't be longer than 64 characters.
	- **Static IP**: If you're using static IP addresses create at least one network site and associate at least one IP subnet with it.
	- **VLAN**: If you're using VLANs with static IP addressing create corresponding network site for the VLAN and subnet pairs. If you're using DHCP create corresponding network sites for VLAN information only.
	- **Network virtualization**: If you're using network virtualization create at least one network site with an associated IP subnet so that the logical network has an IP address pool.
	- **Load balancer**: If the logical network will contain a load balancer create at least one network site with an associated IP subnet.
5. If you're using an external network managed by a vendor network management console or virtual switch extension manager outside VMM you can configure settings in the vendor conole and import them into VMM.
6. In **Host groups that can use this network site** select each host group to which you want to make the logical network available.
7. In **Associated VLANs and IP subnets** click **Insert Row** to specify the settings that you want to assign to the network site. If you selecting PVLAN you'll need to add a **SecondaryVLAN** for each VLAN. Ensure that the VLANs and subnets are available in your physical network. If you leave the VLAN field empty VMM assigns a value of 0 to indicate that VLANs aren't used. In trunk mode 0 indicates native VLAN.
8. In **Summary** review the settings and click **Finish**. When the job shows as **Completed** verify the logical network in **Logical Networks and IP Pools**.

## Next steps

If you created network sites and associated one or more IP subnets with them (you're not using DHCP) you can create static IP address pools from those subnets. Then VMM can automatically allocate IP addresses to VMs in the network site. [Set up IP address pools](manage-network-static-address-pools.md).
