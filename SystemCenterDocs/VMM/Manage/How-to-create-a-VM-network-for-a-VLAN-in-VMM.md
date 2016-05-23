---
title: How to create a VM network for a VLAN in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dba9273e-008e-4f21-a3cf-52f9b1530f60
---
# How to create a VM network for a VLAN in VMM
You can use familiar virtual local area network \(VLAN\) technology for network isolation, and manage your configuration in [!INCLUDE[vmm12sp1_long](../../Token/vmm12sp1_long_md.md)] by creating VM networks for your VLANs. To plan your VM networks, see [Plan VM networks for a VLAN-based configuration](Overview--plan-VM-networks-in-VMM.md#BKMK_VLAN). To see how this procedure fits into an overall workflow, see [Implementing the configuration](Configuring-logical-networks,-VM-networks,-and-logical-switches-in-VMM.md#BKMK_implementing) in "Configuring logical networks, VM networks, and logical switches in VMM."

> [!NOTE]
> A "VLAN\-based configuration" means a configuration where VLANs are used for isolation, not just for broadcast boundaries.

When you create a VM network for a VLAN, if there are IP address pools configured on the underlying logical network \(specifically, in the network site for that VLAN\), the IP address pools automatically become available on the VM network. For more information, see [Guidelines for IP address pools](Overview--plan-logical-networks,-network-sites,-and-IP-address-pools-in-VMM.md#BKMK_address_pools) in "Overview: plan logical networks, network sites, and IP address pools in VMM."

## <a name="BKMK_VMN"></a>Create a VM network on a logical network that uses VLANs for isolation
To perform this procedure, you must already have a logical network that uses the **VLAN\-based independent networks** option. \(The exception is with private VLAN technology, in which case the logical network can use the **Private VLAN \(PVLAN\) networks** option.\)

#### To create a VM network on a logical network that uses VLANs for isolation

1.  Open the **VMs and Services** workspace.

2.  On the **Home** tab, in the **Show** group, click **VM Networks**.

3.  In the **VMs and Services** pane, click **VM Networks**.

4.  On the **Home** tab, in the **Create** group, click **Create VM Network**.

    The Create VM Network Wizard opens.

5.  On the **Name** page, type a name and an optional description, and then in the **Logical network** list, select a logical network. Click **Next**.

    > [!NOTE]
    > The wizard pages and VM network properties that you can configure will vary depending on the properties of the logical network that you selected.

6.  On the **Isolation Options** page, select one of the following options, and then click **Next**. If you do not see these options, confirm that you selected a logical network that uses either the **VLAN\-based independent networks** option or the **Private VLAN \(PVLAN\) networks** option, or see the links listed at the end of this topic.

    -   **Automatic** Select this option to have [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] automatically configure the isolation of the VM network. [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] will select a network site and subnet VLAN, based on those that are available on the logical network.

    -   **Specify a VLAN** Select this option to manually configure the isolation of the VM network, and then select the **Network site** and **Subnet VLAN**.

        > [!NOTE]
        > This option is available only to Administrators and Fabric Administrators \(Delegated Administrators\). Tenant Administrators can select only the **Automatic** option.

7.  On the **Summary** page, review and confirm the settings, and then click **Finish**.

8.  Verify that the VM network appears in the **VM Networks and IP Pools** pane.

After a virtual machine has been deployed in [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)], you can view the IP address or addresses assigned to that virtual machine. To do this, right\-click the listing for the virtual machine, click **Properties**, click the **Hardware Configuration** tab, click the network adapter, and in the results pane, click the **Connection details** button.

> [!IMPORTANT]
> If you configure a virtual machine to obtain a static IP address from an IP address pool, you must also configure the virtual machine to use a static MAC address. You can either specify the MAC address manually \(during the **Configure Settings** step\) or have [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] automatically assign a MAC address from a MAC address pool.
> 
> This requirement for static MAC addresses is necessary because [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] uses the MAC address to identify which network adapter to set the static IP address to, and this identification must happen before the virtual machine starts. Identifying the network adapter is especially important if a virtual machine has multiple adapters. If the MAC addresses were assigned dynamically through Hyper\-V, [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] could not consistently identify the correct adapter to set a static IP address on.
> 
> [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] provides static MAC address pools by default, but you can customize the pools. [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] provides static MAC address pools by default, but you can customize the pools, as described in [VMM networking reference: creating custom MAC address pools in VMM](VMM-networking-reference--creating-custom-MAC-address-pools-in-VMM.md).

## See Also
[Overview: plan VM networks in VMM](Overview--plan-VM-networks-in-VMM.md)
[How to create a VM network for network virtualization and add an IP address pool in VMM](How-to-create-a-VM-network-for-network-virtualization-and-add-an-IP-address-pool-in-VMM.md)
[Configuring logical networks, VM networks, and logical switches in VMM](Configuring-logical-networks,-VM-networks,-and-logical-switches-in-VMM.md)
[Managing network resources with VMM](Managing-network-resources-with-VMM.md)


