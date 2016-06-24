---
title: Overview: creating and deploying virtual machines in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 75447cbf-5a90-49b7-a5ca-2a3b6a310cb4
---
# Overview: creating and deploying virtual machines in VMM
Virtual Machine Manager (VMM) provides a number of methods for creating and deploying virtual machines, and for applying standard configuration settings to those virtual machines. This section provides information about these methods, and about other concepts that are related to virtual machines.

## Methods for creating and deploying virtual machines

-   **Create and deploy a stand-alone virtual machine**—You can manually create a stand-alone virtual machine as follows:

    -   **Create and deploy a virtual machine from a blank virtual hard disk**—After creating the virtual machine using this method you can install an operating system from an .iso image, CD or DVD, or from a network boot if a Pre-Boot Execution Environment (PXE) server is available. 
    -   **Create and deploy a virtual machine from an existing virtual hard disk**—Using this method you can create a virtual machine from an existing virtual hard disk stored in the VMM library. We recommend that you use a virtual hard disk that has been generalized using Sysprep, otherwise the new virtual machine will have the same identity as the source machine. 

    -   **Create and deploy a virtual machine from an existing virtual machine**—Using this method, you can clone an existing virtual machine in the VMM library to create a new one. We recommend that you clone a virtual machine that has been generalized using Sysprep, so that the cloned virtual machines do not have the same identity. When you use this method to create a virtual machine, VMM automatically uses differencing disk if a base disk is detected on the host that the cloned virtual machine is being created on.

-   **Create and deploy a virtual machine using a virtual-to-virtual (V2V) conversion**—Use this method to copy an existing VMware virtual machine and create a Hyper-V virtual machine.

    You can also use the Microsoft Virtual Machine Converter (MVMC) for V2V conversions. For more information, see [Microsoft Virtual Machine Converter 3.0](http://technet.microsoft.com/library/dn873998.aspx).

-   **Create and deploy a virtual machine using a virtual machine template**—Use this method to create virtual machines with consistent configuration settings taken from a template. Virtual machine templates are preconfigured XML objects stored in the VMM library. Templates can be used to control and restrict the virtual machine configurations available for selection by self-service users. Templates have a number of properties associated with them, including a guest operating system profile, a hardware profile, and one or more VHDs which can be used to create a new virtual machine. To create virtual machine templates, you first create the required profiles, and then create templates based on those profiles. Templates can be created from an existing template, from a virtual hard disk stored in the library, or from an existing virtual machine deployed on a host.

    When you use this method to create and deploy a virtual machine, the usage of differencing disk is optimized, allowing for a more efficient process.

 -   **Create and deploy virtual machines in a service deployment**—With VMM, you can create services, which are logical groupings of virtual machines that are configured and deployed together, and managed as a single entity. Services can be single-tier or multi-tier. A single-tier service consists of a single virtual machine that provides additional configuration settings to those provided by a virtual machine template. A multi-tiered service contains multiple virtual machines. For example, a multi-tier service might consist of a SQL server tier and a Web App tier. You define a service by configuring a service template, which includes information about virtual machines that are deployed in the service. You can create a new service template, or create a service template based on an existing virtual machine template.

    When you use this method to create and deploy a virtual machine, the usage of differencing disk is optimized, allowing for a more efficient process.



-   **Rapid provisioning of virtual machines** In VMM, you can rapidly provision virtual machines by using storage area network (SAN) copy technology such as snapshot and clone. Rapid provisioning is available for stand-alone virtual machines and for virtual machines that are deployed as a service. 

## Using differencing disks for creating and deploying virtual machines
You can use differencing disks when you create virtual machines using a virtual machine template, or when you use a service. Differencing disks are associated with a base virtual hard disk that does not change. This base disk works with differencing disks that contain any modifications to the base disk. This allows you to isolate the changes to the base disk, and to optimize several operations in VMM that are related to virtual machines. Using a small set of initial virtual disks, you can use differencing disks so that a large percentage of the disk data is shared among multiple virtual disks.

VMM optimizes support for differencing disks to provide the following benefits:

-   Optimized migration of storage that utilizes differencing disks. During a migration, VMM does not migrate base disks unless it is necessary.

-   Optimize virtual machine deployment time by utilizing differencing disks. VMM will attempt to identify and utilize differencing disks on the target computer.

-   When differencing disks is utilized, deployment of the base virtual disk is optimized by taking advantage of the Windows Offloaded Data Transfers (ODX) capability to copy files to the guest machine during service deployment.

-   Optimize time and storage of cloning of virtual machines by utilizing differencing disks. VMM provides the option to create and utilize differencing disks during a cloning operation.

When using differencing disks, administrators should pay attention to the following:

-   Ensure that unused base virtual disks on hosts are removed.

-   If a base virtual disk becomes corrupted, or unavailable for any other reason, all virtual disks that depend on the lost disk are lost too. As with any critical data, to mitigate that risk, you should follow a backup plan that will ensure the high availability of the base virtual disks.

## Fast file copy
During virtual machine deployment, VMM needs to move and copy large files, such as VHD’s, between two locations. Fast file copy improves the performance of file transfers, mostly by leveraging the Windows Offloaded Data Transfers (ODX) feature introduced in Windows Server 2012 R2. In VMM, background intelligent transfer (BITS) is still used as a mechanism for file transfers. However, when possible (for example when copying files to SANs that support ODX), VMM leverages ODX, greatly improving the time performance of virtual machine deployments. For information about Windows ODX, see [Windows Offloaded Data Transfers Overview](http://technet.microsoft.com/library/hh831628.aspx).



