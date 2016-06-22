---
title: VMM networking reference: IP address pool requirements for multicasting or broadcasting
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aad9a045-1f25-4297-aab1-fba7c502d7b5
---
# VMM networking reference: IP address pool requirements for multicasting or broadcasting
If you are using network virtualization on your VM networks, you can support an application that requires multicasting or broadcasting on the VM networks. To do this, you must create an IP address pool that supports multicasting, and you must follow several other configuration requirements. \(For information about what it means to use network virtualization on a VM network, see [Prerequisites for gateways in VMM](Prerequisites-for-gateways-in-VMM.md).\) The requirements for using multicasting or broadcasting on a VM network are as follows:

-   The logical network that you create must have network virtualization enabled.

-   You must configure an IP address pool on the logical network and select the multicast setting for the pool.

    Note that in the Create Static IP Address Pool Wizard, the multicast setting is visible only if the pool is created on a logical network \(not on a VM network\) and if network virtualization is enabled on that logical network.

-   For the VM network in which you want to support multicasting, the IP protocol setting \(either IPv4 or IPv6\) must match the IP protocol setting for the underlying logical network. To configure this, in the Create VM Network Wizard, on the **Isolation** page of the wizard, select the same IP address protocol \(IPv4 or IPv6\) for both the logical network and the VM network.

    Note that after you finish creating the VM network, you cannot view this protocol setting in the VMM management console. Instead, run the Windows PowerShell cmdlet [Get-SCVMNetwork](http://technet.microsoft.com/library/jj613172.aspx) to view the setting. Use the following syntax, where `<VMNetworkName>` is the name of your VM network:

    `Get-SCVMNetwork –Name <VMNetworkName> | Format-List Name, IsolationType, *PoolType`

    In the display, a protocol \(IPv4 or IPv6\) is listed for the pool type:

    |Pool type as listed in the display|Description|
    |--------------------------------------|---------------|
    |**PAIPAddressPoolType**|**PA or "provider addressing"**: IP addresses in the logical network|
    |**CAIPAddressPoolType**|**CA or "customer addressing"**: IP addresses in the VM network|

When these configuration steps are complete, multicast and broadcast packets on the VM network will use the IP addresses from the multicast IP address pool. Within each VM network, each subnet that you configure will consume one IP address from the multicast pool.

## See Also
[Overview: plan logical networks, network sites, and IP address pools in VMM](Overview--plan-logical-networks,-network-sites,-and-IP-address-pools-in-VMM.md)
[Prerequisites for gateways in VMM](Prerequisites-for-gateways-in-VMM.md)
[How to create a logical network and IP address pools in VMM](How-to-create-a-logical-network-and-IP-address-pools-in-VMM.md)
[VMM networking reference: illustrations, settings, and optional procedures](VMM-networking-reference--illustrations,-settings,-and-optional-procedures.md)
[Managing network resources with VMM](Managing-network-resources-with-VMM.md)


