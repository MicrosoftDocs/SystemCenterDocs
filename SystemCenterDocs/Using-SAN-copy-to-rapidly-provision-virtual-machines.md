---
title: Using SAN copy to rapidly provision virtual machines
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3e3c0888-c3dc-4c23-aa4d-3a599f9b0682
---
# Using SAN copy to rapidly provision virtual machines
Rapid provisioning provides a method for deploying new virtual machines to storage arrays without the requirement for copying virtual machines over the network. [!INCLUDE[vmm12sp1_long](./Token/vmm12sp1_long_md.md)] enables you to take advantage of your storage area network \(SAN\) infrastructure for cloning virtual machines, and use a VM template to customize the guest operating system. You can use rapid provisioning to deploy stand\-alone virtual machines and virtual machines that are deployed as part of a service.

Rapid provisioning through SAN copy enables you to quickly create virtual machines from a SAN copy\-capable template. You can create a SAN copy\-capable template from a virtual hard disk that resides on a storage logical unit that supports SAN copy through cloning or snapshots. When you create a new virtual machine by using the SAN copy\-capable template, [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] quickly creates a read\-write copy of the logical unit that contains the virtual hard disk, and places the virtual machine files on the new logical unit.

When [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] deploys a virtual machine by using rapid provisioning through SAN copy, [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] uses a SAN transfer instead of a network transfer. During a SAN transfer, a SAN copy of the logical unit that contains the virtual machine is created and is assigned to the destination host or host cluster. Because the files for a virtual machine are not actually moved over the network when you transfer a virtual machine over a SAN, it is much faster than a transfer over a standard network.

> [!CAUTION]
> Any storage that is accessible by the provisioned computer may be partitioned during the provisioning process even if a specific disk is selected to be used as the operating system disk. In this case data will be lost. To guarantee the use of a specific boot volume, use deep discovery and do not restart the computer before the deployment of the operating system completes.

## Methods for rapid provisioning using SAN copy
You can use either of the following methods to create a SAN copy\-capable template.

> [!NOTE]
> The outlined methods provide a high\-level overview of the workflow, and assume that the prerequisites are met. Links to more detailed procedures for each method are provided. The prerequisites are described in [Prerequisites for rapid provisioning using SAN copy](./Using-SAN-copy-to-rapidly-provision-virtual-machines.md#BKMK_prereq), later in this topic.

### Method 1: Create a SAN copy\-capable template from a new virtual machine

1.  From a storage pool that is managed by [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] and allocated to the host group where the target host resides, create and assign a storage logical unit to the host.

    > [!NOTE]
    > You can also use your storage array vendor’s management tools to create and assign the logical unit.

2.  Create a virtual machine with a blank virtual hard disk file on the logical unit.

3.  Install and customize the guest operating system and the applications that you want. Generalize the image by using Sysprep.exe with the **\/generalize** and the **\/oobe** options to generalize the associated virtual hard disk. For more information about Sysprep, see [Sysprep Command-Line Options](http://technet.microsoft.com/library/hh825033.aspx).

4.  Use the Create VM Template Wizard to create a SAN\-copy capable template from the virtual machine.

    When you create the template, [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] transfers the logical unit that includes the virtual hard disk file from the host to the library through a SAN transfer. The library indexes the virtual hard disk file during the next refresh.

You can then create and deploy new virtual machines by using the SAN copy\-capable template. When you deploy a new virtual machine, [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] creates a clone or snapshot of the logical unit that contains the virtual hard disk file, by using a disk that is allocated from the managed storage pool. [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] automatically unmasks the new logical unit to the host.

For detailed steps, see [How to create a SAN copy-capable template from a new virtual machine](./How-to-create-a-SAN-copy-capable-template-from-a-new-virtual-machine.md).

### Method 2: Create a SAN copy\-capable template from an existing virtual machine

1.  Create a logical unit from a storage pool that is managed by [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] and allocated to the host group where the library server resides. Assign the logical unit to the library server.

    > [!NOTE]
    > If you want to perform this procedure entirely within [!INCLUDE[vmm12short](./Token/vmm12short_md.md)], you must add the library server as a managed Hyper\-V host. This action enables you to assign the logical unit to the library server. If you do not want to make the library server a managed Hyper\-V host, you can use your array vendor’s management tools to register the logical unit to the library server.

2.  On the library server, mount the logical unit to a folder path in the library share.

    > [!NOTE]
    > If the storage is managed by [!INCLUDE[vmm12short](./Token/vmm12short_md.md)], you can mount the logical unit to a folder path in the library share at the same time that you assign the logical unit to the library server.

3.  Copy the existing virtual hard disk file \(that has been generalized by using Sysprep\) to the folder path where you mounted the logical unit.

4.  Create a SAN\-copy capable template by using the virtual hard disk file.

You can then create and deploy new virtual machines by using the SAN copy\-capable template. When you do, [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] creates a clone or snapshot of the logical unit, which automatically creates a new logical unit from the storage pool. [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] automatically unmasks the new logical unit to the host.

For detailed steps, see [How to create a SAN copy-capable template from an existing virtual machine](./How-to-create-a-SAN-copy-capable-template-from-an-existing-virtual-machine.md).

## <a name="BKMK_prereq"></a>Prerequisites for rapid provisioning using SAN copy
Before you begin, ensure that the following prerequisites are met:

-   The storage array must support the new storage management features in [!INCLUDE[vmm12short](./Token/vmm12short_md.md)].

-   The storage array must support cloning or snapshots, and the cloning or snapshots feature must be enabled.

    > [!NOTE]
    > This might require additional licensing from your storage vendor.

-   The storage pool that you want to use for rapid provisioning must be under [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] management. To meet this requirement, you must add the Storage Management Initiative Specification \(SMI\-S\) provider for the array, discover storage pools, classify the storage, and set the preferred allocation method for the storage array to either snapshot or cloning.

-   The storage pool that you want to use for rapid provisioning must be allocated to the host group where you want to use rapid provisioning of virtual machines.

-   The Hyper\-V hosts that you want to use as placement destinations must be members of the host group. Additionally, the following prerequisites must be met:

    -   If you want to create a SAN\-copy capable template from a new virtual machine, the host where you create the virtual machine must also be a member of this host group.

    -   If you want to create a SAN\-copy capable template from an existing virtual machine, and want to create and assign the logical unit from the library server, the library server must be a member of this host group. Therefore, the library server must be a Hyper\-V host. \(If you do not want to add the library server as a host, you can assign the logical unit out\-of\-band by using your storage array vendor’s management tools.\)

-   If you want to use rapid provisioning to deploy generation 2 virtual machines, you must choose a host with an operating system that supports them. Generation 2 virtual machines are supported as of [!INCLUDE[winblue_server_2](./Token/winblue_server_2_md.md)].

    For more information about generation 2 virtual machines, see [Understanding generation 1 and generation 2 virtual machines in VMM](./Understanding-generation-1-and-generation-2-virtual-machines-in-VMM.md).

-   All Hyper\-V hosts that you want to use for rapid provisioning and the library server must have access to the storage array. Also, they must use the same type of SAN connectivity. For SAN migrations to succeed, you cannot have some hosts that connect to the array through Fibre Channel and others that connect through iSCSI. Configuration varies, depending on your storage hardware.

    > [!NOTE]
    > For specific configuration information, see your storage array vendor’s documentation.

    Configuration typically includes the following:

    -   The Multipath I\/O \(MPIO\) feature must be added on each host that will access the Fibre Channel or iSCSI storage array. You can add the MPIO feature through Server Manager. If the MPIO feature is already enabled before you add a host to [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] management, [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] will automatically enable MPIO for supported storage arrays by using the Microsoft provided Device Specific Module \(DSM\). If you already installed vendor\-specific DSMs for supported storage arrays, and then add the host to [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] management, the vendor\-specific MPIO settings will be used to communicate with those arrays.

        If you add a host to [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] before you add the MPIO feature, you must manually configure MPIO to add the discovered device hardware IDs. Or, you can install vendor\-specific DSMs.

        > [!NOTE]
        > For more information, including information about how to install MPIO, see[Microsoft Multipath I/O (MPIO) Users Guide for Windows Server 2012](http://www.microsoft.com/download/details.aspx?id=30450).

    -   If you are using a Fibre Channel storage area network \(SAN\), each host that will access the storage array must have a host bus adapter \(HBA\) installed. Additionally, ensure that the hosts are zoned accordingly so that they can access the storage array.

    -   If you use an iSCSI SAN, ensure that iSCSI portals have been added and that the iSCSI initiator is logged into the array. Additionally, ensure that the Microsoft iSCSI Initiator Service on each host is started and set to **Automatic**. For information about how to create an iSCSI session on a host through [!INCLUDE[vmm12short](./Token/vmm12short_md.md)], see [How to configure storage on a Hyper-V host in VMM](./How-to-configure-storage-on-a-Hyper-V-host-in-VMM.md).

For information about supported storage arrays, how to bring storage under [!INCLUDE[vmm12short](./Token/vmm12short_md.md)] management, how to configure the preferred capacity allocation method for a managed storage array, and how to allocate storage to a host group, see [Overview: configuring storage in VMM](assetId:///928b6f3d-3b6b-4f37-8671-b8fabdd62ad0).

## In this section
Use the following steps to deploy a virtual machine by using rapid provisioning.

|Task|Description|
|--------|---------------|
|Step 1: Use either of the following instructions:<br /><br />-   [How to create a SAN copy-capable template from a new virtual machine](./How-to-create-a-SAN-copy-capable-template-from-a-new-virtual-machine.md)<br />-   [How to create a SAN copy-capable template from an existing virtual machine](./How-to-create-a-SAN-copy-capable-template-from-an-existing-virtual-machine.md)|Describes how to create a SAN copy\-capable template from either a new or existing virtual machine. Includes scenario\-specific prerequisites.|
|Step 2: [How to deploy a new virtual machine from the SAN copy-capable template](./How-to-deploy-a-new-virtual-machine-from-the-SAN-copy-capable-template.md)|Describes how to create and deploy the new virtual machine by using the SAN copy\-capable template.|

## See Also
[Managing virtual machines with VMM](./Managing-virtual-machines-with-VMM.md)
[Managing tenant resources with VMM](./Managing-tenant-resources-with-VMM.md)
[Overview: storage capabilities in VMM](./Overview--storage-capabilities-in-VMM.md)
[Overview: the VMM storage lifecycle](./Overview--the-VMM-storage-lifecycle.md)


