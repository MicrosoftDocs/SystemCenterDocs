---
title: How to configure priority in VMM for a virtual machine on a host cluster
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a5fa6cd1-8249-4d87-b2c1-d14aa003176b
---
# How to configure priority in VMM for a virtual machine on a host cluster
If you deploy or are planning to deploy virtual machines on a host cluster, you can use [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)] to configure priority settings for the virtual machines. With these settings, the cluster starts or places high\-priority virtual machines before medium\-priority or low\-priority virtual machines. This ensures that the high\-priority virtual machines are allocated memory and other resources first, for better performance. Also, after a node failure, if the high\-priority virtual machines do not have the necessary memory and other resources to start, the lower priority virtual machines will be taken offline to free up the necessary resources for the high\-priority machines. Virtual machines that are preempted are later restarted in priority order.

You can also configure the virtual machine priority setting in a virtual machine template, so that any virtual machines that are created with that template will have the specified virtual machine priority. For virtual machines that have been deployed on a host cluster, you can also configure these settings by using Failover Cluster Manager.

For information about other settings related to availability of virtual machines on a host cluster, see [Configuring availability options for virtual machines in VMM](../Topic/Configuring-availability-options-for-virtual-machines-in-VMM.md).

**Account requirements** To complete this procedure you must be a member of the Administrator or Delegated Administrator user role, or a self\-service user who has the **Deploy** action in the scope of your user role.

### To configure priority for a virtual machine on a host cluster or in a virtual machine template designed for deployment on a host cluster

1.  Configure a virtual machine or virtual machine template by using one of the following options:

    1.  To configure a deployed virtual machine, in the **VMs and Services** workspace, navigate to the host on which the virtual machine is deployed. In the results pane, right\-click the virtual machine, and then click **Properties**.

    2.  To configure a stored virtual machine, in the **Library** workspace, navigate to the library server on which the virtual machine is stored. In the results pane, right\-click the virtual machine, and then click **Properties**.

    3.  To configure a virtual machine while you are creating it, follow an appropriate procedure under [Creating and deploying virtual machines in VMM](../Topic/Creating-and-deploying-virtual-machines-in-VMM.md) to open the **Create Virtual Machine Wizard** and to proceed to the **Configure Hardware** page.

    4.  To configure a virtual machine template, in the **Library** workspace, under **Templates**, click **VM Templates**. In the results pane, right\-click the virtual machine template, and then click **Properties**.

2.  On the **Hardware Configuration** tab or \(for the wizard\) the **Configure Hardware** page, scroll down to **Advanced** and under it, click **Availability**.

3.  Confirm that **Make this virtual machine highly available** is checked. \(On a deployed virtual machine, this setting cannot be changed, because it depends on whether the virtual machine is deployed on a host cluster.\)

4.  Under **Virtual machine priority**, select a priority of **High**, **Medium**, or **Low** for the virtual machine. If you want the virtual machine to always require a manual start and never pre\-empt other virtual machines, select **Do not restart automatically**.

5.  Click **OK** or complete the wizard.

6.  To verify the setting, reopen the properties sheet.

## See Also
[How to create and deploy a virtual machine from a blank virtual hard disk](../Topic/How-to-create-and-deploy-a-virtual-machine-from-a-blank-virtual-hard-disk.md)
[How to create and deploy a virtual machine from an existing virtual hard disk](../Topic/How-to-create-and-deploy-a-virtual-machine-from-an-existing-virtual-hard-disk.md)
[How to create a virtual machine template](../Topic/How-to-create-a-virtual-machine-template.md)
[How to create and deploy a virtual machine from a template](../Topic/How-to-create-and-deploy-a-virtual-machine-from-a-template.md)
[Configuring availability options for virtual machines in VMM](../Topic/Configuring-availability-options-for-virtual-machines-in-VMM.md)
[Configuring virtual machine options and settings](../Topic/Configuring-virtual-machine-options-and-settings.md)
[Managing virtual machines with VMM](../Topic/Managing-virtual-machines-with-VMM.md)
[Managing tenant resources with VMM](../Topic/Managing-tenant-resources-with-VMM.md)

