---
title: How to create a SAN copy-capable template from an existing virtual machine
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fd02e62b-86f9-4282-a857-453c0641a2a9
---
# How to create a SAN copy-capable template from an existing virtual machine
You can use the procedures in this topic to create a SAN copy\-capable template from an existing virtual machine in [!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)]. In these procedures, you create and assign a logical unit to the library server, mount the logical unit to a folder in the library share, copy an existing virtual hard disk to the folder in the library share, and then create a SAN\-copy capable template by using the virtual hard disk file as the template source.

## Prerequisites
Before you begin these procedures, make sure that the following prerequisites are met:

-   Your configuration must meet all the prerequisites that are defined in the [Prerequisites for rapid provisioning using SAN copy](./Using-SAN-copy-to-rapidly-provision-virtual-machines.md#BKMK_prereq) section of "Rapid Provisioning of Virtual Machines Using SAN Copy Overview."

-   If you want to perform this procedure entirely within [!INCLUDE[vmm12short](./Token/vmm12short_md.md)], you must add the library server as a managed Hyper\-V host. This enables you to assign the logical unit to the library server through [!INCLUDE[vmm12short](./Token/vmm12short_md.md)]. If you do not want to make the library a managed Hyper\-V host, you can use your array vendor’s management tools to assign the logical unit to the library server.

-   You must have an existing virtual hard disk \(that was generalized by using Sysprep\) that you want to use as a base image for rapid provisioning.

-   Create a folder in the library share that you will use to mount the logical unit to, and to store the virtual hard disk.

    For example, create a folder in the **SEALibrary** library share that is named **Rapid Provision VHD**.

#### To create a SAN\-copy capable virtual hard disk

1.  Create a logical unit from a storage pool that is managed by [!INCLUDE[vmm12short](./Token/vmm12short_md.md)], assign it to the library server, format the logical unit, and mount the logical unit to the folder path that you created in the Prerequisites section of this topic.

    If the library server is a managed Hyper\-V host, you can create and assign the logical unit from the library server. You can also format the disk with NTFS and mount the logical unit to the folder path in the library share at the same time. For information about how to create and assign a logical unit to a host through [!INCLUDE[vmm12short](./Token/vmm12short_md.md)], see [How to configure storage on a Hyper-V host in VMM](./How-to-configure-storage-on-a-Hyper-V-host-in-VMM.md).

    > [!IMPORTANT]
    > When you create the logical unit, choose the option **Mount in the following empty NTFS folder**, click **Browse**, and then click the folder that you created in the Prerequisites section. Do not assign a drive letter. Also, do not ever create multiple mount points to the folder.

    If the library server is not a managed Hyper\-V host, use your array vendor’s management tools to create the logical unit, and to unmask the logical unit to the library server. Then, mount the logical unit to the folder path in the library share that you created in the Prerequisites section of this topic. To do this, follow these steps:

    1.  Open Disk Management. To do this, click **Start**, type **diskmgmt.msc** in the search box, and then press ENTER.

    2.  Rescan the disks, initialize the disk, and then format the disk. To rescan the disks, on the **Action** menu, click **Rescan Disks**. To initialize the disk, right\-click the disk, and then click **Initialize Disk**.

        > [!IMPORTANT]
        > Do not assign a drive letter to the disk.

    3.  Mount the partition using a folder path in the library share. To do this, right\-click the disk, and then click **Change Drive Letter and Paths**. Click **Add**, and then click **Mount in the following empty NTFS folder**. Click **Browse**, locate and then click the empty library folder that you created in the Prerequisites section of this topic, and then click **OK**.

        > [!IMPORTANT]
        > Do not ever create multiple mount points to the folder.

        For example, mount the partition to the **Rapid Provision VHD** folder that you created in the SEALibrary library share.

    4.  Close Disk Management.

2.  Copy the virtual hard disk that you want to use to the new folder in the library share.

    > [!IMPORTANT]
    > The logical unit that you use must not contain any data. The virtual hard disk that you copy to the logical unit in this procedure must be the only file on the logical unit.

3.  In the VMM console, open the **Library** workspace, and then refresh the library share.

    The new folder that you created appears in the library share. To verify that the virtual hard disk is SAN copy\-capable, click the new folder, and then in the **Physical Library Objects** pane, click the virtual hard disk file. In the details pane for the virtual hard disk file, make sure that the **SAN copy capable** field indicates a value of **Yes**.

#### To create a SAN copy\-capable template

1.  Open the **Library** workspace.

2.  In the **Library** pane, expand **Library Servers**, expand the library share where you mounted the folder, and then click the SAN copy capable virtual hard disk that you created in the previous procedure.

3.  On the **Home** tab, in the **Create** group, click **Create VM Template**.

    The Create VM Template Wizard opens.

4.  On the **VM Template Identity** page, in the **VM Template name** box, enter a name for the template and an optional description, and then click **Next**.

    For example, enter the name **WS12 Rapid Provision**.

5.  Complete the rest of the New VM Template Wizard. Note the following:

    -   On the **Configure Hardware** page, specify the storage classification. Make sure that the field is empty, or that you select the classification that was assigned to the logical unit that you created. \(To do this, under **Bus Configuration**, click the virtual hard disk. In the **Classification** list, specify the storage classification.\)

    -   Realize that if you plan to use the template for the rapid\-provisioning of stand\-alone virtual machines, any settings that you enter in the **Configure Applications** and the **Configure SQL Server** pages of the wizard are ignored. These settings are only used for virtual machines that are deployed as part of a service.

    After you complete the wizard, open the **Jobs** workspace to view the job status. Verify that the job to create the template has a status of **Completed**.

6.  To verify that the template was created, in the **Library** workspace, in the **Library** pane, expand **Templates**, and then click **VM Templates**.

    In the **Templates** pane, verify that the new template is listed.

    > [!TIP]
    > To add the SAN Copy Capable column to the Templates pane, right\-click the column header, and then click **SAN Copy Capable**.

## See Also
[Using SAN copy to rapidly provision virtual machines](./Using-SAN-copy-to-rapidly-provision-virtual-machines.md)
[How to deploy a new virtual machine from the SAN copy-capable template](./How-to-deploy-a-new-virtual-machine-from-the-SAN-copy-capable-template.md)
[Managing virtual machines with VMM](./Managing-virtual-machines-with-VMM.md)
[Managing tenant resources with VMM](./Managing-tenant-resources-with-VMM.md)


