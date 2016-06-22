---
title: How to view and modify properties of a deployed virtual machine in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 65cfeb42-4516-42c9-8d33-1717e6cfc9a2
---
# How to view and modify properties of a deployed virtual machine in VMM
After a virtual machine has been deployed in Virtual Machine Manager \(VMM\), you can view the properties of the virtual machine. You can modify some of the properties that you view in the properties dialog box. However, for some properties, the state of the virtual machine must be off to allow modifications.

The IP addresses displayed in virtual machine properties include all addresses on a vNIC, not just the addresses that are in an IP pool.

### To view and to modify properties of a deployed virtual machine in VMM

1.  Open the **VMs and Services** workspace.

2.  Expand **All Hosts**, expand the host group that the virtual machine is deployed on, and then select the host that the virtual machine is deployed on.

3.  Under **VMs**, right\-click the name of the virtual machine, and then click **Properties**.

4.  In the virtual machine’s properties dialog box, click on the various tabs to view the properties of the virtual machine.

    For example:

    -   To view IP addresses: Click the **Hardware Configuration** tab, click the network adapter, and in the results pane, click the **Connection details** button.

    -   To view processor and memory: Click the **Hardware Configuration** tab, and in the results pane, under **General**, click **Processor** or **Memory**. If you need to, you can modify the number of processors and the amount of memory that is allocated.

## See Also
[Creating and deploying virtual machines in VMM](Creating-and-deploying-virtual-machines-in-VMM.md)
[How to Create IP Address Pools for VM Networks in VMM](assetId:///ae6e919f-0308-4e2f-a8ad-8d97ccba77dc)


