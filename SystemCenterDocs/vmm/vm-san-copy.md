---
ms.assetid: 63e75b37-0bba-44d1-a8d9-dc1d8273ff48
title: Deploy VMs with rapid provisioning using SAN copy in the VMM fabric
description: This article describes how to rapidly provision VMs in the VMM fabric using SAN copy
author: jyothisuri
ms.author: jsuri
ms.date: 04/02/2025
ms.topic: article
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: intro-deployment, engagement-fy23, UpdateFrequency2, engagement-fy24
---


# Deploy VMs with rapid provisioning using SAN copy in the VMM fabric

This article describes how to rapidly provision VMs in the System Center Virtual Machine Manager (VMM) fabric using SAN copy.

Rapid provisioning provides a method for deploying new virtual machines to storage arrays without needing to copy VMs over the network. VMM uses the SAN infrastructure for cloning VMs, with a VM template to customize the guest operating system.

- You can use rapid provisioning to deploy standalone VMs and VMs that are deployed as part of a service.
- You create a SAN copy-capable template from a Virtual Hard Disk (VHD) that resides on a storage logical unit that supports SAN copy through cloning or snapshots.
- When you create a VM using the SAN copy-capable template, VMM quickly creates a read-write copy of the logical unit that contains the VHD and places the virtual machine files on the new logical unit.<br>
When VMM deploys a virtual machine using rapid provisioning through SAN copy, VMM uses a SAN transfer instead of a network transfer. During a SAN transfer, a SAN copy of the logical unit that contains the virtual machine is created and is assigned to the destination host or host cluster. Because the files for a virtual machine aren't moved over the network when you transfer a virtual machine over a SAN, it's much faster than a transfer over a standard network.
- You can use either of the following methods to create a SAN copy-capable template:
    - Create a SAN-copy capable template from a new VM.
    - Create a SAN-copy capable template from an existing VM.


## Before you start

Here are some considerations before you start deploying VMs:

- Any storage that is accessible by the provisioned computer can be partitioned during the provisioning process even if a specific disk is selected to be used as the operating system disk. In this case, data will be lost. To guarantee the use of a specific boot volume, use deep discovery and don't restart the computer before the deployment of the operating system completes.
- The storage array must support the new storage management features in VMM.
- The storage array must support cloning or snapshots, and the cloning or snapshots feature must be enabled. This might require additional licensing from your storage vendor.
- The storage pool that you want to use for rapid provisioning must be under VMM management. To meet this requirement, you must add the Storage Management Initiative Specification (SMI-S) provider for the array, discover storage pools, classify the storage, and set the preferred allocation method for the storage array to either snapshot or cloning.
- The storage pool that you want to use for rapid provisioning must be allocated to the host group where you want to use rapid provisioning of virtual machines.
- The Hyper-V hosts that you want to use as placement destinations must be members of the host group. Additionally, the following prerequisites must be met:
    - If you want to create a SAN-copy capable template from a new virtual machine, the host where you create the virtual machine must also be a member of this host group.

    - If you want to create a SAN-copy capable template from an existing virtual machine, and want to create and assign the logical unit from the library server, the library server must be a member of this host group. Therefore, the library server must be a Hyper-V host. (If you don't want to add the library server as a host, you can assign the logical unit out-of-band using your storage array vendor’s management tools.)
    :::moniker range="<=sc-vmm-2019"
    - If you want to use rapid provisioning to deploy Generation 2 VMs, you must choose a host with an operating system that supports them.
    :::moniker-end    
    - All Hyper-V hosts that you want to use for rapid provisioning and the library server must have access to the storage array. Also, they must use the same type of SAN connectivity. For SAN migrations to succeed, you can't have some hosts that connect to the array through Fibre Channel and others that connect through iSCSI. Configuration varies, depending on your storage hardware.

- You must get specific configuration information from the storage vendor, but configuration typically requires:

    - The Multipath I/O (MPIO) feature must be added on each host that will access the Fibre Channel or iSCSI storage array. You can add the MPIO feature through Server Manager.
    - If the MPIO feature is already enabled before you add a host to VMM management, VMM will automatically enable MPIO for supported storage arrays using the Microsoft provided Device Specific Module (DSM). If you already installed vendor-specific DSMs for supported storage arrays and then add the host to VMM management, the vendor-specific MPIO settings will be used to communicate with those arrays.
    - If you add a host to VMM before you add the MPIO feature, you must manually configure MPIO to add the discovered device hardware IDs. Alternatively, you can install vendor-specific DSMs.
    - If you're using a Fibre Channel Storage Area Network (SAN), each host that will access the storage array must have a Host Bus Adapter (HBA) installed. Additionally, ensure that the hosts are zoned accordingly so that they can access the storage array.
    - If you use an iSCSI SAN, ensure that iSCSI portals have been added and that the iSCSI initiator is logged into the array. Additionally, ensure that the Microsoft iSCSI Initiator Service on each host is started and set to Automatic. For information on how to create an iSCSI session on a host through VMM, see [How to configure Storage on a Hyper-V Host in VMM](hyper-v-storage.md#configure-storage-for-a-hyper-v-cluster).


## Create a SAN copy-capable template from a new virtual machine

Create a new VM on a logical unit assigned to a Hyper-V host. On the library server, create a SAN-copy capable template from the VM. 

>[!NOTE]
>- The library server doesn't need to be a managed Hyper-V host, but it must be able to access the storage pool in which the logical unit resides.
>- When you create the template, the logical unit is automatically unregistered from the host and registered to the library server.

1. Create a logical unit in the VMM storage fabric from the managed storage pool you want to use for rapid provisioning. Alternatively, you can create and assign the logical unit in your storage array management tool.
2. Allocate the logical unit to the host group where the target host resides. Then assign to logical unit to the host. When you assign the LUN, you can format it and assign a drive letter. Ensure that the logical unit you want to assign must be empty.
3.  Create a virtual machine with a blank virtual hard disk file on the logical unit.

    - In **Select Source**,  select **Create the new virtual machine with a blank virtual hard disk**.
    - In **Configure Hardware**, configure the required settings. Ensure that **Create a new virtual hard disk** is selected.
    - In **Select Destination**, accept the default setting to **Place the virtual machine on a host**.
    - In **Configure Settings**, in **Select Destination Folder**, select the drive that you created from the assigned logical unit. Verify that **SAN (Migration Capable)** appears next to the drive information. For example: **(L:\) [9.92 GB free of 10.00 GB, SAN (Migration Capable)]**.
    - In **Machine Resources**, select **Virtual Hard Disk**. In **Browse** > **Select Destination Folder**, select the drive you created from the assigned logical unit.
    - In **Select Network** and **Add Properties**, select the required settings. In **Summary**, review the settings and select **Create**. Verify that the VM is listed in **VMs and Services** > **All Hosts** > **VMs**.

4.  On the new VM, install and customize the guest operating system and the applications that you want. Generalize the image using Sysprep.exe with the **/generalize** and the **/oobe** options to generalize the associated virtual hard disk. [Learn more](/previous-versions/windows/it-pro/windows-8.1-and-8/hh825033(v=win.10)). When you're finished, ensure there are no .iso image files attached to the virtual DVD drive.

## Create a SAN copy-capable template from an existing VM

Create a template from an existing VM.

- If you want to perform this procedure in VMM, the library server must be added as a managed Hyper-V host. This enables you to assign the logical unit to the library server through VMM. If you don't want to make the library a managed Hyper-V host, you can use your array vendor’s management tools to assign the logical unit to the library server.
- You must have an existing virtual hard disk (that was generalized using Sysprep) that you want to use as a base image for rapid provisioning.
- Create a folder in the library share that you'll use to mount the logical unit to and to store the virtual hard disk. For example, create a folder in the SEALibrary library share that is named Rapid Provision VHD.

To create a template from an existing VM, follow these steps:

1. Create a logical unit in the VMM storage fabric from the managed storage pool you want to use for rapid provisioning.
2. Format the logical unit and mount it to the folder path you created.
3. Assign the logical unit to the library server. If the library server is a managed Hyper-V host, you can create and assign the logical unit from the library server. You can also format the disk with NTFS and mount the logical unit to the folder path in the library share at the same time.
    - When you create the logical unit, select the option **Mount in the following empty NTFS folder** > **Browse**, and then select the folder that you created.
    - Don't assign a drive letter. Also, don't ever create multiple mount points to the folder.

4. If the library server isn't a managed Hyper-V host, use your array vendor’s management tools to create the logical unit and to unmask the logical unit to the library server. Then, do the following:
    - Don't assign a drive letter.
    - Use Disk Management (diskmgmt.msc) to rescan the disk, initialize the disk, and format it.
    - In Disk Management, mount the logical unit to the folder path you created in the library share (**Change Drive Letter and Paths** > **Add** > **Mount in the following empty NTFS folder**, and select the empty library folder).
5. Copy the virtual hard disk you want to use to the new folder in the library share.

    > [!NOTE]
    > The virtual hard disk must be the only file on the logical unit.

6. The new folder that you created appears in the library share. To verify the virtual hard disk SAN copy-capable, select the new folder, and in **Physical Library Objects**, select the VHD file. **SAN copy capable** must indicate **Yes**.


## Create a SAN-copy capable template

To create a SAN-copy capable template, follow these steps:

1. Select **Library** > **Create** > **Create VM Template**.
2. In **Create VM Template Wizard** > **Select Source**, select **From an existing virtual machine that is deployed on a host** > **Browse**. Select the VM on the logical unit. Select **Yes** on the warning message.
3. In **Identity**, enter a template name and description.
4. In **Configure Hardware**, select **Next**. The classification that appears matches what you assigned to the storage pool from which you created the logical unit.
5. In **Configure Operating System**, select **Next**.
6. In **Select Library Server**, select the library server where you want to create the template. Verify that the **Transfer Type** is **SAN** and select **Next**. The library server must have access to the same storage pool as the host.
7. In **Select Path**, select **Browse**, and select a location on the library server to store the VM files.
8. In **Summary**, review the settings and select **Create**. In **Jobs**, you can track the template being created. Wait for the **Completed** status. Verify the template in **Library** > **Templates** > **VM Templates**.


## Deploy a VM from the template

Now deploy a VM from the SAN-copy capable template. This procedure explains how to deploy a standalone VM. Alternatively, you can select the template when you [create a service](library-resources.md). Ensure that:

- The hosts where you want to place the VMs must have access to the managed storage pool where the logical unit that is associated with the template resides.
- If you want to deploy the virtual machines to a private cloud, the storage classification that is assigned to the logical unit that was used to create the SAN clone-capable template must be available to the private cloud.
- For cloud deployment, the host groups that are used to provide resources for the private cloud must contain the hosts that have access to the managed storage pool where the logical unit that is associated with the template resides.

To deploy a VM from the template, follow these steps:

1. Select **VMs and Services** > **Create** > **Create Virtual Machine**.
2. In the Create Virtual Machine Wizard  > **Select Source**, select **Use an existing virtual machine, VM template or virtual hard disk** > **Browse**. Select type **VM Template**, and select the template you created for rapid provisioning. The template must indicate **Yes** in the **SAN Copy Capable** column.
3. In **Select Source**, select **Next**.
4. Complete the rest of the steps  wizard to create and deploy the virtual machine.

    >[!NOTE]
    > - In **Configure Hardware** > **Bus Configuration**, leave the **Classification** list empty or select the storage classification that 
    > - In **Select Host** or **Select Cloud**, ensure the **Transfer Type** column indicates **SAN**.
    > - If you selected to place the virtual machine on a host, in **Configure Settings** > **Machine Resources**, select the virtual hard disk to verify the deployment options. For rapid provisioning through SAN copy, ensure that the method to deploy the virtual hard disk to the host list is **Transfer the virtual disk by using the SAN**.

5. After you complete the wizard, open **Jobs** > **Create virtual machine job** to view the job status.
6. When you create a virtual machine from the SAN copy-capable template, a new logical unit is automatically provisioned from the same storage pool where the virtual hard disk that was used to create the SAN copy-capable template from resides. The logical unit is automatically registered and mounted on the target host.
7. To verify that the virtual machine was created, open the VMs and Services workspace. Expand **All Hosts** or **Clouds** and locate and select the destination host or private cloud. In **VMs**, verify that the new virtual machine appears. If you open Disk Management (Diskmgmt.msc) on the destination host, you can see the new disk that is assigned and registered to the host.

## Next steps

[Manage the VM settings](vm-settings.md).
