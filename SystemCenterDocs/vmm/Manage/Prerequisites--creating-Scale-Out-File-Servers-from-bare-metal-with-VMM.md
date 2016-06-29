---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  Prerequisites  creating Scale Out File Servers from bare metal with VMM
ms.technology:  virtual-machine-manager
ms.assetid:  ae6ab645-0882-420d-942a-1617d76b9b52
---

# Prerequisites: creating Scale-Out File Servers from bare metal with VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

This topic lists the prerequisites for the process of provisioning Scale-Out File Servers from bare metal using Virtual Machine Manager (VMM):

-   [Physical computer and related requirements](#BKMK_computer)

-   [PXE server requirements](#BKMK_pxe)

-   [Profile requirements (for the physical computer profile)](#BKMK_profile)

## <a name="BKMK_computer"></a>Physical computer and related requirements
The computers to which you deploy Scale-Out File Servers can be �bare-metal computers� (no operating system installed), or computers with an installed operating system that will be overwritten during the process.

-   **BMC**: Each physical computer must have a baseboard management controller (BMC) installed and configured for out-of-band management by VMM.

-   **BIOS boot order**: On each computer, set the BIOS boot order to boot from a Pre-Boot Execution Environment (PXE)-enabled network adapter as the first device.

-   **DNS replication time**: If your environment has multiple Domain Name System (DNS) servers, where DNS replication may take some time, we strongly recommend that you create DNS entries for the computer names that will be assigned to the physical computers, and allow time for DNS replication to occur. Otherwise, deployment of the computers may fail.

## <a name="BKMK_pxe"></a>PXE server requirements
You must have a PXE server configured with Windows Deployment Services.
The PXE server must be in the same subnet as the physical computers that you want to provision, and must be configured for VMM to use as described in [How to add a PXE server to VMM](How-to-add-a-PXE-server-to-VMM.md).

## <a name="BKMK_profile"></a>Profile requirements (for the physical computer profile)
Physical computer profiles include information such as the location of the operating system image to use during deployment, and hardware and operating system settings.

> [!IMPORTANT]
> Determine whether your computers use Extensible Firmware Interface (EFI) or basic input/output system (BIOS). If you have computers of each type, you must create a separate profile for each type.

Before you create a physical computer profile, review the following requirements:

-   [Virtual hard disk requirements](Prerequisites--creating-hosts-or-host-clusters-from-bare-metal-with-VMM.md#BKMK_vhd)

-   [Operating system requirements for the virtual hard disk that you deploy](Prerequisites--creating-hosts-or-host-clusters-from-bare-metal-with-VMM.md#BKMK_osreq)

-   [Answer file or custom resources (optional)](Prerequisites--creating-hosts-or-host-clusters-from-bare-metal-with-VMM.md#BKMK_answer)

-   [Other requirements for a physical computer profile](Prerequisites--creating-hosts-or-host-clusters-from-bare-metal-with-VMM.md#BKMK_other)

If you're ready to create the physical computer profile, see [How to create a physical computer profile to provision Scale-Out File Server nodes from bare metal in VMM](How-to-create-a-physical-computer-profile-to-provision-Scale-Out-File-Server-nodes-from-bare-metal-in-VMM.md).

### <a name="BKMK_vhd"></a>Virtual hard disk requirements
One of the elements you need for deploying Scale-Out File Servers from bare metal is a generalized virtual hard disk with an appropriate operating system. The virtual hard disk must be on a library share. The choice of operating system is listed in [Operating system requirements for the virtual hard disk that you deploy](Prerequisites--creating-hosts-or-host-clusters-from-bare-metal-with-VMM.md#BKMK_osreq), later in this topic.

> [!NOTE]
> -   We recommend that for production servers, you use a fixed disk (.vhd or .vhdx file format) to increase performance and to help protect user data. Note that by default, when you create a physical computer profile, VMM converts a dynamic disk to a fixed disk.
> -   If you use Remote Desktop Services (RDS) to manage servers, we recommend that you enable the RDS connections in the image. You can also enable RDS by using an answer file in the physical computer profile.

To create the virtual hard disk, you can create a virtual machine, install the guest operating system, and then use Sysprep with the **/generalize** and the **/oobe** options. For more information, see [Sysprep Command-Line Options](http://technet.microsoft.com/library/hh825033.aspx).

Another method that you can use to create a virtual hard disk is to follow the prerequisites and Steps 1 and 2 in the following topic: [Boot to VHD (Native Boot): Add a Virtual Hard Disk to the Boot Menu](http://technet.microsoft.com/library/hh825691.aspx). For more information, see [Understanding Virtual Hard Disks with Native Boot](http://technet.microsoft.com/library/hh825689.aspx).

### <a name="BKMK_osreq"></a>Operating system requirements for the virtual hard disk that you deploy
The operating system on the virtual hard disks that you deploy on Scale-Out File Servers must support the boot from virtual hard disk (VHD) option. For information about supported operating systems, see [Server Operating Systems](https://technet.microsoft.com/library/dn997307.aspx).

> [!NOTE]
> You can add a Windows Server Technical Preview node to a Windows Server 2012 R2 cluster, subject to the requirements specified previously; however, you cannot add a Windows Server 2012 R2 node to a Windows Server Technical Preview cluster.

For more information, see [Understanding Virtual Hard Disks with Native Boot](http://technet.microsoft.com/library/hh825689.aspx).

### <a name="BKMK_answer"></a>Answer file or custom resources (optional)
If you want a physical computer profile to include references to an answer file (Unattend.xml file) or to custom resources (for example, an application installer that you will reference in post-deployment script commands), create the answer file or obtain the custom resources before deployment, and add them to a VMM library share.

> [!NOTE]
> Within a library share, place custom resources in one or more folders with a .CR (custom resource) extension. VMM will recognize them as custom resources.

For example, you might want to create an answer file to enable Remote Desktop Services and place it on a library share. Then you can select that file when you configure a physical computer profile.

> [!IMPORTANT]
> When you deploy Scale-Out File Servers from bare metal, VMM automatically performs the following (no answer file or post-deployment commands needed):
> 
> -   Installs the
>                       failover cluster feature and file server role on each node.
> -   After creating the cluster, enables the Scale-Out File Server role for the cluster.

### <a name="BKMK_other"></a>Other requirements for a physical computer profile
Before you create a physical computer profile, also review the following requirements:

-   **Custom drivers** If you plan to assign custom drivers, the driver files must exist in the library. You can tag the drivers in the library, so that you can later filter them by tag. For more information, see [How to add driver files to the VMM library](How-to-add-driver-files-to-the-VMM-library.md).

-   **Run As accounts** Two Run As accounts will be needed:

    -   A Run As account for joining computers to the domain. You can create a Run As account in the **Settings** workspace. For example, you could create the Run As account **Add Physical Computer**. For more information, see [How to create a Run As account in VMM](How-to-create-a-Run-As-account-in-VMM.md).

    -   A Run As account for access to the baseboard management controller (BMC) on each computer. For example, you could create the Run As account **BMC Administrator**.

## See Also
[Deploying Scale-Out File Servers from bare metal with VMM](Deploying-Scale-Out-File-Servers-from-bare-metal-with-VMM.md)
[Managing Scale-Out File Servers with VMM](Managing-Scale-Out-File-Servers-with-VMM.md)
[Managing storage resources and capacity with VMM](Managing-storage-resources-and-capacity-with-VMM.md)
[Managing infrastructure resources with VMM](Managing-infrastructure-resources-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)



