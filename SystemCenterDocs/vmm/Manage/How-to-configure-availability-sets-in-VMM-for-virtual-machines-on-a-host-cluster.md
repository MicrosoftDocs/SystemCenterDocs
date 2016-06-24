---
title: How to configure availability sets in VMM for virtual machines on a host cluster
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4ed5fceb-d013-4376-a8ae-694c659f3e07
---
# How to configure availability sets in VMM for virtual machines on a host cluster
If you deploy virtual machines on a host cluster, you can use Virtual Machine Manager (VMM) to configure availability sets for the virtual machines. When you place virtual machines in an availability set, VMM will attempt to keep those virtual machines on separate hosts and avoid placing them together on the same host whenever possible. This helps to improve continuity of service.

You can also configure availability sets in a service template, to specify how virtual machines that are created with that template should be placed on hosts. 

For virtual machines that have been deployed on a host cluster, another way to configure this setting is to use Windows PowerShell commands for failover clustering. In this context, the setting appears in the [Get-ClusterGroup](http://technet.microsoft.com/library/hh847242.aspx) listing and is called **AntiAffinityClassNames**.

For information about other settings related to availability of virtual machines on a host cluster, see [Configuring availability options for virtual machines in VMM](Configuring-availability-options-for-virtual-machines-in-VMM.md).

**Account requirements** To complete this procedure you must be a member of the Administrator or Delegated Administrator user role, or a self-service user who has the **Deploy** action in the scope of your user role.

### To configure availability sets for a virtual machine on a host cluster

1.  Open the properties sheet of the virtual machine by using one of the following actions:

    1.  To configure a deployed virtual machine, in the **VMs and Services** workspace, navigate to the host on which the virtual machine is deployed. In the results pane, right-click the virtual machine, and then click **Properties**.

    2.  To configure a stored virtual machine, in the **Library** workspace, navigate to the library server on which the virtual machine is stored. In the results pane, right-click the virtual machine, and then click **Properties**.

2.  On the **Hardware Configuration** tab, scroll down to **Advanced** and under it, click **Availability**.

3.  Confirm that **Make this virtual machine highly available** has the intended setting. (On a deployed virtual machine, the setting cannot be changed, because it depends on whether the virtual machine is deployed on a host cluster.)

4.  Under **Availability sets**, click **Manage availability sets**.

5.  Click the name of an availability set, and use the controls to add or remove the set. Repeat this action until all of the intended availability sets appear in the **Assigned properties** list. To create a new availability set, click the **Create** button, provide a name for the set, and then click **OK**.

6.  In the **Manage Availability Sets** dialog box, click **OK**.

7.  In the properties sheet, click **OK**.

8.  To verify the setting for a deployed virtual machine, in the listing for the virtual machine, view the name under **Availability Set Name**.




