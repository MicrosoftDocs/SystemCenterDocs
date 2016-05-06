---
title: Overview: configuring storage in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 928b6f3d-3b6b-4f37-8671-b8fabdd62ad0
---
# Overview: configuring storage in VMM
This topic describes the following aspects of configuring storage in [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)]:

-   **Usage scenarios**: [Usage scenarios for storage in VMM](../Topic/Overview--configuring-storage-in-VMM.md#BKMK_scenarios)

-   **Basic types**: [Types of storage supported by VMM: local and remote, block and file](../Topic/Overview--configuring-storage-in-VMM.md#BKMK_blockfile)

-   **Protocols**: [Storage protocols and standards supported by VMM](../Topic/Overview--configuring-storage-in-VMM.md#BKMK_protocols)

-   **Overall lifecycle**: [Storage lifecycle: deploying and managing storage resources](../Topic/Overview--configuring-storage-in-VMM.md#BKMK_lifecycle)

For more specific workflows and task sequences, see:

-   Overview: configuring storage using Scale\-Out File Server clusters in VMM

-   [Overview: configuring block storage VMM](../Topic/Overview--configuring-block-storage-VMM.md)

## <a name="BKMK_scenarios"></a>Usage scenarios for storage in VMM
Typical usage scenarios for storage features include using VMM to perform the following:

-   **Configuring storage and making it available to hosts or host clusters**: At the beginning of the storage configuration process, you can use [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] to simplify tasks such as exposing the storage to the virtual machine hosts, initializing disks, and formatting new volumes. With Scale\-Out File Server clusters, you can use [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] to initialize and format volumes, then create Cluster Shared Volumes \(CSVs\) and file shares, and assign permissions so that the host or host cluster can access the file shares. [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] can also assign additional storage to a host or cluster that already has storage assigned.

    [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] also simplifies the process of making storage available to virtual machines and private cloud users. You can create *storage classifications* that fit your environment, for example, **Gold**, **Silver**, and **Bronze**. Then you can assign those classifications to the appropriate storage, for example, to a storage pool. Finally, you can make a particular storage classification available to a particular set of virtual machines or cloud users, avoiding the need to assign each individual unit of storage manually.

    You can also use these methods to automatically assign storage in SAN\-based rapid provisioning scenarios in which LUNs are cloned.

    For more information about the preceding workflow, see one of the following topics:

    -   Overview: configuring storage using Scale\-Out File Server clusters in VMM

    -   [Overview: configuring block storage VMM](../Topic/Overview--configuring-block-storage-VMM.md)

-   **Scale\-Out File Server creation and configuration**: You can use [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] to create a Scale\-Out File Server and manage its storage. For more information, see Overview: configuring storage using Scale\-Out File Server clusters in VMM.

-   **Assignment of storage as part of host cluster creation**: You can use [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] to create a host cluster with up to 64 Hyper\-V nodes. You can automate the assignment of the cluster storage as part of the same workflow. For more information, see:

    -   Creating a cluster in VMM from existing servers running a Windows Server operating system

    -   [Deploying Hyper-V hosts or host clusters from bare metal with VMM](../Topic/Deploying-Hyper-V-hosts-or-host-clusters-from-bare-metal-with-VMM.md)

-   **Rapid provisioning**: Storage arrays can create copies of virtual disks very efficiently with minimal load on the virtual machine host. With [!INCLUDE[vmm12short](../Token/vmm12short_md.md)], you can leverage this capability to rapidly create virtual machines. [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] can instruct the array to create a copy of a virtual disk by provisioning new storage on the array, by using a snapshot, or by cloning. [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] then exposes the storage to the host by mounting the file system and by associating the virtual disk with the virtual machine. With the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] console, you can use rapid provisioning to create stand\-alone virtual machines or service\-based virtual machines. You can also integrate rapid provisioning into your own provisioning tools by using Windows PowerShell. For more information, see [Using SAN copy to rapidly provision virtual machines](../Topic/Using-SAN-copy-to-rapidly-provision-virtual-machines.md).

## <a name="BKMK_blockfile"></a>Types of storage supported by VMM: local and remote, block and file
The two broadest categories of storage that [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] recognizes are local and remote storage. Local storage represents storage capacity directly attached to a server \(or on the server\), and is typically used for low\-cost virtualization solutions. Remote storage offloads work from the server to an external storage device where the storage hardware provides scaling and capacity.

[!INCLUDE[vmm12short](../Token/vmm12short_md.md)] helps you configure and manage both block storage and file storage:

-   **Block storage**: [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] supports the use of block\-level storage devices that expose logical unit numbers \(LUNs\) for storage, by using Fibre Channel, iSCSI, and Serial Attached SCSI \(SAS\) connection mechanisms. For more information, see [Configuring block storage in VMM](../Topic/Configuring-block-storage-in-VMM.md).

-   **File storage**: [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] supports the use of a Scale\-Out File Server, using file shares, as the storage for hosts or host clusters. For more information, see Configuring storage using Scale\-Out File Server clusters in VMM.

    Network shares that support the Server Message Block \(SMB\) 3.0 Protocol can also reside on a network\-attached storage \(NAS\) device from storage vendors such as EMC and NetApp.

## <a name="BKMK_protocols"></a>Storage protocols and standards supported by VMM
[!INCLUDE[vmm12short](../Token/vmm12short_md.md)] supports a variety of storage protocols, standards, and providers:

-   **Windows Storage Management API \(SMAPI\) and related providers**:

    -   [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] supports SMAPI. SMAPI was introduced in [!INCLUDE[win8_server_2](../Token/win8_server_2_md.md)] for the management of directly attached storage and external storage arrays. SMAPI is combined with a Storage Management Provider \(SMP\), or the Microsoft Standards\-Based Storage Management Service and an SMI\-S provider. SMAPI supersedes the Virtual Disk Service \(VDS\) application programming interface \(API\) in [!INCLUDE[win8_server_2](../Token/win8_server_2_md.md)]. For more information, see [An Introduction to Storage Management in Windows Server](http://blogs.msdn.com/b/san/archive/2012/06/26/an-introduction-to-storage-management-in-windows-server-2012.aspx).

    -   [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] uses SMAPI to manage external storage by using SMP, or uses SMAPI together with a standards\-based Storage Management Service to communicate with storage that is compliant with the Storage Management Initiative Specification \(SMI\-S\).

-   **Scale\-Out File Servers with Storage Spaces**: [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] provides support for creating and managing Scale\-Out File Servers with Storage Spaces. For more information, see Configuring storage using Scale\-Out File Server clusters in VMM.

-   **SMB 3.0 file shares**: As of [!INCLUDE[win8_server_2](../Token/win8_server_2_md.md)], Server Message Block \(SMB\) 3.0 file shares are supported for shared storage for Hyper\-V. By using [!INCLUDE[vmm12short](../Token/vmm12short_md.md)], you can assign SMB file shares to Hyper\-V hosts and host clusters.

-   **Thin provisioning logical units**: [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] supports creation of a thin provisioning logical unit \(LU\), including creation of a thin provisioned logical unit on a storage pool. Thin provisioning makes it possible for you to allocate more capacity to specific applications or users than is physically available. The storage array must support thin provisioning, and the storage administrator must enable thin provisioning for a storage pool.

-   **iSCSI arrays**: In addition to discovery and management of iSCSI arrays with static targets, [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] includes support for the discovery and management of iSCSI target arrays that support dynamic and manual targets, for example, Starwind, HP P2000, Dell EqualLogic, and Microsoft iSCSI Software Target.

-   **Microsoft iSCSI Software Target**: [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] provides support for the Microsoft iSCSI Software Target by using an SMI\-S provider. Microsoft iSCSI was integrated into the server operating system as of [!INCLUDE[win8_server_2](../Token/win8_server_2_md.md)]. The installation file \(.msi\) for the SMI\-S provider for Microsoft iSCSI Target Server is included in the installation, in the path of CDLayout.EVAL\\amd64\\Setup\\msi\\iSCSITargetPRov\\iSCSITargetSMISProvider.msi. For more information about the Microsoft iSCSI Software Target, see:

    -   [Configuring iSCSI Target Server and the SMI-S Provider in VMM](../Topic/Configuring-iSCSI-Target-Server-and-the-SMI-S-Provider-in-VMM.md)

    -   [Introduction of iSCSI Target in Windows Server 2012](http://blogs.technet.com/b/filecab/archive/2012/05/21/introduction-of-iscsi-target-in-windows-server-2012.aspx)

    -   [Six Uses for the Microsoft iSCSI Software Target](http://blogs.technet.com/b/storageserver/archive/2009/12/11/six-uses-for-the-microsoft-iscsi-software-target.aspx)

## <a name="BKMK_lifecycle"></a>Storage lifecycle: deploying and managing storage resources
[!INCLUDE[vmm12short](../Token/vmm12short_md.md)] helps you manage storage throughout the lifecycle of storage resources. The following list describes a generalized workflow. For a workflow that specifically describes Scale\-Out File Servers, see Overview: configuring storage using Scale\-Out File Server clusters in VMM.

The storage lifecycle goes through the following stages:

-   **Storage discovery**: By using [!INCLUDE[vmm12short](../Token/vmm12short_md.md)], you can automatically discover local and remote storage that includes storage arrays, pools, and logical units, such as storage volumes or logical unit numbers \(LUNs\), disks, volumes, and virtual disks.

-   **Storage classification**: You can create classifications that fit your situation, then classify discovered storage and manage it based on your own classifications.

-   **Storage provisioning**: By using [!INCLUDE[vmm12short](../Token/vmm12short_md.md)], you can provision new LUNs or disks from available capacity for a Hyper\-V host or host cluster. New LUNs can be provisioned by using any of the following methods. The method that you use depends on the type of storage array and the virtualization workload that you must deploy.

    -   **From file shares on Windows\-based file servers**: You can provision new file shares on Scale\-Out File Servers, and on NAS devices.

    -   **From available capacity**: If you have a collection of available storage, you can create a new LUN, disk, or file share from it. You can control the number and size of LUNs, disks, or shares that you create.

    -   **From a writeable snapshot of an existing LUN**: By creating a writeable snapshot of an existing LUN, you can rapidly create many copies of an existing virtual disk. You can provision multiple virtual machines in a short amount of time, with minimal load on the hosts. Depending on the array, snapshots use space very efficiently and can be created almost instantaneously.

    -   **From a clone of a LUN**: By creating a clone of an existing LUN, you offload the work of creating a full copy of a virtual disk to the array. Depending on the array, clones typically do not use space efficiently and can take some time to create.

-   **Storage allocation**: You can allocate available storage pools and LUNs to defined host groups that can represent, for example, business groups and locations. Resources typically must be allocated on the host group level before they can be assigned to hosts. If you allocate a storage pool, you can work from the host, and create and assign LUNs as needed. In addition, [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] can automatically create LUNs from the storage pool, if you use rapid provisioning to provision virtual machines with SAN snapshots or cloning.

-   **Storage decommissioning**: By using [!INCLUDE[vmm12short](../Token/vmm12short_md.md)], you can decommission managed storage. This capability is important to avoid running out of storage capacity over time.

## See Also
[Configuring Storage in VMM](../Topic/Configuring-Storage-in-VMM.md)

