---
title: How to configure preferred and possible owners for a virtual machine on a host cluster
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b3395d9f-b75c-4b97-9a33-299dd2a84677
---
# How to configure preferred and possible owners for a virtual machine on a host cluster
If you deploy virtual machines on a host cluster, you can use [!INCLUDE[vmm12sp1_long](../../Token/vmm12sp1_long_md.md)] to configure preferred owners and possible owners for the virtual machines. By default, there are no preferred owners \(there is no preference\), and the possible owners include all nodes \(servers\) in the host cluster.

For information about other settings related to availability of virtual machines on a host cluster, see [Configuring availability options for virtual machines in VMM](Configuring-availability-options-for-virtual-machines-in-VMM.md).

**Account requirements** To complete this procedure you must be a member of the Administrator or Delegated Administrator user role, or a self\-service user who has the **Deploy** action in the scope of their user role.

### To configure preferred and possible owners for a virtual machine

1.  In the **VMs and Services** workspace, navigate to the host on which the virtual machine is deployed. In the results pane, right\-click the virtual machine, and then click **Properties**.

2.  Click the **Settings** tab and configure the options:

    -   To control which nodes \(servers\) in the cluster will own the virtual machine most of the time, configure the preferred owners list.

    -   To prevent a virtual machine from being owned by a particular node, configure the possible owners list, omitting only the nodes that should never own the virtual machine.

3.  In the properties sheet, click **OK**.

4.  To verify the settings, reopen the properties sheet.

## See Also
[Overview: creating and deploying virtual machines in VMM](Overview--creating-and-deploying-virtual-machines-in-VMM.md)
[Configuring availability options for virtual machines in VMM](Configuring-availability-options-for-virtual-machines-in-VMM.md)
[Configuring virtual machine options and settings](Configuring-virtual-machine-options-and-settings.md)
[Managing virtual machines with VMM](Managing-virtual-machines-with-VMM.md)
[Managing tenant resources with VMM](Managing-tenant-resources-with-VMM.md)


