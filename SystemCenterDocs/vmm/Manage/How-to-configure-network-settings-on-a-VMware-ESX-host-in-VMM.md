---
title: How to configure network settings on a VMware ESX host in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c391296f-7c63-4e56-9597-92d4616c4fc2
---
# How to configure network settings on a VMware ESX host in VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

You can use the following procedures to configure logical network settings on a VMware ESX host in Virtual Machine Manager (VMM), and to view compliance information for physical network adapters on the host.

To make logical networks available to virtual machines on an external virtual network, you must associate logical networks with physical network adapters on the ESX host. Compliance information indicates whether all IP subnets and VLANs that are included in the network site that is associated with a logical network are assigned to the physical network adapter.

## Prerequisites
Before you begin these procedures, make sure that the following prerequisites are met:

-   In the VMM console, you must have already configured the logical networks that you want to associate with the physical network adapter. For more information, see [How to create a logical network and IP address pools in VMM](How-to-create-a-logical-network-and-IP-address-pools-in-VMM.md).

    > [!NOTE]
    > By default, when you add a host to VMM management, VMM automatically creates logical networks on host physical network adapters that do not have logical networks defined. For an ESX host, the default behavior is to create logical networks that match the virtual network switch name. For more information about the default behavior, see [How to configure global network settings in VMM](How-to-configure-global-network-settings-in-VMM.md).

-   If the logical network has associated network sites, one or more of the network sites must be scoped to the host group where the ESX host resides.

> [!IMPORTANT]
> VMM does not automatically create port groups on ESX hosts. Therefore, for logical networks and associated network sites, you must use vCenter Server to configure port groups with the necessary VLANs that correspond to the network sites.

#### To associate logical networks with a physical network adapter (for an external virtual network)

1.  Open the **Fabric** workspace.

    > [!NOTE]
    > The term fabric is used to denote the infrastructure - the software, servers, high-speed connections and switches that enable access to storage devices in a network.

2.  In the **Fabric** pane, expand **Servers** > **All Hosts**, and then click the host group where the host resides.

3.  In the **Hosts** pane, click the ESX host that you want to configure.

4.  On the **Host** tab, in the **Properties** group, click **Properties**.

5.  In the *Host Name* **Properties** dialog box, click the **Hardware** tab.

6.  Under **Network Adapters**, click the physical network adapter that you want to configure.

7.  Under **Logical network connectivity**, select the check box next to each logical network that you want to associate with the physical network adapter.

    > [!NOTE]
    > Be aware that all logical networks are listed here, not just the logical networks that are available to the host group where the host resides.

    For example, if you configured a logical network called Management, and that logical network is available to the host group where the host resides, select the check box next to **Management**.

8.  To view advanced settings, click **Advanced**. In the **Advanced Network Adapter Properties** dialog box for an ESX host, you can view the IP subnets and VLANs that are available for a given logical network on the network adapter. By default, for a selected logical network, the IP subnets and VLANs that are scoped to the host group or inherited through the parent host group are assigned to the network adapter.

    > [!NOTE]
    > If no IP subnets or VLANs appear in the **Available** or **Assigned** columns, this indicates that no network site exists for the selected logical network that is scoped to the host group or inherited by the host group.

    To view the available IP subnets and VLANs, click a logical network in the **Logical network** list. As mentioned earlier, you must use vCenter Server to configure port groups with the necessary VLANs that correspond to the network sites.

    In the **Logical network** list, if the **Unassigned** option is available, you can view any VLANs that the physical network adapter is connected to, but are not included in a network site. If desired, you can define them in a network site.

9. To verify the settings, in the *Host Name* **Properties** dialog box, click the **Virtual Networks** tab. Then click a virtual network and verify that the intended logical network is listed.

#### To view compliance information for a physical network adapter

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Networking**, and then click **Logical Networks**.

3.  On the **Home** tab, in the **Show** group, click **Hosts**.

4.  In the **Logical Network Information for Hosts** pane, expand the host, and then click a physical network adapter.

5.  In the **Compliance** column, view the compliance status.

    -   A value of **Fully compliant** indicates that all subnets and VLANs that are included in the network site are assigned to the network adapter.

    -   A value of **Partially compliant** indicates that there is only a partial match between the IP subnets and VLANs that are included in the network site and what is assigned to the network adapter.

        In the details pane, the **Logical network information** section lists the assigned IP subnets and VLANs for the physical network adapter. If an adapter is partially compliant, you can view the reason why in the **Compliance errors** section.

    -   A value of **Non compliant** indicates that there are no corresponding IP subnets and VLANs that are defined for the logical network that are assigned to the physical adapter.

## See Also
[Managing VMware ESX hosts and vCenter servers with VMM](Managing-VMware-ESX-hosts-and-vCenter-servers-with-VMM.md)
[Managing network resources with VMM](Managing-network-resources-with-VMM.md)
[Managing hosts and host clusters with VMM](Managing-hosts-and-host-clusters-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)



