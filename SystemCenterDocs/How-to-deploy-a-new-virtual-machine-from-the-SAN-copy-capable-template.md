---
title: How to deploy a new virtual machine from the SAN copy-capable template
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bf217c19-f448-46bb-8e5d-9b4604af236b
---
# How to deploy a new virtual machine from the SAN copy-capable template
You can use this procedure to deploy a virtual machine from a SAN copy\-capable template that you created for rapid provisioning in [!INCLUDE[vmm12sp1_long](Token/vmm12sp1_long_md.md)]. You can use the SAN copy\-capable template to deploy stand\-alone virtual machines, and to deploy virtual machines as part of a service. This procedure shows how to deploy a new stand\-alone virtual machine by using rapid provisioning. If you want to use the template during service creation, you can select an existing SAN clone\-capable virtual machine template when you create a service.

> [!IMPORTANT]
> The hosts where you want to place the virtual machines must have access to the managed storage pool where the logical unit that is associated with the template resides. If you want to deploy the virtual machines to a private cloud, the storage classification that is assigned to the logical unit that was used to create the SAN clone\-capable template must be available to the private cloud. Additionally, the host groups that are used to provide resources for the private cloud must contain the hosts that have access to the managed storage pool where the logical unit that is associated with the template resides.

### To deploy a virtual machine through rapid provisioning

1.  Open the **VMs and Services** workspace.

2.  On the **Home** tab, in the **Create** group, click the **Create Virtual Machine** drop\-down arrow, and then click **Create Virtual Machine**.

    The Create Virtual Machine Wizard opens.

3.  On the **Select Source** page, make sure that **Use an existing virtual machine, VM template or virtual hard disk** is selected, and then click **Browse**.

4.  In the **Select Virtual Machine Source** dialog box, under **Type: VM Template**, click the template that you created for rapid provisioning, and then click **OK**.

    > [!IMPORTANT]
    > Make sure that there is a value of **Yes** for the template in the **SAN Copy Capable** column.

5.  On the **Select Source** page, click **Next**.

6.  Complete the rest of the steps in the New Virtual Machine wizard to create and deploy the virtual machine. Note the following:

    -   On the **Configure Hardware** page, under **Bus Configuration**, leave the **Classification** list empty, or select the storage classification that matches the classification of the logical unit where the SAN copy capable virtual hard disk resides.

    -   On the **Select Host** page or the **Select Cloud** page, make sure that the **Transfer Type** column for the host or private cloud that you select indicates **SAN**.

    -   If you selected to place the virtual machine on a host, on the **Configure Settings** page, under **Machine Resources**, click the virtual hard disk to verify the deployment options. For rapid provisioning through SAN copy, make sure that the value in the **Method to deploy the virtual hard disk to the host** list is **Transfer the virtual disk by using the SAN**.

7.  After you complete the wizard, open the **Jobs** workspace to view the job status. To view job details, click the **Create virtual machine** job.

    When you create a virtual machine from the SAN copy\-capable template, a new logical unit is automatically provisioned from the same storage pool where the virtual hard disk that was used to create the SAN copy\-capable template from resides. The logical unit is automatically registered and mounted on the target host.

8.  To verify that the virtual machine was created, open the **VMs and Services** workspace. Expand **All Hosts** or **Clouds**, depending on where you deployed the virtual machine, and then locate and click the destination host or private cloud. In the **VMs** pane, verify that the new virtual machine appears. If you open Disk Management \(Diskmgmt.msc\) on the destination host, you can see the new disk that is assigned and registered to the host.

## See Also
[Using SAN copy to rapidly provision virtual machines](Using-SAN-copy-to-rapidly-provision-virtual-machines.md)
[Managing virtual machines with VMM](Managing-virtual-machines-with-VMM.md)
[Managing tenant resources with VMM](Managing-tenant-resources-with-VMM.md)


