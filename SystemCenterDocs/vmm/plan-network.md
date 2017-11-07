---
ms.assetid: 72a60bb6-55e6-4305-a318-7fe88512f2c4
title: Plan the VMM networking fabric
description: This article provides information about preparing the VMM network fabric
author:  rayne-wiselman
ms.author: raynew
manager:  carmonm
ms.date:  11/07/2017
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---


# Plan the VMM networking fabric



This article describes how to plan your networking fabric in System Center - Virtual Machine Manager (VMM).

## Networking components

VMM networking contains a number of components, summarized in the following table:

**Networking component** | **Details**
--- | ---
**Logical networks** | In VMM your physical networks are defined as logical networks. Logical networks are a useful way of abstracting your underlying physical network infrastructure. Logical network settings will match or mirror your physical network environment. For example the IP addresses and VLAN properties will match exactly, a network site in a logical network will contain configuration settings for the site.<br/><br/>By default VMM creates logical ntwork automatically when you add a Hyper-V host to the fabric if a suitable network can't be found. You can disable this option.<br/><br/> To abstract logical networks from the VMs that use them VMM provides **VM networks**. You connect the virtual adapter of a VM to a VM networks.
**MAC address pools** | You can create MAC address pools for VMs running on virtualization hosts in the VMM fabric. When you use static MAC address pools VMM can automatically generate and assign MAC addresses to VMs. You can use a standard pool or configure a custom pool.
**Load balancers** | VMM supports adding hardware load balancers or using NLB to load balance requests to a service tier
**VIP templates** | Virtual IP (VIP) templates contain load balancing information for a particular type of traffic. For example you could have a template that specifies how to balance HTTPS traffic on a specific load balancer.
**Logical switches** | Logical switches are containers for virtual switch settings. You apply logical switches to hosts so that you have consistent switch settings across all hosts. VMM  tracks switch settings on hosts deployed with logical switches to ensure compliance.
**Port profiles** | Port profiles act as containers for the properties you want a network adapter to have. Instead of configuring properties per network adapter you set up in the port profile and apply that profile to an adapter.<br/><br/>There are two types of port profiles. Virtual port profiles contain settings that are applied to virtual network adapters connect to VMs or used by virtualization hosts. Uplink port profiles are used to define how a virtual switch connects to a logical network.
**Port classifications** | Port classifications are abstract containers for virtual port profile settings. This abstraction means that admins and tenants can assign a port classification to a VM template, while the VM's logical switch determines which port profile should be used. rofiles and then both admins and tenant can select a suitable classification. VMM contains a number of default port classifications. For example there's a classification for VMs that need high bandwidth and a different one for VMs that need low bandwidth. Port classifications are linked to virtual port profiles when you configure logical switches.

## Plan logical networks

During deployment you'll need to create logical networks and set up network sites and IP addressing in each network. Then you'll create VM networks based on those logical networks.

Here's what you'll need to plan:

1. **Automation creation**: Decide whether you want to let VMM create logical networks. VMM will automatically create a logical network each time you add a virtualization host. VMM doesn't create network sites in the automatically-created logical network. You can turn this option off in **Settings** > **General** > **Network Settings** and clear **Automatic creation of logical networks**.
2. **Logical network capacity**: If you're going to create logical networks manually figure out what you'll need to represent your physical network topology. For example if you need a management network and a network used by VMs you should create two logical networks.
3. **Logical network types**: Figure out the type of logical network you need. You'll configure VM networks on top of logical networks and those VM networks can provide network virtualization with the ability to crate multiple virtual networks on a shared physical networks, or VM networks can provide isolation with VLANS and PVLANS. When you configure the logical network you'll need to indicate the type of network you need.
4. **Network sites**: Determine how many network sites you need in the logical network. You could plan around host groups and host locations. For example a Seattle host group and a New York host group. You don't need network sites if you don't have VLANs and you're using DHCP to allocate IP addresses.
5. **VLANs/subnets**: Figure out the VLANs and IP subnets you need in the logical network. These will mirror what you have in your physical network topology.
6. **IP addressing**: If you're using static IP address assignment determine which logical networks need static address pools.

Here's what you'll need to do:

1. Identify baseline logical networks: Identify a set of initial logical networks that mirror the physical networks in your environment.
2. Identify additional logical networks for specific requirements: Define logical networks with  specific purpose or perform a particular function within your environment. One of the benefits of logical networks is that you can separate computer and network services with different business purposes without needing to change your physical infrastructure.
3. Determine isolation requirements: Identify which logical networks need to be isolated and how that isolation will be enforced, either through physical separation, VLAN/PVLAN, or network virtualization. Remember that you need isolation if the logical network is going to be used by multiple tenants. If you have a single tenant or customer isolation is optional. In turn, if you don't need isolation you'll only need a single VM network that maps to the logical network.
4. Determine the network sites, VLANs, PVLANs, and IP pools that need to be defined for each logical network you have identified.
5. Figure out which logical network will associate with which virtualization hosts.

## Plan logical networks, network sites, and IP address pools
Use the following table to plan for the logical networks, VM networks, and IP address pools you will need to support a virtualized infrastructure.

|Item to review or determine|Description and (as needed) links within this topic|
|-------------------------------|---------------------------------------------------------|
| Logical networks already created by default by VMM|When you add a Hyper-V host to VMM, logical networks may be created by default, based on DNS suffixes. |
| How many logical networks you need, and the purpose of each|Plan to create logical networks to represent the network topology for your hosts. For example, if you need a management network, a network used for cluster heartbeats, and a network used by virtual machines, create a logical network for each.|
| Categories that your logical networks fall into|Review the purposes of your logical networks, and categorize them:<br /><br />-   **No isolation**: For example, a cluster-heartbeat network for a host cluster.<br />-   **VLAN**: Isolation provided by your VLANs.<br />-   **Virtualized**: Provides a foundation for Hyper-V network virtualization.<br />-   **External**: Managed through a network manager (vendor network-management console or virtual switch extension manager) outside of VM. <br/><br/>-   **IPAM**: Managed through an IP Address Management (IPAM) server. |
| How many network sites are needed in each logical network|One common way to plan network sites is around host groups and host locations. For example, for a "Seattle" host group and a "New York" host group, if you had a MANAGEMENT logical network, you might create two network sites, called **MANAGEMENT - Seattle** and **MANAGEMENT - New York**. |
| Which VLANs and/or IP subnets are needed in each network site|The VLANs and IP subnets you assign should match your topology. |
| Which logical networks (or specifically, which network sites) will need IP address pools|Determine which logical networks will use static IP addressing or load balancing, and which logical networks will be the foundation for network virtualization. For these logical networks, plan for IP address pools. |

## Logical networks created by default

In the VMM console, **Fabric** >**Networking** > **Logical networks**, you might see logical networks created by VMM by default. VMM creates these networks to ensure that when you add a host, you have at least one logical network for deploying virtual machines and services. No network sites are created automatically.

To illustrate how these settings work, suppose that you have not changed the settings, and you add a Hyper-V host to VMM management. In this case, VMM automatically creates logical networks that match the first DNS suffix label of the connection-specific DNS suffix on each host network adapter. On the logical network,VMM also creates a VM network that is configured with “no isolation.” For example, if the DNS suffix for the host network adapter was corp.contoso.com, VMM would create a logical network named “corp,” and on it, a VM network named “corp” that is configured with no isolation.

## Guidelines for network sites: VLAN and IP subnet settings
The main guideline specifying VLANs and IP subnets for network sites is to reflect your network topology. For details, see the following table.

> [!NOTE]
> Network sites are sometimes referred to as "logical network definitions," for example, in Windows PowerShell commands.

|Purpose of logical network|Guideline for network sites in that logical network|
|------------------------------|-------------------------------------------------------|
|**Static IP**: Logical network that will use static IP addressing, for example, a network that supports host cluster nodes|Create at least one network site and associate at least one IP subnet with the network site.|
|**DHCP (but not VLANs)**: Logical network that does not include VLANs, with all computers or devices using DHCP|No network sites are necessary.|
|**VLANs**: Logical network for VLAN-based independent networks|-   If the VLANs use static IP addressing, create corresponding network sites that specify VLAN and IP subnet information.<br />-   If the VLANs use DHCP, create corresponding network sites that specify only VLAN information (no subnets).|
|**Network virtualization**: Logical network that will be the foundation for VM networks using network virtualization|Create at least one network site and associate at least one IP subnet with the site. The IP subnet is necessary because this logical network will need an IP address pool.<br /><br />Assign a VLAN to the network site if appropriate.|
|**Load balancing**: Logical network that will include a load balancer that is managed by VMM|Create at least one network site and associate at least one IP subnet with the network site.|

> [!NOTE]
> For an external network, that is, a network managed through a vendor network-management console or virtual switch extension manager outside of VMM, you can configure settings through the vendor network-management console, and allow them to be imported from the vendor network-management database into VMM.

## Guidelines for IP address pools
In general, create IP address pools where you will use static IP addressing or load balancing; also create IP address pools on logical networks that will be the foundation for VM networks supporting network virtualization. VMM uses IP address pools to assign IP addresses to Hyper-V hosts that you deploy through VMM, and to Windows-based virtual machines that you deploy through VMM, regardless of the type of host they are running on (Hyper-V or VMware ESX).

The following table provides detailed guidelines. Additional information about IP address pools is provided after the table.

|Purpose of logical network|Guideline for creating IP address pools for that logical network, or for VM networks built on that logical network|
|------------------------------|----------------------------------------------------------------------------------------------------------------------|
|**Static IP**: Logical network with "no isolation," and requiring static IP addressing, for example, a network that supports host cluster nodes|Create one or more IP address pools for the logical network.<br /><br />For a logical network with "no isolation," if you create a VM network on the logical network, any IP address pools will automatically become available on the VM network. In other words, the VM network will give direct access to the logical network.|
|**VLANs**: Logical network for VLAN-based independent networks, using static IP addressing (rather than DHCP)|Create IP address pools on the logical network—one IP address pool for each VLAN where static IP addressing will be used.<br /><br />Later, when you create the VM networks that represent the VLANs, the IP address pools will automatically become available on those VM networks.|
|**Network virtualization**: Logical network that will be the foundation for VM networks using network virtualization|Create IP address pools on the logical network that provides the foundation for the VM networks. Later, when you create the VM networks, you will also create IP address pools on them (and see the important note after this table). If you use DHCP on the VM networks, VMM will respond to a DHCP request with an address from an IP address pool.<br /><br />The process of creating an IP address pool for a VM network is similar to the process of creating an IP address pool for a logical network.|
|**Load balancing**: Logical network that will be the foundation for a VM network, where you will use load balancing in a "service tier" (part of a set of virtual machines deployed together as a VMM "service")|Create a static IP address pool on the VM network, and in it, define a reserved range of IP addresses. When you use VMM to deploy a load-balanced service tier that uses the VM network, VMM uses the reserved range of IP addresses to assign virtual IP (VIP) addresses to the load balancer.|


> [!IMPORTANT]
> If you configure a virtual machine to obtain a static IP address from an IP address pool, you must also configure the virtual machine to use a static MAC address. You can either specify the MAC address manually (during the **Configure Settings** step) or have VMM automatically assign a MAC address from a MAC address pool.
>
> This requirement for static MAC addresses is necessary because VMM uses the MAC address to identify which network adapter to set the static IP address to, and this identification must happen before the virtual machine starts. Identifying the network adapter is especially important if a virtual machine has multiple adapters. If the MAC addresses were assigned dynamically through Hyper-V, VMM could not consistently identify the correct adapter to set a static IP address on.
>
> VMM provides static MAC address pools by default, but you can customize the pools. VMM provides static MAC address pools by default, but you can customize the pools.

-   When you create a static IP address pool, you can configure associated information, such as default gateways, Domain Name System (DNS) servers, DNS suffixes, and Windows Internet Name Service (WINS) servers. All of these settings are optional.

-   IP address pools support both IPv4 and IPv6 addresses. However, you cannot mix IPv4 and IPv6 addresses in the same IP address pool.

> [!NOTE]
> After a virtual machine has been deployed in VMM, you can view the IP address or addresses assigned to that virtual machine. To do this, right-click the listing for the virtual machine, click **Properties**, click the **Hardware Configuration** tab, click the network adapter, and in the results pane, click **Connection details**.

## Next steps

- [Set up the networking fabric](manage-networks.md)
