---
title: VMM networking reference: creating a custom port profile for virtual network adapters
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 159fc3d5-9733-4659-8f42-39487ec9ab2e
---
# VMM networking reference: creating a custom port profile for virtual network adapters
Whenyou configure a logical switch in Virtual Machine Manager \(VMM\), you can select from a number of built\-in port profiles for virtual network adapters. However, you can also configure a custom port profile for virtual network adapters, using the settings listed in this topic.

### To create a port profile for virtual network adapters

1.  Open the **Fabric** workspace.

2.  On the **Home** tab, in the **Show** group, click **Fabric Resources**.

3.  In the **Fabric** pane, expand **Networking**, and then click **Port Profiles**.

4.  On the **Home** tab, in the **Create** group, click **Create**, and then click **Hyper\-V Port Profile**.

    The wizard for creating port profiles opens.

5.  On the **General** page, enter a name and optional description for the port profile, click **Virtual network adapter port profile**, and then click **Next**.

6.  On the **Offload Settings** page, optionally select one or more settings, and then click **Next**. For more information about each setting, see [Offload settings for virtual network adapters](#BKMK_OffloadSettings).

7.  On the **Security Settings** page, optionally select one or more settings, and then click **Next**. For more information about each setting, see [Security settings for virtual network adapters](#BKMK_SecuritySettings).

## <a name="BKMK_OffloadSettings"></a>Offload settings for virtual network adapters
When you create a custom port profile for virtual network adapters, you can assign specific offload capabilities to the port profile. Then you can associate the port profile with logical switches that you create. Logical switches are containers for settings and capabilities that you want to apply to multiple network adapters in VMM. For more information about logical switches, see [Overview: plan logical switches and port profiles in VMM](Overview--plan-logical-switches-and-port-profiles-in-VMM.md).

The following table provides details about offload settings for virtual network adapters.

|Offload capability|Description|
|----------------------|---------------|
|**Virtual machine queue \(VMQ\)**|With VMQ, packets that are destined for a virtual network adapter are delivered directly to a queue for that adapter, and they do not have to be copied from the management operating system to the virtual machine.<br /><br />VMQ requires support from the physical network adapter.|
|**IPsec task offloading**|With this type of offloading, some or all of the computational work that IPsec requires is shifted from the computer’s CPU to a dedicated processor on the network adapter. For details about IPsec task offloading, see [What's New in Hyper-V Virtual Switch](http://technet.microsoft.com/library/jj679878.aspx).<br /><br />IPsec task offloading requires support from the physical network adapter and the guest operating system.|
|**Single\-root I\/O virtualization \(SR\-IOV\)**|With SR\-IOV, a network adapter can be assigned directly to a virtual machine. The use of SR\-IOV maximizes network throughput while minimizing network latency and minimizing the CPU overhead that is required to process network traffic.<br /><br />SR\-IOV requires support from the host hardware and firmware, the physical network adapter, and drivers in the management operating system and the guest operating system.<br /><br />To use SR\-IOV with VMM, SR\-IOV must be enabled or configured in multiple places. It must be enabled in the port profile, and in the logical switch in which you include the port profile. It must also be configured correctly on the host, when you create the virtual switch that brings together the port settings and the logical switch that you want to use on the host. In the port profile, the SR\-IOV setting is in **Offload Settings**, and in the logical switch configuration, the SR\-IOV setting is in the **General** settings. In the virtual switch, attach the port profile for virtual network adapters to the virtual switch by using a port classification. You can use the SR\-IOV port classification that is provided in VMM, or you can create your own port classification.|

## <a name="BKMK_SecuritySettings"></a>Security settings for virtual network adapters
When you create a custom port profile for virtual network adapters, you can assign specific security settings to the port profile. Then you can associate the port profile with logical switches that you create. Logical switches are containers for settings and capabilities that you want to apply to multiple network adapters in VMM. For more information about logical switches, see [Overview: plan logical switches and port profiles in VMM](Overview--plan-logical-switches-and-port-profiles-in-VMM.md).

The following table provides details about security settings for virtual network adapters.

|Security capability|Description|
|-----------------------|---------------|
|**MAC spoofing**|With media access control \(MAC\) spoofing, a virtual machine can change the source MAC address in outgoing packets to an address that is not assigned to that virtual machine. For example, a load\-balancer virtual appliance might require this setting to be enabled.|
|**DHCP guard**|With DHCP guard, you can protect against a malicious virtual machine that represents itself as a Dynamic Host Configuration Protocol \(DHCP\) server for man\-in\-the\-middle attacks.|
|**Router guard**|With router guard, you can protect against advertisement and redirection messages that are sent by an unauthorized virtual machine that represents itself as a router.|
|**Guest teaming**|With guest teaming, you can team the virtual network adapter with other network adapters that are connected to the same switch.|
|**IEEE priority tagging**|With Institute of Electrical and Electronics Engineers, Inc. \(IEEE\) priority tagging, outgoing packets from the virtual network adapter can be tagged with IEEE 802.1p priority. These priority tags can be used by Quality of Service \(QoS\) to prioritize traffic. If IEEE priority tagging is not allowed, the priority value in the packet is reset to 0.|
|**Guest specified IP addresses** \(where supported by the host\)|This affects virtual machine networks \(VM networks\) that use Hyper\-V network virtualization only. With this option, the virtual machine \(guest\) can add and remove IP addresses on this virtual network adapter. This can simplify the process of managing virtual machine settings. Guest\-specified IP addresses are required for virtual machines that use guest clustering with network virtualization. The IP address that a guest adds must be within an existing IP subnet in the VM network.|

## See Also
[VMM networking reference: illustrations, settings, and optional procedures](VMM-networking-reference--illustrations,-settings,-and-optional-procedures.md)
[How to create a logical switch in VMM](How-to-create-a-logical-switch-in-VMM.md)
[Configuring logical networks, VM networks, and logical switches in VMM](Configuring-logical-networks,-VM-networks,-and-logical-switches-in-VMM.md)
[Managing network resources with VMM](Managing-network-resources-with-VMM.md)


