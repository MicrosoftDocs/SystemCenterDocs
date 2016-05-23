---
title: Overview: plan VM networks in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9319e518-2b01-4462-bb05-bbddfed6e00d
---
# Overview: plan VM networks in VMM
In [!INCLUDE[vmm12sp1_long](../../Token/vmm12sp1_long_md.md)], after you complete the planning described in [Overview: plan logical networks, network sites, and IP address pools in VMM](Overview--plan-logical-networks,-network-sites,-and-IP-address-pools-in-VMM.md), you can plan your VM networks. Use this table for more information:

|Purpose of VM network|Description|
|-------------------------|---------------|
|**For VLANs**: see [Plan VM networks for a VLAN-based configuration](Overview--plan-VM-networks-in-VMM.md#BKMK_VLAN) in this topic|You can use familiar virtual local area network \(VLAN\) technology for network isolation, and manage your configuration in [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)].|
|**For Hyper\-V network virtualization**: see [Plan VM networks for Hyper-V network virtualization](Overview--plan-VM-networks-in-VMM.md#BKMK_hnv) in this topic|You can support multiple tenants \(also called clients or customers\) with their own networks, isolated from the networks of others, by using VM networks configured for network virtualization.|
|**Direct access to the logical network \("no isolation"\)**: described in this table|A VM network can provide direct access to a logical network. No planning is needed, other than to identify the logical network to give access to. This is the type of VM network typically used for management networks \(for example, the network used for managing a host\).|

## <a name="BKMK_VLAN"></a>Plan VM networks for a VLAN\-based configuration
You can use familiar virtual local area network \(VLAN\) technology for network isolation, and manage your configuration in [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)].

> [!NOTE]
> A "VLAN\-based configuration" means a configuration where VLANs are used for isolation, not just for broadcast boundaries.

Use the following guidelines to plan for VM networks for a VLAN\-based configuration:

-   Plan for a logical network with VLAN and IP subnet settings as described in the [Guidelines for network sites: VLAN and IP subnet settings](Overview--plan-logical-networks,-network-sites,-and-IP-address-pools-in-VMM.md#BKMK_vlans_ip) section in "Overview: plan your logical networks, network sites, and IP address pools." For the logical network, you will use the **VLAN\-based independent networks** option.

-   Plan for one VM network for each network site \(and VLAN\) in your configuration.

The following illustration shows the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] configuration for a network where VLAN 1 and VLAN 4 are used for network isolation. In [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)], the logical network uses the **VLAN\-based independent networks** setting, and contains network sites with the appropriate VLAN and IP subnet settings \(only one network site is visible\). For each VLAN, a VM network has been created, and it receives the VLAN and IP subnet information directly from the logical network. The associated IP address pools provide for static IP addressing in the VM networks.

![](Image/01_TH_VM_netwk_VLAN.png)

**Figure 1   VM networks for VLAN configuration**

In the illustration, bold text represents items you configure by opening a wizard or a **Properties** dialog box. Regular text represents items on a page or tab within the wizard or dialog box.

## <a name="BKMK_hnv"></a>Plan VM networks for Hyper\-V network virtualization
To support multiple tenants \(also called clients or customers\) with their own networks, isolated from the networks of others, use VM networks configured for Hyper\-V network virtualization. For more information about Hyper\-V network virtualization, which was introduced in [!INCLUDE[win8_server_2](../../Token/win8_server_2_md.md)], see [Network Virtualization technical details](http://technet.microsoft.com/library/jj134174.aspx).

On VM networks that use network virtualization, your tenants can use any IP addresses that they want for their virtual machines, regardless of the IP addresses that are used on other VM networks. Also, you can enable your tenants to configure some aspects of their own networks, based on limits that you specify.

> [!NOTE]
> Network virtualization is supported only on hosts that are running [!INCLUDE[winthreshold_server_2](../../Token/winthreshold_server_2_md.md)], [!INCLUDE[winblue_server_2](../../Token/winblue_server_2_md.md)], or [!INCLUDE[win8_server_2](../../Token/win8_server_2_md.md)]. Hosts running [!INCLUDE[nextref_server_7](../../Token/nextref_server_7_md.md)] do not support network virtualization.

Use the following guidelines to plan for VM networks that use network virtualization:

-   Plan for a logical network with VLAN and IP subnet settings as described in the [Guidelines for network sites: VLAN and IP subnet settings](Overview--plan-logical-networks,-network-sites,-and-IP-address-pools-in-VMM.md#BKMK_vlans_ip) section in "Overview: plan your logical networks, network sites, and IP address pools." For the logical network, you will select **One connected network** and then select **Allow new VM networks created on this logical network to use network virtualization**.

    Optionally, you can also select **Create a VM network with the same name to allow virtual machines to access this logical network directly**. Even after one such VM network is created, you can create additional VM networks that are isolated from other VM networks.

-   On top of that logical network, plan for multiple VM networks on which you will select **Isolate using Hyper\-V network virtualization**.

The following illustration shows the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] configuration for  a VM network called "AdventureWorks" that uses Hyper\-V network virtualization. The underlying logical network, "Contoso1," is configured with **Allow new VM networks created on this logical network to use network virtualization**. In the VM network, the associated IP address pools provide for static IP addressing.

![](Image/02_th_vm_netwk_nv.gif)

**Figure 2    VM networks with network virtualization**

In the illustration, bold text represents items you configure by opening a wizard or a **Properties** dialog box. Regular text represents items on a page or tab within the wizard or dialog box.

To explore older diagrams showing logical networks and VM networks, see the [!INCLUDE[sc2012r2_1](../../Token/sc2012r2_1_md.md)] topic, [Configuring VM Networks in VMM Illustrated Overview](https://technet.microsoft.com/library/jj983727.aspx).

## See Also
[How to create a VM network for a VLAN in VMM](How-to-create-a-VM-network-for-a-VLAN-in-VMM.md)
[How to create a VM network for network virtualization and add an IP address pool in VMM](How-to-create-a-VM-network-for-network-virtualization-and-add-an-IP-address-pool-in-VMM.md)
[Configuring logical networks, VM networks, and logical switches in VMM](Configuring-logical-networks,-VM-networks,-and-logical-switches-in-VMM.md)
[Managing network resources with VMM](Managing-network-resources-with-VMM.md)


