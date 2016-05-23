---
title: Overview: configuring block storage VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5fecd415-77ed-47b3-b812-4525986bc403
---
# Overview: configuring block storage VMM
The topics in this section support the [!INCLUDE[vmm12sp1_long](../../Token/vmm12sp1_long_md.md)] storage lifecycle as it applies to block storage devices.

1.  **Classify storage**—The process of classifying storage assigns a meaningful classification to storage pools. For example, you might assign a classification of GOLD to a storage pool that resides on the fastest, most redundant storage array. For instructions, see [How to create storage classifications in VMM](How-to-create-storage-classifications-in-VMM.md).

    > [!NOTE]
    > You can create storage classifications before or after [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] discovers you storage devices; you can also create classifications as needed while you configure the storage capacity.

2.  **Discover storage**—From the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] console, start the Add Storage Devices Wizard, and select the required provider type, Windows\-based file server, SMI\-S, or WMI SMP. The Windows\-based file server and SMI\-S providers require an IP address or FQDN. For SMI\-S, you connect to the SMI\-S storage provider to discover storage. For WMI SMP providers, you select the required provider from a drop\-down list box. For instructions, see [How to add and classify SMI-S and SMP storage devices in VMM](How-to-add-and-classify-SMI-S-and-SMP-storage-devices-in-VMM.md).

3.  **Select a method for creating logical units**—Specify how logical units are to be created during virtual machine rapid provisioning. Note that, by default, new logical units are created from available capacity. You only have to modify this default setting if you want to use rapid provisioning with SAN copy technology, such as cloning or snapshots. For instructions, see [How to select a method for creating logical units in VMM](How-to-select-a-method-for-creating-logical-units-in-VMM.md).

4.  **Provision storage**—Create logical units of storage. For instructions, see [How to provision storage logical units in VMM](How-to-provision-storage-logical-units-in-VMM.md). Alternatively, you can create logical units out\-of\-band by using your array vendor’s management tools. If you use this method, it takes some time for [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] to refresh and reflect the changes.

5.  **Assign storage to a host group**—From the Storage node of the [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] console or in the **Properties** dialog box of the target host group, allocate pre\-created logical units or storage pools to specific host groups. For instructions, see [How to allocate storage logical units to a host group in VMM](How-to-allocate-storage-logical-units-to-a-host-group-in-VMM.md), and [How to allocate storage pools to a host group in VMM](How-to-allocate-storage-pools-to-a-host-group-in-VMM.md).

    > [!NOTE]
    > If you allocate a storage pool, you can create and assign logical units directly from managed hosts in the host group that can access the storage array. In addition, [!INCLUDE[vmm12short](../../Token/vmm12short_md.md)] can automatically create logical units from the storage pool if you use rapid provisioning to provision virtual machines by using SAN snapshots or cloning. During the rapid provisioning process, logical units are automatically created and assigned.

6.  **Assign the storage to hosts and clusters**—After you configure storage and assign storage to host groups, you can assign the storage to servers that are running Hyper\-V and host clusters as shared via a Cluster Shared Volume \(CSV\) or available storage. Note that all nodes in the cluster should have access to the storage array by using host bus adapters \(HBA\) or iSCSI. If you allocated a storage pool to a host group, you can create and optionally assign logical units directly in the **Properties** dialog box of a host or host cluster. If the storage array supports iSCSI host connectivity, you can create iSCSI sessions to the storage array in the **Properties** dialog box of a host. For instructions, see:

    1.  [How to configure storage on a Hyper-V host in VMM](How-to-configure-storage-on-a-Hyper-V-host-in-VMM.md)

    2.  [How to configure storage on a Hyper-V host cluster in VMM](How-to-configure-storage-on-a-Hyper-V-host-cluster-in-VMM.md)

    > [!NOTE]
    > The hosts must be able to access the storage array. For example, if you use a Fibre Channel SAN, each host must have a host bus adapter \(HBA\) and must be zoned correctly. For more information about Fibre Channel, see [Managing Virtual Fibre Channel fabrics with VMM](Managing-Virtual-Fibre-Channel-fabrics-with-VMM.md).

7.  In needed, you can remove logical units. For instructions, see [How to remove storage logical units in VMM](How-to-remove-storage-logical-units-in-VMM.md).

## See Also
[Configuring block storage in VMM](Configuring-block-storage-in-VMM.md)
[Managing storage resources and capacity with VMM](Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


