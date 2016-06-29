---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  Overview  plan logical switches and port profiles in VMM
ms.technology:  virtual-machine-manager
ms.assetid:  bd5d1337-fd15-4c00-a07e-a2e02286cd8d
---

# Overview: plan logical switches and port profiles in VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

In Virtual Machine Manager (VMM), you can use logical switches (and the port profiles inside them) to help you configure switch settings consistently across multiple hosts. A logical switch is like a template for a virtual switch�it acts as a container for the switch settings and capabilities that you want to use. Instead of configuring switch settings individually for each network adapter, you can specify settings and capabilities in a logical switch, and then use the logical switch to apply those settings consistently across network adapters on multiple hosts.

For a series of videos that illustrate the process of creating and  using a logical switch in System Center 2012 R2, which is similar  to (though not the same as) the process for System Center 2016 Technical Preview, see [Virtual Machine Manager Network Object Fundamentals](https://technet.microsoft.com/library/mt156974.aspx).

To plan your logical switch, go through the sections that apply to your requirements:

|Section in this topic|Description|
|-------------------------|---------------|
|[Review how a logical switch acts as a container for network settings](Overview--plan-logical-switches-and-port-profiles-in-VMM.md#BKMK_illustration)|Illustrates a logical switch, showing it as a container for port profiles and port classifications.|
|[Review the purposes that your networks serve](Overview--plan-logical-switches-and-port-profiles-in-VMM.md#BKMK_purposes)|Lists common purposes that networks serve. Identifying your networks' purposes can make it easier to choose virtual port settings for a logical switch.|
|[Review your IP addressing, VLANs, any switch extensions, and other basic network characteristics](Overview--plan-logical-switches-and-port-profiles-in-VMM.md#BKMK_IP_VLAN)|Helps you review the following as you plan your logical switch:<br /><br />-   IP addressing and VLANs as reflected in your logical networks and VM networks<br />-   The switch extensions and providers that you use in your environment<br />-   The network managers (virtual switch extension managers) that you use in your environment<br />-   Whether you will use NIC teaming<br />-   Whether you will configure bandwidth settings|
|[Optional: review load-balancing algorithm and  teaming mode](Overview--plan-logical-switches-and-port-profiles-in-VMM.md#BKMK_modes)|Helps you review NIC teaming settings you might configure in your logical switch|
|[Optional: review options for configuring bandwidth](Overview--plan-logical-switches-and-port-profiles-in-VMM.md#BKMK_bandwidth)|Helps you review bandwidth settings you might configure in your logical switch|

## <a name="BKMK_illustration"></a>Review how a logical switch acts as a container for network settings
The following illustration shows how a logical switch acts as a template or container for switch settings or capabilities that you want to use. At the top of the illustration, in the host group �Test systems,� there is a single test system on which the administrator has configured switch and port settings individually. Lower in the illustration, there are multiple hosts in host groups, to which a logical switch has been applied. The logical switch helps ensure that switch and port settings are applied consistently across the host systems.


> [!NOTE]
> When you add an uplink port profile to a logical switch, it's placed in a list of profiles in the logical switch. Then, when you select that logical switch for a network adapter in a host, you can open the list and select the uplink port profile for that network adapter. This helps you to create consistency in the settings across multiple hosts, but also adjust the settings for a given network adapter.

## <a name="BKMK_purposes"></a>Review the purposes that your networks serve
To begin to plan logical switches (and the port profiles that are included in them), it's helpful to identify the purposes that your networks serve. The following list shows typical purposes that you might identify for your networks. As you configure a logical switch, you can choose from among VMM's built-in port profiles (and the port classifications you associate with them) for networks that serve these purposes:

-   Host management

-   Network virtualization

-   Guest dynamic IP addressing

-   Live migration

-   Cluster communication

-   iSCSI

-   Network load balancing

-   SR-IOV

The built-in port profiles and port classifications in VMM are designed for the preceding list of purposes. As needed, you can create custom port profiles and port classifications. For more information, see [VMM networking reference: creating a custom port profile for virtual network adapters](VMM-networking-reference--creating-a-custom-port-profile-for-virtual-network-adapters.md) and [VMM networking reference: creating a port classification in VMM](VMM-networking-reference--creating-a-port-classification-in-VMM.md).

## <a name="BKMK_IP_VLAN"></a>Review your IP addressing, VLANs, any switch extensions, and other basic network characteristics
As you plan for logical switches, it's helpful to review the following aspects of your networks:

-   **IP addressing and VLANs as reflected in your logical networks and VM networks**: Review the names of the logical networks (specifically, the network sites) and VM networks that represent your network configuration. You will select logical networks, network sites, and VM networks as you configure a logical switch.

    If you have not configured logical networks or VM networks yet, see [Configuring logical networks, VM networks, and logical switches in VMM](Configuring-logical-networks,-VM-networks,-and-logical-switches-in-VMM.md).

-   **Switch extensions and providers**: Switch extensions are software that you can install on the VMM management server and then include in a logical switch. Switch extensions allow you to monitor network traffic, use Quality of Service (QoS) to control how network bandwidth is used, enhance the level of security, or otherwise expand the capabilities of a switch.

    If you're using switch extensions (which usually require provider software), determine whether they are Microsoft software�for example, included in Windows Server Technical Preview. If they're not, before creating a logical switch, be sure the vendor's provider software is installed on the VMM management server. If you have installed a high-availability VMM management server on a cluster, be sure to install the provider on all nodes of the cluster. For more information, refer to documentation from the vendor. After you install the provider, restart the System Center Virtual Machine Manager service.

    After these steps are completed, and you are proceeding through the **Create Logical Switch Wizard**, your extension will be displayed in a list in the wizard, and you'll be able to select it. In VMM, four types of switch extensions are supported:

    -   **Monitoring** extensions can be used to monitor and report on network traffic, but they cannot modify packets.

    -   **Capturing** extensions can be used to inspect and sample traffic, but they cannot modify packets.

    -   **Filtering** extensions can be used to block, modify, or defragment packets. They can also block ports.

    -   **Forwarding** extensions can be used to direct traffic by defining destinations, and they can capture and filter traffic. To avoid conflicts, only one forwarding extension can be active on a logical switch.

-   **Virtual switch extension manager and provider**: A virtual switch extension manager is also called a network manager or forwarding extension manager. If you're using a virtual switch extension manager for managing a given network (which usually requires provider software), determine whether it is Microsoft software. If it's not, be sure the vendor's provider software is installed on the VMM management server. If you have installed a high-availability VMM management server on a cluster, be sure to install the provider on all nodes of the cluster. For more information, refer to documentation from the vendor. After you install the provider, restart the System Center Virtual Machine Manager service.

    After you have completed these steps, add the virtual switch extension manager to VMM as described in [VMM networking reference: using a virtual switch extension manager or network manager in VMM](VMM-networking-reference--using-a-virtual-switch-extension-manager-or-network-manager-in-VMM.md). After it has been added, settings can be imported into and exported out of VMM. That is, you can configure and view settings either in VMM or your network manager, and the two interfaces synchronize with each other.

-   **NIC teaming and related settings**: Review whether you want to use NIC Teaming, also known as load balancing and failover (LBFO), for your network adapters. With NIC Teaming, you can use default settings for the load-balancing algorithm and teaming mode, or choose settings that fit your environment. For descriptions, see [Load-balancing algorithm](Overview--plan-logical-switches-and-port-profiles-in-VMM.md#BKMK_algorithm) and [Teaming mode](Overview--plan-logical-switches-and-port-profiles-in-VMM.md#BKMK_teaming), later in this topic.

-   **Bandwidth and bandwidth allocation**: Review your networks according to bandwidth: low, medium, or high. Also review the relative importance of different kinds of network traffic. This makes it easier for you to decide on the "Minimum bandwidth mode" and minimum bandwidth settings, which together help ensure that adequate bandwidth is set aside for important types of network communication when traffic is heavy. For more information, see [Minimum bandwidth modes](Overview--plan-logical-switches-and-port-profiles-in-VMM.md#BKMK_bandwidth), later in this topic.

## <a name="BKMK_modes"></a>Optional: review load-balancing algorithm and  teaming mode
If you plan to enable NIC teaming in your logical switch, review the details in the following sections in this topic:

-   [Load-balancing algorithm](Overview--plan-logical-switches-and-port-profiles-in-VMM.md#BKMK_algorithm)

-   [Teaming mode](Overview--plan-logical-switches-and-port-profiles-in-VMM.md#BKMK_teaming)

### <a name="BKMK_algorithm"></a>Load-balancing algorithm
To enable teaming of network adapters, you can configure teaming settings in a logical switch, then use that logical switch to apply the settings consistently across multiple network adapters. In the logical switch, for the **Uplink mode**, select **Team**, and configure the **Load-balancing algorithm** setting as described in this section (also see [Teaming mode](Overview--plan-logical-switches-and-port-profiles-in-VMM.md#BKMK_teaming), later in this topic).

With NIC teaming, the load-balancing algorithm determines how network traffic is distributed between the network adapters. You can use the default load-balancing algorithm selected in the wizard, or choose from the following table. Note that if you do not enable teaming in the logical switch, this option will have no effect.

For background information about load-balancing algorithms and teaming modes, see [NIC Teaming Overview](http://technet.microsoft.com/library/hh831648.aspx).

|Load-balancing algorithm|Description|
|-----------------------------|---------------|
|**Hyper-V Port**|Distributes network traffic based on the Hyper-V switch port identifier of the source virtual machine. This is the default algorithm.|
|**Transport Ports**|Uses the source and destination TCP ports and the IP addresses to create a hash and then assigns the packets that have that hash value to one of the available network adapters.|
|**IP Addresses**|Uses the source and destination IP addresses to create a hash and then assigns the packets that have that hash value to one of the available network adapters.|
|**Mac Addresses**|Uses the source and destination MAC addresses to create a hash and then assigns the packets that have that hash value to one of the available network adapters.|
|**Dynamic**|Uses the dynamic load balancing that is available in Windows Server Technical Preview and Windows Server 2012 R2 only.|
|**Host default**|This specifies the **Dynamic** algorithm for hosts that support it, and the **Hyper-V Port** algorithm for hosts that do not.|

### <a name="BKMK_teaming"></a>Teaming mode
To enable teaming of network adapters, you can configure teaming settings in a logical switch, then use that logical switch to apply the settings consistently across multiple network adapters. In the logical switch, for the **Uplink mode**, select **Team**, and configure the **Teaming mode** setting as described in this section (also see [Load-balancing algorithm](Overview--plan-logical-switches-and-port-profiles-in-VMM.md#BKMK_algorithm), earlier in this topic).

You can use the default teaming mode selected in the wizard, or choose from the following list. Note that if you do not enable teaming in the logical switch, this option will have no effect.

For background information about load-balancing algorithms and teaming modes, see [NIC Teaming Overview](http://technet.microsoft.com/library/hh831648.aspx).

|Teaming mode|Description|
|----------------|---------------|
|**Switch Independent**|Specifies that a network switch configuration is not needed for the NIC team. Because the network switch is not configured to know about the interface teaming, the team interfaces can be connected to different switches. This is the default mode.|
|**LACP**|Uses the Link Aggregation Control Protocol (LACP) from IEEE 802.1ax (also known as IEEE 802.3ad) to dynamically identify links that are connected between the host and a given switch.|
|**Static Teaming**|Requires configuration on both the switch and the host to identify which links form the team.|

## <a name="BKMK_bandwidth"></a>Optional: review options for configuring bandwidth
You can control how bandwidth is used on network adapters by setting the minimum bandwidth mode, and where applicable, minimum bandwidth values. The following table describes the bandwidth modes.

|Bandwidth mode|Description|
|------------------|---------------|
|**Default**|The mode will be set to **Absolute** if the switch is not SR-IOV-enabled, or **None** if the switch is SR-IOV-enabled.|
|**Weight**|Minimum bandwidth is a weighted value ranging from 1 to 100.|
|**Absolute**|Minimum bandwidth is bits per second.|
|**None**|Minimum bandwidth is disabled on the switch. Users cannot configure minimum bandwidth on any network adapter connected to the switch.|





