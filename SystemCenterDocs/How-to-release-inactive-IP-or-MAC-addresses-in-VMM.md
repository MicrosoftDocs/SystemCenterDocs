---
title: How to release inactive IP or MAC addresses in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ff59f3fe-d82d-416a-bc14-b779b6cc3a3f
---
# How to release inactive IP or MAC addresses in VMM
You can use the following procedure to release inactive IP addresses and MAC addresses. When you release an inactive address, [!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)] returns the address to the static IP address or MAC address pool, and considers it available for reassignment. An IP or MAC address is considered inactive when either of the following conditions is true:

-   A host that was assigned a static IP address through the bare\-metal deployment process is removed from [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] management. When you remove the host, any IP and MAC addresses that were statically assigned to virtual machines on the host are also marked as inactive.

-   A virtual machine goes into a missing state because it was removed outside [!INCLUDE[vmm12short](./Token/vmm12short_md.md)].

### To release inactive IP addresses

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Networking** > **Logical Networks**.

3.  On the **Home** tab, in the **Show** group, click **Fabric Resources**.

4.  In the **Logical Networks and IP Pools** pane, expand the logical network, and then click the desired IP address pool.

5.  On the **Home** tab, in the **Properties** group, click **Properties**.

6.  Click the **Inactive addresses** tab.

7.  Select the check box next to each inactive IP address that you want to release, or select the check box in the table header row to select all the addresses, and then click **Release**.

### To release inactive MAC addresses

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Networking** > **MAC Address Pools**.

3.  On the **Home** tab, in the **Show** group, click **Fabric Resources**.

4.  In the **MAC Pools** pane, click the desired MAC address pool.

5.  On the **Home** tab, in the **Properties** group, click **Properties**.

6.  Click the **Inactive addresses** tab.

7.  Select the check box next to each inactive MAC address that you want to release, or select the check box in the table header row to select all the addresses, and then click **Release**.

## See Also
[VMM networking reference: creating custom MAC address pools in VMM](./VMM-networking-reference--creating-custom-MAC-address-pools-in-VMM.md)
[How to create a logical network and IP address pools in VMM](./How-to-create-a-logical-network-and-IP-address-pools-in-VMM.md)
[Overview: plan logical networks, network sites, and IP address pools in VMM](./Overview--plan-logical-networks,-network-sites,-and-IP-address-pools-in-VMM.md)
[Modifying logical networks and VM networks in VMM](./Modifying-logical-networks-and-VM-networks-in-VMM.md)
[Configuring logical networks, VM networks, and logical switches in VMM](./Configuring-logical-networks,-VM-networks,-and-logical-switches-in-VMM.md)
[Managing network resources with VMM](./Managing-network-resources-with-VMM.md)


