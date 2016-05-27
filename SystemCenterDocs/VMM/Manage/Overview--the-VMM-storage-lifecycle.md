---
title: Overview: the VMM storage lifecycle
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b0d5224-065f-4418-87ab-88fcb809b37d
---
# Overview: the VMM storage lifecycle
With [!INCLUDE[vmm12sp1_long](../../includes/vmm12sp1_long_md.md)], you can simplify and automate the process of discovering, classifying, and assigning storage to support your virtualized environment. You can also use [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] to modify and expand your storage resources. In general, [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] supports the following lifecycle for storage resources \(details may vary for different storage technologies\).

1.  **Classify storage.** You can use storage classifications as labels to group or subdivide your storage resources. When users create virtual machines, they can assign storage based on the label without knowing the underlying configuration.

    For more information, see [How to create storage classifications in VMM](How-to-create-storage-classifications-in-VMM.md).

    > [!NOTE]
    > You can create storage classifications before or after [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] discovers you storage devices; you can also create classifications as needed while you configure the storage capacity.

    > [!NOTE]
    > If you are using Scale\-Out File Servers for storage, you can add quality of service policies to your storage classifications; for more information, see [Managing quality of service policies for Scale-Out File Servers in VMM](Managing-quality-of-service-policies-for-Scale-Out-File-Servers-in-VMM.md).

2.  **Discover storage devices.**[!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] can automatically discover local and remote storage resources that include storage arrays, pools, and logical units.

    For more information, see the following topics:

    -   [How to add an existing Scale-Out File Server to storage in VMM](How-to-add-an-existing-Scale-Out-File-Server-to-storage-in-VMM.md)

    -   [How to create a Scale-Out File Server in VMM using existing servers](How-to-create-a-Scale-Out-File-Server-in-VMM-using-existing-servers.md)

    -   [How to discover and classify Virtual Fibre Channel Fabrics with VMM](How-to-discover-and-classify-Virtual-Fibre-Channel-Fabrics-with-VMM.md)

    -   [How to add and classify SMI-S and SMP storage devices in VMM](How-to-add-and-classify-SMI-S-and-SMP-storage-devices-in-VMM.md)

    > [!NOTE]
    > If you want to use a Scale\-out File Server for storage, you can start with a set of unconfigured computers and use [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] to provision them \(also known as bare\-metal provisioning a Scale\-out File Server\). At the end of the provisioning process, the Scale\-out File Server is ready to configure with [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)]. For more information, see [How to deploy a Scale-Out File Server from bare metal in VMM](How-to-deploy-a-Scale-Out-File-Server-from-bare-metal-in-VMM.md).

3.  **Configure the storage structure.** After [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] discovers resources, you can use [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] to configure them. For example, you can use [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] to initialize disks and format volumes. You can configure either block or file storage types: depending on the type of storage device, you can create and configure file shares or logical units.

    Alternatively, you can create logical units out\-of\-band by using your array vendor’s management tools. 
      If you use this method, it takes some time for [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] to discover and reflect the changes.

    For more information, see the following topics:

    -   [Configuring storage using Scale-Out File Servers in VMM](Configuring-storage-using-Scale-Out-File-Servers-in-VMM.md)

    -   [Configuring block storage in VMM](Configuring-block-storage-in-VMM.md)

    -   [Managing Virtual Fibre Channel fabrics with VMM](Managing-Virtual-Fibre-Channel-fabrics-with-VMM.md)

    > [!NOTE]
    > If you are using the rapid SAN provisioning method to create virtual machines, [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] configures the appropriate logical units automatically. For more information, see [Using SAN copy to rapidly provision virtual machines](Using-SAN-copy-to-rapidly-provision-virtual-machines.md).

4.  **Assign storage to a host group.** You can use [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] to group your virtual machine hosts, and then assign resources at the host group level.
    For example, you can create host groups that represent different locations business groups, and assign different storage resources to those groups according to their location or usage needs.

    For more information, see the following topics:

    -   [How to allocate storage pools to a host group in VMM](How-to-allocate-storage-pools-to-a-host-group-in-VMM.md)

    -   [How to allocate storage logical units to a host group in VMM](How-to-allocate-storage-logical-units-to-a-host-group-in-VMM.md)

5.  **Assign storage to hosts and clusters.** After you configure storage and assign storage to host groups, you can assign specific storage resources to virtual machine hosts and host clusters. If you allocated a storage pool to a host group, you can create and optionally assign logical units directly in the **Properties** dialog box of a host or host cluster.

    For more information, see the following topics:

    -   [How to configure storage on a Hyper-V host in VMM](How-to-configure-storage-on-a-Hyper-V-host-in-VMM.md)

    -   [How to configure storage on a Hyper-V host cluster in VMM](How-to-configure-storage-on-a-Hyper-V-host-cluster-in-VMM.md)

    -   [How to assign file shares on a Scale-Out File Server to a Hyper-V host or cluster in VMM](How-to-assign-file-shares-on-a-Scale-Out-File-Server-to-a-Hyper-V-host-or-cluster-in-VMM.md)

    > [!NOTE]
    > If you are using the rapid SAN provisioning method to create virtual machines, [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] assigns the appropriate logical units automatically. For more information, see [Using SAN copy to rapidly provision virtual machines](Using-SAN-copy-to-rapidly-provision-virtual-machines.md).

6.  **Make storage available to users**. You can associate specific storage classifications with virtual machine templates or private clouds. When users create virtual machines using those templates or within those private clouds, those virtual machines automatically use the appropriate storage resources.

    For more information, see the following topics:

    -   [How to create a virtual machine template](How-to-create-a-virtual-machine-template.md)

    -   [Creating and managing private clouds with VMM](assetId:///6fbce258-d10e-4bc0-91fc-de4f5e00905f)

7.  **Modify storage resources as needed.**

    For more information, see the following topics:

    -   [Modifying Scale-Out File Servers in VMM](Modifying-Scale-Out-File-Servers-in-VMM.md)

    -   [How to add a bare-metal computer to a Scale-Out File Server in VMM](How-to-add-a-bare-metal-computer-to-a-Scale-Out-File-Server-in-VMM.md)

    -   [Upgrading Windows Server 2012 R2 Scale-Out File Servers to Windows Server 2016 Technical Preview in VMM](Upgrading-Windows-Server-2012-R2-Scale-Out-File-Servers-to-Windows-Server-2016-Technical-Preview-in-VMM.md)

    -   [How to remove storage logical units in VMM](How-to-remove-storage-logical-units-in-VMM.md)

## See Also
[Managing storage resources and capacity with VMM](Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


