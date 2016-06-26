---
title: How to create a SAN copy-capable template from a new virtual machine
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 31a0cf55-1141-4db6-9e78-ec51b1279259
---
# How to create a SAN copy-capable template from a new virtual machine
You can use the procedures in this topic to create a SAN copy-capable template from a new virtual machine in Virtual Machine Manager (VMM). In these procedures, you create a new virtual machine on a logical unit that is assigned to a Hyper-V host, and then create a SAN-copy capable template from the virtual machine on the library server. When you create the template, the logical unit is automatically unregistered from the host and registered to the library server.

## Prerequisites
Before you begin these procedures, make sure that the following prerequisites are met:

-   Your configuration must meet all the prerequisites that are defined in the [Prerequisites for rapid provisioning using SAN copy](Using-SAN-copy-to-rapidly-provision-virtual-machines.md#BKMK_prereq) section of "Rapid Provisioning of Virtual Machines Using SAN Copy Overview." Note that the library server does not have to be a managed Hyper-V host. However, it must have access to the storage pool where the logical unit that you use for rapid provisioning resides.

-   You must create a logical unit from the managed storage pool that you want to use for rapid provisioning, and assign it to the host where you want to create the new virtual machine. You must also format the logical unit with NTFS, and assign a drive letter. You can use any of the following methods:

    -   Create and assign the logical unit through the VMM console from the Storage tab in the managed Hyper-V host’s properties. When you assign the logical unit, you can format and assign a drive letter to the logical unit at the same time. For information about how to create and assign a logical unit to a host through VMM, see [How to configure storage on a Hyper-V host in VMM](How-to-configure-storage-on-a-Hyper-V-host-in-VMM.md).

    -   Create a logical unit from the Storage node in the Fabric workspace. Then, allocate the logical unit to a host group, and assign the logical unit to the host from the managed Hyper-V host. When you assign the logical unit, you can format and assign a drive letter to the logical unit at the same time. For information about how to create a logical unit from the Storage node, see [How to provision storage logical units in VMM](How-to-provision-storage-logical-units-in-VMM.md).

    -   Use your storage array vendor’s management tools to create and assign the logical unit. You can use Disk Management (Diskmgmt.msc) to format the logical unit and assign a drive letter after the logical unit is assigned to the host.

    > [!NOTE]
    > In the example scenario, drive L: is used to represent the drive letter that is assigned to the logical unit.

-   The logical unit that you want to use for the new virtual machine must be empty.

#### To create a SAN copy-capable virtual hard disk on a host

1.  Open the **VMs and Services** workspace.

2.  On the **Home** tab, in the **Create** group, click the **Create Virtual Machine** drop-down arrow, and then click **Create Virtual Machine**.

    The Create Virtual Machine Wizard opens.

3.  On the **Select Source** page, click **Create the new virtual machine with a blank virtual hard disk**, and then click **Next**.

4.  On the **Identity** page, enter the virtual machine name—for example, the name **Rapid Provision Base VM WS12**—and an optional description. In the **Generation** box, select **Generation 1** or **Generation 2**. (For more information, see [Understanding generation 1 and generation 2 virtual machines in VMM](Understanding-generation-1-and-generation-2-virtual-machines-in-VMM.md).) Then click **Next**.

5.  On the **Configure Hardware** page, configure the desired hardware settings for the virtual machine, and then click **Next**.

    > [!NOTE]
    > Make sure that the **Create a new virtual hard disk** option is selected.

6.  On the **Select Destination** page, accept the default setting of **Place the virtual machine on a host**, and then click **Next**.

7.  On the **Select Host** page, select the host where you assigned the logical unit that you want to use for rapid provisioning, and then click **Next**.

8.  On the **Configure Settings** page, do the following:

    1.  Under **Locations**, click **Virtual Machine Location**. In the results pane, under the **Virtual machine path** box, click **Browse**. In the **Select Destination Folder** dialog box, click the drive that you created from the assigned logical unit, and then click **OK**.

        > [!NOTE]
        > In the **Select Destination Folder** dialog box, verify that the text **SAN (Migration Capable)** appears next to the drive information.

        For example, click drive **(L:\\) [9.92 GB free of 10.00 GB, SAN (Migration Capable)]**.

    2.  Under **Machine Resources**, click **Virtual Hard Disk**. In the results pane, next to the **Destination path** box, click **Browse**. In the **Select Destination Folder** dialog box, click the same drive that you selected in step 8a (the drive that you created from the assigned logical unit), and then click **OK**.

        For example, click drive **L:\\**.

    3.  Click **Next** to continue.

9. On the **Select Networks** page, select the desired logical network, virtual network, and VLAN setting.

10. On the **Add Properties** page, configure the desired settings, and then click **Next**.

11. On the **Summary** page, review the settings, and then click **Create**.

    Open the **Jobs** workspace to view the job status. Verify that the job has a status of **Completed w/ Info**, and then close the dialog box.

12. In the **VMs and Services** workspace, under **All Hosts**, click the host where you placed the virtual machine. In the **VMs** pane, verify that the new virtual machine is listed.

13. On the new virtual machine, install and customize the guest operating system and any desired applications. Generalize the image by running Sysprep.exe.

    > [!NOTE]
    > When you are finished, make sure that there are no .iso image files attached to the virtual DVD drive.

#### To create a SAN copy-capable template

1.  Open the **Library** workspace.

2.  On the **Home** tab, in the **Create** group, click **Create VM Template**.

    The Create VM Template Wizard opens.

3.  On the **Select Source** page, click **From an existing virtual machine that is deployed on a host**, click **Browse**, click the virtual machine on the host that resides on the logical unit, and then click **OK**.

    For example, click a virtual machine name such as **Rapid Provision Base VM WS12**, and then click **OK**.

4.  On the **Select Source** page, click **Next**.

5.  Review the warning message, and then click **Yes** to continue.

6.  On the **VM Template Identity** page, enter a name for the template in the **VM Template name** box, enter an optional description, and then click **Next**.

    For example, enter a name such as **Rapid Provision Template WS12**, and then click **Next**.

7.  On the **Configure Hardware** page, click **Next**.

    > [!NOTE]
    > Notice that a storage classification appears in the **Classification** list for the virtual hard disk. The classification matches what you assigned to the storage pool from which you created the logical unit.

8.  On the **Configure Operating System** page, click **Next**.

9. On the **Select Library Server** page, click the library server where you want to create the template. Verify that the **Transfer Type** column for the selected library server indicates **SAN**, and then click **Next**.

    > [!IMPORTANT]
    > The library server must have access to the same storage pool as the host.

10. On the **Select Path** page, next to the **Virtual machine path** box, click **Browse**. In the **Select Destination Folder** dialog box, select a location on the library server to store the virtual machine files, click **OK**, and then click **Next**.

11. On the **Summary** page, click **Create**.

    Open the **Jobs** workspace to view the job status. Verify that the job has a status of **Completed**.

12. To verify that the template was created, in the **Library** workspace, in the **Library** pane, expand **Templates**, and then click **VM Templates**.

    In the **Templates** pane, verify that the new template is listed, with a status of **OK**.

    > [!TIP]
    > To add the SAN Copy Capable column to the Templates pane, right-click the column header, and then click **SAN Copy Capable**.

