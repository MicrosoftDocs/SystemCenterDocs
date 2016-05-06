---
title: How to allocate storage logical units to a host group in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7a13ae51-326c-4623-ba16-a330e7eac2a1
---
# How to allocate storage logical units to a host group in VMM
You can use the following procedure to allocate storage logical units to a host group in the [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)] console. After you make the logical units available to a host group, if servers that are running Hyper\-V are configured to access the storage, you can assign the logical units to servers that are running Hyper\-V and host clusters that reside in the host group and any child host groups.

> [!TIP]
> You can also allocate logical units to a host group through the host group properties.

## Prerequisites
Before you begin this procedure, ensure that:

-   The storage pools where the logical units reside have been discovered by [!INCLUDE[vmm12short](../Token/vmm12short_md.md)]. For more information, see [How to add and classify SMI-S and SMP storage devices in VMM](../Topic/How-to-add-and-classify-SMI-S-and-SMP-storage-devices-in-VMM.md).

-   Unassigned logical units must exist in the storage pools from which you want to allocate storage capacity. For information about creating logical units by using [!INCLUDE[vmm12short](../Token/vmm12short_md.md)], see [How to provision storage logical units in VMM](../Topic/How-to-provision-storage-logical-units-in-VMM.md). Alternately, you can create logical units by using your storage array vendor’s management tools or by using a server that you use to manage Hyper\-V. This server must be able to access the storage array, and a storage pool must have been allocated to the host group where the server that is running Hyper\-V resides. For more information, see [How to allocate storage pools to a host group in VMM](../Topic/How-to-allocate-storage-pools-to-a-host-group-in-VMM.md).

**Account requirements** To complete this procedure, you must be a member of the Administrator user role or a member of the Delegated Administrator user role where the management scope includes the target host group.

#### To allocate logical units to a host group

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, click **Storage**.

3.  On the **Home** tab, click **Allocate Capacity** to open the **Allocate Storage Capacity** dialog box.

4.  In the **Host groups** list, click the host group to which you want to allocate storage capacity.

    Total and available storage capacity information is displayed for the host group. This information includes the total and available capacity for both local and remote storage, and total and available allocated storage.

5.  To allocate logical units to the host group, click **Allocate Logical Units** to open the **Allocate Logical Units** dialog box.

6.  Optionally, select the **Display as available only storage arrays that are visible to any host in the host group** check box.

7.  For each logical unit that you want to add, under **Available logical units**, click a logical unit that you want to allocate to the host group, and then click **Add**.

8.  When you are finished, click **OK**.

After you have allocated logical units to a host group, you can assign logical units to servers that are running Hyper\-V and host clusters in the host group that can access the storage array. For more information, see the topics [How to configure storage on a Hyper-V host in VMM](../Topic/How-to-configure-storage-on-a-Hyper-V-host-in-VMM.md) and [How to configure storage on a Hyper-V host cluster in VMM](../Topic/How-to-configure-storage-on-a-Hyper-V-host-cluster-in-VMM.md).

## See Also
[Configuring block storage in VMM](../Topic/Configuring-block-storage-in-VMM.md)
[Managing storage resources and capacity with VMM](../Topic/Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](../Topic/Managing-fabric-resources-with-VMM.md)

