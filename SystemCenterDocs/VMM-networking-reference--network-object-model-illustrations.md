---
title: VMM networking reference: network object model illustrations
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 00f72c3e-157c-4310-ad2c-b4a6e8357c4e
---
# VMM networking reference: network object model illustrations
This topic contains illustrations that show the network object model in [!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)]. The illustrations show the relationships among network objects only, rather than indicating information about the wizards through which the objects are configured in the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] console. The illustrations can be especially useful if you are learning about configuring [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] through Windows PowerShell scripts, which reflect the network object models directly.

For more general information about networking in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)], see the overview topics listed in [Configuring logical networks, VM networks, and logical switches in VMM](./Configuring-logical-networks,-VM-networks,-and-logical-switches-in-VMM.md).

The following table describes the illustrations in this topic.

-   Figure 1   [Network object model for logical networks](./VMM-networking-reference--network-object-model-illustrations.md#BKMK_logical2)

-   Figure 2   [Network object model for VM networks in a VLAN-based configuration](./VMM-networking-reference--network-object-model-illustrations.md#BKMK_VLAN2)

-   Figure 3   [Network object model for VM networks configured with network virtualization](./VMM-networking-reference--network-object-model-illustrations.md#BKMK_virtualization2)

-   Figure 4   [Network object model for a VM network that provides direct access to the logical network](./VMM-networking-reference--network-object-model-illustrations.md#BKMK_direct2)

-   Figure 5   [Network object model for VM networks configured with an external network service](./VMM-networking-reference--network-object-model-illustrations.md#BKMK_vendor2)

-   Figure 6   [Network object model for logical switches](./VMM-networking-reference--network-object-model-illustrations.md#BKMK_switch)

## <a name="BKMK_logical2"></a>Network object model for logical networks
The following illustration shows the network object model for logical networks in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)]. The illustration shows the relationships among network objects only, rather than indicating information about the wizards and property sheets through which the objects are configured in the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] console. The illustration can be especially useful if you are learning about configuring [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] through Windows PowerShell scripts, which reflect the network object models directly.

For some objects, sample names such as “Contoso1” and “Building1” are included to help illustrate the purpose of those objects. \(The object labeled “Network site” is also known as a “logical network definition.”\)

![](/Image/01_VMM_Net_Obj.gif)

**Figure 1   Object model for logical networks**

The following key explains the notations on the arrows:

-   **1\-1** means “one\-to\-one.”

-   **1\-M** means “one\-to\-many.”

-   **M\-M** means “many\-to\-many.”

## Network object models for VM networks in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)]
The following illustrations show the network object models for logical networks and VM networks in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)]. These illustrations show the relationships among network objects only, rather than indicating information about the wizards and property sheets through which the objects are configured in the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] console. The illustrations can be especially useful if you are learning about configuring [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] through Windows PowerShell scripts, which reflect the network object models directly.

### <a name="BKMK_VLAN2"></a>Network object model for VM networks in a VLAN\-based configuration
The following illustration shows the network object model for VM networks in a VLAN\-based configuration.

![](/Image/02b_VMM_Net_Obj_upd.gif)

**Figure 2   Object model for VM networks in a VLAN\-based configuration**

The following key explains the notations on the arrows:

-   **1\-1** means “one\-to\-one.”

-   **1\-M** means “one\-to\-many.”

-   **M\-1** means “many\-to\-one.”

### <a name="BKMK_virtualization2"></a>Network object model for VM networks configured with network virtualization
The following illustration shows the network object model for VM networks that are configured with network virtualization.

For some objects, sample names such as “AdventureWorks” and “Contoso1” are included to help illustrate the purpose of those objects.

![](/Image/02_VMM_Net_Obj.gif)

**Figure 3   Object model for VM networks configured with network virtualization**

As indicated in the illustration, the IP addresses on the VM network are also called the “customer address \(CA\) space” because these IP addresses are used by customers \(or clients or tenants\). The IP addresses on the logical network are also called the “provider address \(PA\) space” because these IP addresses are used by providers \(or hosters\).

The notation **1\-M** means “one\-to\-many.”

### <a name="BKMK_direct2"></a>Network object model for a VM network that provides direct access to the logical network
The following illustration shows the network object model for a VM network that provides direct access to the logical network, with no isolation. This is the simplest configuration, where the VM network is the same as the logical network on which it is configured.

![](/Image/02c_VMM_Net_Obj.gif)

**Figure 4   Object model for a VM network that provides direct access to the logical network**

The following key explains the notations on the arrows:

-   **1\-1** means “one\-to\-one.”

-   **1\-M** means “one\-to\-many.”

### <a name="BKMK_vendor2"></a>Network object model for VM networks configured with an external network service
The following illustration shows the network object model for VM networks that are configured with a network service, such as a vendor network\-management console that works with a forwarding extension. This configuration uses a virtual switch extension manager to enable communication with the vendor network\-management console.

![](/Image/02d_VMM_Net_Obj_Ext_upd.gif)

**Figure 5   Object model for VM networks configured with a network service such as a vendor network\-management console**

The following key explains the notations on the arrows:

-   **1\-1** means “one\-to\-one.”

-   **1\-M** means “one\-to\-many.”

## <a name="BKMK_switch"></a>Network object model for logical switches
The following illustration shows the network object model for logical switches in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] in [!INCLUDE[sc_threshold_1](./Token/sc_threshold_1_md.md)]. This illustration shows the relationships among network objects only, rather than indicating information about the wizards and property sheets through which the objects are configured in the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] console. The illustration can be especially useful if you are learning about configuring [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] through Windows PowerShell scripts, which reflect the network object models directly.

For some objects in the illustration, sample names such as “Switch for central buildings” and “High\-bandwidth DB” are included to help illustrate the purpose of those objects. Two of the objects, the **Set of uplink port profiles** and the **Set of port profiles for virtual network adapters**, are visible in Windows PowerShell, but not in the [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] console.

![](/Image/03_VMM_Net_Obj.gif)

**Figure 6   Object model for logical switches**

As indicated in the illustration, the view of the self\-service user includes only port classifications, not other port or switch objects. By choosing a port classification, for example, “High\-bandwidth DB,” the self\-service user can easily choose an appropriate collection of settings for a particular virtual network adapter. Port classifications are created by a fabric administrator or tenant administrator, and they are made available in the cloud.

The following key explains the notations on the arrows:

-   **1\-1** means “one\-to\-one.”

-   **1\-M** means “one\-to\-many.”

-   **M\-1** means “many\-to\-one.”

-   **M\-M** means “many\-to\-many.”

## See Also
[VMM networking reference: illustrations, settings, and optional procedures](./VMM-networking-reference--illustrations,-settings,-and-optional-procedures.md)
[Configuring logical networks, VM networks, and logical switches in VMM](./Configuring-logical-networks,-VM-networks,-and-logical-switches-in-VMM.md)
[Managing network resources with VMM](./Managing-network-resources-with-VMM.md)


