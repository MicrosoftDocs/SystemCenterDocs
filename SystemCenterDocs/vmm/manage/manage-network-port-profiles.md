---
title: Set up port profiles in the VMM fabric
description: This article describes how to create port profiles in the VMM fabric
author:  rayne-wiselman
ms-author: raynew
manager:  cfreemanwa
ms.date:  2016-09-22
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---

# Set up port profiles in the VMM fabric

>Applies To: System Center 2016 - Virtual Machine Manager

Use this article to learn about and set up uplink port profiles and virtual network adapter port profiles in the System Center 2016 - Virtual Machine Manager (VMM) networking fabric.

## Overview

- **Uplink port profiles**: You create uplink port profiles and then apply them to physical network adapters when you deploy switches. Uplink port profiles define the load balancing algorithm for an adapter, and specify how to team multiple network adapters on a host that use the same uplink port profile. This profile is used in conjunction with the logical network that you associated with the adapter.
- **Virtual network adapter port profiles**. You apply virtual network adapter port profiles to virtual network adapters. These profiles define specific capabilities, such as bandwidth limitations, and priority. VMM includes a number of built-in profiles.
- **Port classifications**: After creating a virtual network adapter port profiles you can create port classifications. Port classifications are abstractions that identify different types of virtual network adapter port profiles. For example you could create a classification called FAST to identify ports that are configured to have more bandwidth and another one called SLOW with less bandwidth. Classifications are included in logical switches. Administrators and tenants can choose a classification for their VM virtual machine adapters. By default, VMM includes built-in classifications that map to the built-in virtual network adapter port profiles

## Define uplink port profiles

Some guidelines for creating uplink port profiles:

- You'll need at least one uplink port profile for each physical network in your environment. If you do have a simple environment with a single physical network and all hosts are configured the same way, with the same protocols for network adapter teaming, then you might only need a single uplink port profile. This is rare though. You'll probably need to scope or restrict certain logical networks to a specific group of hosts computer, and this need makes it useful to create multiple uplink port profiles.
- You need to define uplinks for each physical location that has its own VLAN and IP subnets.
- If you plan to restrict or otherwise scope logical networks to a specific set of host
computers, you will need to create uplinks for each group of computers.
- You need separate uplink port profiles for groups of computers (in each physical
location) that have different connectivity requirements or use different teaming
protocols.
- You might consider creating separate uplinks for networks that do not or will
not support network virtualization.
- Network sites that will be included in a profile should be scoped to the same group of host computers. If they aren't you'll receive an out-of-scope error when you try to apply it to a computer that isn't a member of the host groups defines in every one of the network sites included in the uplink profile.
- You should try and ensure that each of the network sites t hat you add to an uplink port profile refers to a different logical network. If you do otherwise all of the VLANs and IP subnets defined in those network sites will be associated with the logical network on any host computer on which the  uplink port profile is applied. If you're not using VLAN isolation the host computer has no way to establish which of the range of possible VLANs and IP subnets will be needed to allow VMs connected to the logical network
- You can create an uplink port profile that contains references to multiple network sites (and hence logical networks). You should ensure that the VLANs and IP addresses in each of the selected sites should be valid (routable) from the physical network adapter to which the port profile has been applied.
- When you apply the profile to a physical network adapter these network sites determine the set of logical networks that should be associated with the physical adapter and the VLANs and IP subnets that will be allocated to VMs and services that connect to those logical networks.


### Create an uplink port profile

1. Click **Fabric** > **Home** > **Show **> **Fabric Resources**. Click **Fabric** tab > **Networking** > **Port Profiles** > **Hyper-V Port Profile**.
2. In **Create Hyper-V Port Profile Wizard** > **General** type in a name, description and select **Uplink Port Profile**. Select the load balancing and teaming settings:

	- **Load balancing**: **Host Default** is the default setting and this will either distribute network traffic based on the Hyper-V switch port identifier of the source VM or use a **Dynamic** loading balancing algorithm, depending what the Hyper-V host supports. Dynamic is only available from Windows Server 2012 R2 onwards. You can also select:
		- Hyper-V port: Distributes network traffic according to the Hyper-V switch port identifier of the source VM.
		- Transport ports: Uses the source and destination TCP ports and the IP addresses to create a hash and then assigns the packets that have that hash value to one of the available network adapters.
		- IP addresses: Uses the source and destination IP addresses to create a hash and then assigns the packets that have that hash value to one of the available network adapters.
		- MAC addresses: Uses the source and destination MAC addresses to create a hash and then assigns the packets that have that hash value to one of the available network adapters.

	- **Teaming**: **Switch Independent** is the default setting and this specifies that physical network switch configuration isn't needed for the NIC team. The network switch is not configured and so allow network adapters within the team to be connected to multiple (non-=trunked) physical switches. You can also select:
		- **LACP**: Use the LACP protocol to dynamically identify links that are connected between the host and a given switch.
		- **Static teaming**: You configure both the switch and host to identify which links form the team.

3. In **Network Configuration** select one or more network sites for this uplink port profile to support. Uplink port profiles contains a list of network sites with each network site representing a link to a different logical network.  Select **Enable Hyper-V Network Virtualization** if you want to enable network virtualization to deploy multiple VM networks on a single physical network. You should only do this if the logical network is configured for network virtualization with **Allow new VM networks created on this logical network to use network virtualization** enabled.
4. In **Summary** review the settings and click **Finish**.

After you create an uplink port profile, the next step is to add it to a logical switch, which places it in a list of profiles that are available through that logical switch. When you apply the logical switch to a network adapter in a host, the uplink port profile is available in the list of profiles, but it is not applied to that network adapter until you select it from the list. This helps you to create consistency in the configurations of network adapters across multiple hosts, but also enables you to configure each network adapter according to your specific requirements.

## Create a virtual network adapter port profile

1. Click **Fabric** > **Home** > **Show **> **Fabric Resources**. Click **Fabric** tab > **Networking** > **Port Profiles** > **Home** > **Create** > **Hyper-V Port Profile**.
2. In **Create Hyper-V Port Profile Wizard** > **General** type in a name, description and select **Uplink Port Profile**.
3. In **Offload Setting**, specify a setting for offloading traffic:

	- **Enable virtual machine queue (VMQ)**: Packets destined for a virtual network adapter are delivered directly to a queue for that adapter, and they do not have to be copied from the management operating system to the virtual machine. The physical network adapter must support VMQ.
	- **Enable IPsec task offloading**: Some or all of the IPsec computational work is shifted from the computer’s CPU to a dedicated processor on the network adapter. The physical network adapter and the guest operating system must support it.
	- **Enable single-root I/O virtualization**: A network adapter can be assigned directly to a virtual machine. This maximizes network throughput while minimizing network latency and minimizing the CPU overhead that is required to process network traffic. The physical network adapter and drivers in the management operating system and guest operating system must support it. If you want to use SR-IOV you'll need to enable it in the port profile (in **Offload** settings) and in the logical switch (**General** settings) that includes the port profile. It must be configured correctly on the host when you create the virtual switch that brings port settings and the logical switch you want to use on the host together. In the virtual switch you attach the port profile to the virtual switch  using a port classification (either the default SR-IOV classification provided by VMM, or a custom one)

4. In **Security Settings** specify:

	- **Allow MAC spoofing**: Allows a virtual machine to change the source MAC address in outgoing packets to an address that is not assigned to that virtual machine. For example, a load-balancer virtual appliance might require this setting to be enabled.
	- **Enable DHCP guard**: Helps protect against a malicious virtual machine that represents itself as a DHCP server for man-in-the-middle attacks.
	- **Allow router guard**: Helps protect against advertisement and redirection messages that are sent by an unauthorized virtual machine that represents itself as a router.
	- **Allow guest teaming**: Allows you to team the virtual network adapter with other network adapters that are connected to the same switch.
	- **Allow IEEE priority tagging**: Allows you to tag outgoing packets from the virtual network adapter with IEEE 802.1p priority. These priority tags can be used by Quality of Service (QoS) to prioritize traffic. If IEEE priority tagging is not allowed, the priority value in the packet is reset to 0.
	- **Allow guest specified IP addresses**: Affects VM networks using network virtualization. The VM (guest) can add and remove IP addresses on this virtual network adapter. This can simplify the process of managing virtual machine settings. Guest-specified IP addresses are required for virtual machines that use guest clustering with network virtualization. The IP address that a guest adds must be within an existing IP subnet in the VM network.

5. In **Bandwidth Settings** specify the minimum and maximum bandwidth that are available to the adapter. The minimum bandwidth can be expressed as megabits per second (Mbps) or as a weighted value (from 0 to 100) that controls how much bandwidth the virtual network adapter can use in relation to other virtual network adapters. Note that bandwidth settings aren't used SR-IOV is enabled on the port profile and logical switch that contains the port profile.
6. In **Summary** review the settings and click **Finish**.

After creating a port profile you can create a port classification.

## Create port classifications for virtual network adapter port profiles

1. Click **Fabric** > **Home** > **Show** > **Fabric Resources**. Click the **Fabric** tab > **Networking** > **Port Classifications** > **Home** > **Create** > **Port Classification**.
2. In **Create Port Classification Wizard** > **Name** specify a classification name.
