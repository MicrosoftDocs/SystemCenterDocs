---
title: How to bring host network adapters into compliance with logical switch settings in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cb0fe4a5-8a67-47b2-94a3-a28e614f6a15
---
# How to bring host network adapters into compliance with logical switch settings in VMM
In [!INCLUDE[vmm12sp1_long](../../Token/vmm12sp1_long_md.md)], you can review and control the configuration of virtual switches that have been created from logical switches. When such a virtual switch is first created, it complies with the settings that are configured in the logical switch. However, the settings on either the virtual switch or the logical switch might later be changed, resulting in a virtual switch that is out of compliance with the corresponding logical switch. [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] provides a straightforward way to see whether a virtual switch is out of compliance, and then to bring the virtual switch back into compliance. Bringing a virtual switch into compliance is also called remediating the virtual switch.

### To view host network adapter settings and increase compliance with logical switch settings

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Networking** > **Logical Switches**.

3.  On the **Home** tab, in the **Show** group, click **Hosts**.

4.  In the **Logical Switch Information for Hosts** pane, view the listings for network adapters and switches.

5.  Expand or collapse the listings as needed, and click an individual virtual switch for which you want to see more information.

6.  In the **Network Compliance** column, view the compliance status.

    -   A value of **Fully compliant** indicates that the settings on the virtual machine host are consistent with the configuration in [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)]. For example, **Fully compliant** indicates that all IP subnets and VLANs that are included in the network site are assigned to the network adapter.

    -   A value of **Partially compliant** indicates that there is only a partial match between the settings on the host and the configuration in [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)].

        In the results pane, the **Logical network information** section lists the assigned IP subnets and VLANs for the network adapter. If an adapter is partially compliant, you can view the reason in the **Compliance errors** section.

    -   A value of **Non compliant** indicates that the settings on the host are missing from the configuration in [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)]. For example, **Non compliant** indicates that none of the IP subnets and VLANs that are defined for the logical network are assigned to the physical adapter. If an adapter is non compliant, you can view the reason in the **Compliance errors** section.

    > [!TIP]
    > In addition to the compliance information, you can also view detailed information about the network adapter, such as the assigned IP address and media access control \(MAC\) address.

7.  To bring a non\-compliant virtual switch into compliance, click the virtual switch and, in the **Network Compliance** group, click **Remediate**. If possible, [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] will bring the virtual switch into compliance.

    If you use failover clustering, you might have to review compliance and perform remediation for virtual switches on all nodes of the cluster.

## See Also
[Configuring logical networks, VM networks, and logical switches in VMM](Configuring-logical-networks,-VM-networks,-and-logical-switches-in-VMM.md)
[Managing network resources with VMM](Managing-network-resources-with-VMM.md)
[How to configure network settings on a host by using a logical switch in VMM](How-to-configure-network-settings-on-a-host-by-using-a-logical-switch-in-VMM.md)


