---
title: How to release inactive IP addresses for VM networks in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2f172715-1a44-41a9-9560-f4a41b6c8dd1
---
# How to release inactive IP addresses for VM networks in VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

With Virtual Machine Manager (VMM) in System Center 2016 Technical Preview, you can use the following procedure to release inactive IP addresses that are in an IP address pool on a VM network. When you release an inactive address, VMM returns the address to the static IP address pool, and considers it available for reassignment. An IP address is considered inactive when either of the following conditions is true:

-   A host that was assigned a static IP address through the bare-metal deployment process is removed from VMM management. When you remove the host, any IP and MAC addresses that were statically assigned to virtual machines on the host are also marked as inactive.

-   A virtual machine goes into a missing state because it was removed outside VMM.

### To release inactive IP addresses for VM networks

1.  Open the **VMs and Services** workspace.

    > [!NOTE]
    > Because this IP address pool is for virtual machines, it is located in the **VMs and services** workspace, not in the **Fabric** workspace.

2.  In the **VMs and Services** pane, click **VM Networks**.

3.  On the **Home** tab, in the **Show** group, click **VM Networks**.

    The **VM Network** tab appears.

4.  Click the **VM Network** tab.

5.  In the **VM Networks and IP Pools** pane, expand the VM network.

6.  Right-click the desired IP address pool, and then click **Properties**.

7.  Click the **Inactive addresses** tab.

8.  Select the check box next to each inactive IP address that you want to release, or select the check box in the table header row to select all the addresses, and then click **Release**.

## See Also
[How to release inactive IP or MAC addresses in VMM](How-to-release-inactive-IP-or-MAC-addresses-in-VMM.md)
[How to create a VM network for network virtualization and add an IP address pool in VMM](How-to-create-a-VM-network-for-network-virtualization-and-add-an-IP-address-pool-in-VMM.md)
[Modifying logical networks and VM networks in VMM](Modifying-logical-networks-and-VM-networks-in-VMM.md)
[Configuring logical networks, VM networks, and logical switches in VMM](Configuring-logical-networks,-VM-networks,-and-logical-switches-in-VMM.md)
[Managing network resources with VMM](Managing-network-resources-with-VMM.md)



