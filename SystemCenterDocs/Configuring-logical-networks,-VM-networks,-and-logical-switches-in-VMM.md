---
title: Configuring logical networks, VM networks, and logical switches in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4d44a1f8-4046-4a97-b10b-30f67fa438ea
---
# Configuring logical networks, VM networks, and logical switches in VMM
You can use [!INCLUDE[vmm12sp1_long](Token/vmm12sp1_long_md.md)] to manage your physical and virtualized network infrastructure. In [!INCLUDE[vmm12short](Token/vmm12short_md.md)], the foundations of the network configuration are networks—the underlying logical networks and the VM networks—and switches. Switches can be configured as standard virtual switches, but this set of topics describes logical switches, which help you configure switch settings consistently across multiple hosts. To configure these network elements in [!INCLUDE[vmm12short](Token/vmm12short_md.md)], use the following overviews and procedures, in the order shown.

## <a name="BKMK_planning"></a>Planning the configuration and configuring global settings
Use the following overviews to plan your configuration:

1.  **Logical networks**: [Overview: plan logical networks, network sites, and IP address pools in VMM](Overview--plan-logical-networks,-network-sites,-and-IP-address-pools-in-VMM.md)

2.  **VM networks**: [Overview: plan VM networks in VMM](Overview--plan-VM-networks-in-VMM.md)

3.  **Logical switches**: [Overview: plan logical switches and port profiles in VMM](Overview--plan-logical-switches-and-port-profiles-in-VMM.md)

Optionally, configure global network settings, which have an effect only when you add a host to [!INCLUDE[vmm12short](Token/vmm12short_md.md)] and you don't have any logical networks associated with physical network adapters on that host. In that situation, [!INCLUDE[vmm12short](Token/vmm12short_md.md)] can use your settings to create a logical network automatically:

-   [How to configure global network settings in VMM](How-to-configure-global-network-settings-in-VMM.md)

## <a name="BKMK_implementing"></a>Implementing the configuration
After you have planned your logical networks, VM networks, and logical switches \(and the elements within them, such as network sites within logical networks\), use the following procedures, in order, to create your network configuration in [!INCLUDE[vmm12short](Token/vmm12short_md.md)]:

1.  **Logical networks**: [How to create a logical network and IP address pools in VMM](How-to-create-a-logical-network-and-IP-address-pools-in-VMM.md)

2.  **VM networks**: Choose the procedure that applies to your environment:

    -   [How to create a VM network for a VLAN in VMM](How-to-create-a-VM-network-for-a-VLAN-in-VMM.md)

    -   [How to create a VM network for network virtualization and add an IP address pool in VMM](How-to-create-a-VM-network-for-network-virtualization-and-add-an-IP-address-pool-in-VMM.md)

3.  **Logical switches** \(creating\): [How to create a logical switch in VMM](How-to-create-a-logical-switch-in-VMM.md)

4.  **Logical switches** \(applying settings to host\): [How to configure network settings on a host by using a logical switch in VMM](How-to-configure-network-settings-on-a-host-by-using-a-logical-switch-in-VMM.md)

Depending on your environment, you might also use the following procedures, for example, if you want to convert the switch on a host from a "standard" virtual switch to a logical switch:

-   [How to convert a host's virtual switch to a logical switch in VMM](How-to-convert-a-host-s-virtual-switch-to-a-logical-switch-in-VMM.md)

-   [How to bring host network adapters into compliance with logical switch settings in VMM](How-to-bring-host-network-adapters-into-compliance-with-logical-switch-settings-in-VMM.md)

## See Also
[Managing network resources with VMM](Managing-network-resources-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


