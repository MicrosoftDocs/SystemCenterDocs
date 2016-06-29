---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  How to view compliance information for a physical network adapter on a host in VMM
ms.technology:  virtual-machine-manager
ms.assetid:  4bc6b71e-39d5-4053-972a-61675154bd2c
---

# How to view compliance information for a physical network adapter on a host in VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

Compliance information lets you see whether the settings on physical network adapters on a host are consistent with the configuration in Virtual Machine Manager (VMM). For example, you can see whether all the IP subnets and VLANs that are included in a network site in a logical network are assigned to a physical network adapter.

If you want more detail about compliance information for logical switches, see [How to bring host network adapters into compliance with logical switch settings in VMM](How-to-bring-host-network-adapters-into-compliance-with-logical-switch-settings-in-VMM.md) instead.

### To view compliance information for a physical network adapter

1.  In the VMM console, open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Networking**, and then click **Logical Networks**.

3.  On the **Home** tab, in the **Show** group, click **Hosts**.

4.  In the **Logical Network Information for Hosts** pane, expand the host, and then click a physical network adapter.

5.  In the **Network Compliance** column, view the compliance.

    |||
    |-|-|
    |**Fully compliant**|All IP subnets and VLANs that are included in the network site are assigned to the network adapter.|
    |**Partially compliant**|If you compare the IP subnets and VLANs that are included in the network site with those that are assigned to the network adapter, there is only a partial match.<br /><br />In the details pane, the **Logical network information** section lists the assigned IP subnets and VLANs for the physical network adapter. If an adapter is partially compliant, you can view the reason in the **Compliance errors** section.|
    |**Non compliant**|None of the IP subnets and VLANs that are defined for the logical network are assigned to the physical network adapter.|

    > [!TIP]
    > In addition to the compliance information, you can also view detailed information about the physical network adapter, such as the assigned IP address and MAC address, and the associated virtual networks.

## See Also
[Overview: plan logical networks, network sites, and IP address pools in VMM](Overview--plan-logical-networks,-network-sites,-and-IP-address-pools-in-VMM.md)
[How to configure network settings on a Hyper-V host in VMM](How-to-configure-network-settings-on-a-Hyper-V-host-in-VMM.md)
[How to configure network settings on a host by using a logical switch in VMM](How-to-configure-network-settings-on-a-host-by-using-a-logical-switch-in-VMM.md)
[How to create a logical network and IP address pools in VMM](How-to-create-a-logical-network-and-IP-address-pools-in-VMM.md)
[How to bring host network adapters into compliance with logical switch settings in VMM](How-to-bring-host-network-adapters-into-compliance-with-logical-switch-settings-in-VMM.md)
[Configuring Hyper-V host properties in VMM](Configuring-Hyper-V-host-properties-in-VMM.md)
[Managing Hyper-V hosts and host clusters with VMM](Managing-Hyper-V-hosts-and-host-clusters-with-VMM.md)
[Managing hosts and host clusters with VMM](Managing-hosts-and-host-clusters-with-VMM.md)
[Managing network resources with VMM](Managing-network-resources-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)



