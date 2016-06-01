---
title: VMM networking reference: creating an uplink port profile in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 25392668-5bc2-42ea-b6ea-293a191b57fa
---
# VMM networking reference: creating an uplink port profile in VMM
When you configure a logical switch, you can also create an uplink port profile. However, you can create uplink port profiles outside of the Create Logical Switch Wizard, using the settings listed in this topic.

> [!IMPORTANT]
> For information about prerequisites and settings for port profiles and logical switches, see [Overview: plan logical switches and port profiles in VMM](Overview--plan-logical-switches-and-port-profiles-in-VMM.md).

### To create an uplink port profile

1.  Open the **Fabric** workspace.

2.  On the **Home** tab, in the **Show** group, click **Fabric Resources**.

3.  In the **Fabric** pane, expand **Networking**, and then click **Port Profiles**.

4.  On the **Home** tab, in the **Create** group, click **Create**, and then click **Hyper\-V Port Profile**.

    The wizard for creating port profiles opens.

5.  On the **General** page, enter a name and optional description for the port profile, and then select **Uplink port profile**. If you plan to enable teaming in the logical switch that includes this uplink port profile, select options for load balancing and teaming, or use the default options. Note that if you do not enable teaming in the logical switch, these options will have no effect.

    > [!NOTE]
    > For more information about the options in the list that follows, see [NIC Teaming Overview](http://technet.microsoft.com/library/hh831648.aspx).

    The options for load balancing and teaming are as follows:

    **Load\-balancing algorithm**: the algorithm that the team uses to distribute network traffic between the network adapters. The following options are available:

    -   **Hyper\-V Port**: Distributes network traffic based on the Hyper\-V switch port identifier of the source virtual machine. This is the default algorithm.

    -   **Transport Ports**: Uses the source and destination TCP ports and the IP addresses to create a hash and then assigns the packets that have that hash value to one of the available network adapters.

    -   **IP Addresses**: Uses the source and destination IP addresses to create a hash and then assigns the packets that have that hash value to one of the available network adapters.

    -   **Mac Addresses**: Uses the source and destination MAC addresses to create a hash and then assigns the packets that have that hash value to one of the available network adapters.

    -   **Dynamic**: Uses the dynamic load balancing that is available in [!INCLUDE[winthreshold_server_2](../../includes/winthreshold_server_2_md.md)] and [!INCLUDE[winblue_server_2](../../includes/winblue_server_2_md.md)] only.

    -   **Host default**: This specifies the **Dynamic** algorithm for hosts that support it, and the **Hyper\-V Port** algorithm for hosts that do not.

    **Teaming mode**: the mode of the NIC teaming. The following options are available:

    -   **Switch Independent**: Specifies that a network switch configuration is not needed for the NIC team. Because the network switch is not configured to know about the interface teaming, the team interfaces can be connected to different switches. This is the default mode.

    -   **LACP**: Uses the Link Aggregation Control Protocol \(LACP\) from IEEE 802.1ax \(also known as IEEE 802.3ad\) to dynamically identify links that are connected between the host and a given switch.

    -   **Static Teaming**: Requires configuration on both the switch and the host to identify which links form the team.

    After you have completed all settings, click **Next**.

6.  On the **Network configuration** page, do the following:

    -   Select one or more network sites for this uplink port profile to support.

    -   If you want to enable network virtualization \(which allows you to deploy multiple VM networks on the same physical network\), select **Enable Hyper\-V Network Virtualization**.

        > [!NOTE]
        > The setting for enabling network virtualization requires a logical network on which you have selected **Allow new VM networks created on this logical network to use network virtualization**.

    -   After you have completed all settings, click **Next**.

7.  On the **Summary** page, review and confirm the settings, and then click **Finish**.

## See Also
[Configuring logical networks, VM networks, and logical switches in VMM](Configuring-logical-networks,-VM-networks,-and-logical-switches-in-VMM.md)
[VMM networking reference: illustrations, settings, and optional procedures](VMM-networking-reference--illustrations,-settings,-and-optional-procedures.md)
[Managing network resources with VMM](Managing-network-resources-with-VMM.md)


