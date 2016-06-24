---
title: Overview: plan logical networks, network sites, and IP address pools in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 56bcb452-b2c0-49ba-a615-62af65dfc066
---
# Overview: plan logical networks, network sites, and IP address pools in VMM
You can use Virtual Machine Manager (VMM) to manage your physical and virtualized network infrastructure. *Logical networks* form the foundation of your network configuration in VMM. You create and name logical networks based on the function they serve in your environment, for example, the “Management,” “Cluster,” “Storage,” or “Tenant” networks. Within each logical network, you create one or more *network sites* that specify IP subnets, virtual local area networks (VLANs), or subnet/VLAN pairs that represent your environment.

In a logical network, you can provide static IP addressing by creating static IP address pools for the logical network. Dynamic Host Configuration Protocol (DHCP) is also an option.

This topic provides planning guidance and recommendations. For a list of specific procedures, see [Implementing the configuration](Configuring-logical-networks,-VM-networks,-and-logical-switches-in-VMM.md#BKMK_implementing) in "Configuring logical networks, VM networks, and logical switches in VMM."

This topic contains the following sections:

-   [Plan your logical networks, network sites, and IP address pools](Overview--plan-logical-networks,-network-sites,-and-IP-address-pools-in-VMM.md#BKMK_plan)

-   [Logical networks created by default](Overview--plan-logical-networks,-network-sites,-and-IP-address-pools-in-VMM.md#BKMK_default)

-   [Guidelines for network sites: VLAN and IP subnet settings](Overview--plan-logical-networks,-network-sites,-and-IP-address-pools-in-VMM.md#BKMK_vlans_ip)

-   [Guidelines for IP address pools](Overview--plan-logical-networks,-network-sites,-and-IP-address-pools-in-VMM.md#BKMK_address_pools)

## <a name="BKMK_plan"></a>Plan your logical networks, network sites, and IP address pools
Use the following table to plan for the logical networks, VM networks, and IP address pools you will need to support a virtualized infrastructure.

|Item to review or determine|Description and (as needed) links within this topic|
|-------------------------------|---------------------------------------------------------|
|1. Logical networks already created by default by VMM|When you add a Hyper-V host to VMM, logical networks may be created by default, based on DNS suffixes. See [Logical networks created by default](Overview--plan-logical-networks,-network-sites,-and-IP-address-pools-in-VMM.md#BKMK_default) in this topic.|
|2. How many logical networks you need, and the purpose of each|Plan to create logical networks to represent the network topology for your hosts. For example, if you need a management network, a network used for cluster heartbeats, and a network used by virtual machines, create a logical network for each.|
|3. Categories that your logical networks fall into|Review the purposes of your logical networks, and categorize them:<br /><br />-   **No isolation**: For example, a cluster-heartbeat network for a host cluster.<br />-   **VLAN**: Isolation provided by your VLANs.<br />-   **Virtualized**: Provides a foundation for Hyper-V network virtualization.<br />-   **External**: Managed through a network manager (vendor network-management console or virtual switch extension manager) outside of VM. For more information, see [VMM networking reference: using a virtual switch extension manager or network manager in VMM](VMM-networking-reference--using-a-virtual-switch-extension-manager-or-network-manager-in-VMM.md).<br />-   **IPAM**: Managed through an IP Address Management (IPAM) server. For more information, see [VMM networking reference: using an IPAM Server in VMM](VMM-networking-reference--using-an-IPAM-Server-in-VMM.md).|
|4. How many network sites are needed in each logical network|One common way to plan network sites is around host groups and host locations. For example, for a "Seattle" host group and a "New York" host group, if you had a MANAGEMENT logical network, you might create two network sites, called **MANAGEMENT - Seattle** and **MANAGEMENT - New York**. For additional suggestions, see [Guidelines for network sites: VLAN and IP subnet settings](Overview--plan-logical-networks,-network-sites,-and-IP-address-pools-in-VMM.md#BKMK_vlans_ip).|
|5. Which VLANs and/or IP subnets are needed in each network site|The VLANs and IP subnets you assign should match your topology. See [Guidelines for network sites: VLAN and IP subnet settings](Overview--plan-logical-networks,-network-sites,-and-IP-address-pools-in-VMM.md#BKMK_vlans_ip) in this topic.|
|6. Which logical networks (or specifically, which network sites) will need IP address pools|Determine which logical networks will use static IP addressing or load balancing, and which logical networks will be the foundation for network virtualization. For these logical networks, plan for IP address pools. See [Guidelines for creating IP address pools](Overview--plan-logical-networks,-network-sites,-and-IP-address-pools-in-VMM.md#BKMK_address_pools) in this topic.|

## <a name="BKMK_default"></a>Logical networks created by default
In VMM, in the **Fabric** workspace, under **Networking** > **Logical networks**, you might see logical networks created by VMM by default. VMM creates these networks to ensure that when you add a host, you have at least one logical network for deploying virtual machines and services. No network sites are created automatically. For information about changing the defaults, see [How to configure global network settings in VMM](How-to-configure-global-network-settings-in-VMM.md).

To illustrate how these settings work, suppose that you have not changed the settings, and you add a Hyper-V host to VMM management. In this case, VMM automatically creates logical networks that match the first DNS suffix label of the connection-specific DNS suffix on each host network adapter. On the logical network,VMM also creates a VM network that is configured with “no isolation.” For example, if the DNS suffix for the host network adapter was corp.contoso.com, VMM would create a logical network named “corp,” and on it, a VM network named “corp” that is configured with no isolation.

## <a name="BKMK_vlans_ip"></a>Guidelines for network sites: VLAN and IP subnet settings
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
> For an external network, that is, a network managed through a vendor network-management console or virtual switch extension manager outside of VMM, you can configure settings through the vendor network-management console, and allow them to be imported from the vendor network-management database into VMM. For more information, see [VMM networking reference: using a virtual switch extension manager or network manager in VMM](VMM-networking-reference--using-a-virtual-switch-extension-manager-or-network-manager-in-VMM.md).

## <a name="BKMK_address_pools"></a>Guidelines for IP address pools
In general, create IP address pools where you will use static IP addressing or load balancing; also create IP address pools on logical networks that will be the foundation for VM networks supporting network virtualization. VMM uses IP address pools to assign IP addresses to Hyper-V hosts that you deploy through VMM, and to Windows-based virtual machines that you deploy through VMM, regardless of the type of host they are running on (Hyper-V or VMware ESX).

The following table provides detailed guidelines. Additional information about IP address pools is provided after the table.

|Purpose of logical network|Guideline for creating IP address pools for that logical network, or for VM networks built on that logical network|
|------------------------------|----------------------------------------------------------------------------------------------------------------------|
|**Static IP**: Logical network with "no isolation," and requiring static IP addressing, for example, a network that supports host cluster nodes|Create one or more IP address pools for the logical network.<br /><br />For a logical network with "no isolation," if you create a VM network on the logical network, any IP address pools will automatically become available on the VM network. In other words, the VM network will give direct access to the logical network.|
|**VLANs**: Logical network for VLAN-based independent networks, using static IP addressing (rather than DHCP)|Create IP address pools on the logical network—one IP address pool for each VLAN where static IP addressing will be used.<br /><br />Later, when you create the VM networks that represent the VLANs, the IP address pools will automatically become available on those VM networks.|
|**Network virtualization**: Logical network that will be the foundation for VM networks using network virtualization|Create IP address pools on the logical network that provides the foundation for the VM networks. Later, when you create the VM networks, you will also create IP address pools on them (and see the important note after this table). If you use DHCP on the VM networks, VMM will respond to a DHCP request with an address from an IP address pool.<br /><br />The process of creating an IP address pool for a VM network is similar to the process of creating an IP address pool for a logical network.|
|**Load balancing**: Logical network that will be the foundation for a VM network, where you will use load balancing in a "service tier" (part of a set of virtual machines deployed together as a VMM "service")|Create a static IP address pool on the VM network, and in it, define a reserved range of IP addresses. When you use VMM to deploy a load-balanced service tier that uses the VM network, VMM uses the reserved range of IP addresses to assign virtual IP (VIP) addresses to the load balancer.|

Additional information about IP address pools follows.

> [!IMPORTANT]
> If you configure a virtual machine to obtain a static IP address from an IP address pool, you must also configure the virtual machine to use a static MAC address. You can either specify the MAC address manually (during the **Configure Settings** step) or have VMM automatically assign a MAC address from a MAC address pool.
> 
> This requirement for static MAC addresses is necessary because VMM uses the MAC address to identify which network adapter to set the static IP address to, and this identification must happen before the virtual machine starts. Identifying the network adapter is especially important if a virtual machine has multiple adapters. If the MAC addresses were assigned dynamically through Hyper-V, VMM could not consistently identify the correct adapter to set a static IP address on.
> 
> VMM provides static MAC address pools by default, but you can customize the pools. VMM provides static MAC address pools by default, but you can customize the pools, as described in [VMM networking reference: creating custom MAC address pools in VMM](VMM-networking-reference--creating-custom-MAC-address-pools-in-VMM.md).

-   When you create a static IP address pool, you can configure associated information, such as default gateways, Domain Name System (DNS) servers, DNS suffixes, and Windows Internet Name Service (WINS) servers. All of these settings are optional.

-   IP address pools support both IPv4 and IPv6 addresses. However, you cannot mix IPv4 and IPv6 addresses in the same IP address pool.

> [!NOTE]
> After a virtual machine has been deployed in VMM, you can view the IP address or addresses assigned to that virtual machine. To do this, right-click the listing for the virtual machine, click **Properties**, click the **Hardware Configuration** tab, click the network adapter, and in the results pane, click **Connection details**.

## See Also
[How to create a logical network and IP address pools in VMM](How-to-create-a-logical-network-and-IP-address-pools-in-VMM.md)
[Configuring logical networks, VM networks, and logical switches in VMM](Configuring-logical-networks,-VM-networks,-and-logical-switches-in-VMM.md)
[Managing network resources with VMM](Managing-network-resources-with-VMM.md)


