---
title: How to allocate storage pools to a host group in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 109cc677-3ae5-4a89-b8bb-12fa9d5f2f13
---
# How to allocate storage pools to a host group in VMM
You can use the following procedure to allocate one or more storage pools to a host group in [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)]. After you allocate a storage pool to a host group, you can do either of the following:

-   Create logical units from servers that are running Hyper\-V in the host group that can access the storage array where the storage pool resides.

    > [!NOTE]
    > For more information, see [How to configure storage on a Hyper-V host in VMM](../Topic/How-to-configure-storage-on-a-Hyper-V-host-in-VMM.md) and [How to configure storage on a Hyper-V host cluster in VMM](../Topic/How-to-configure-storage-on-a-Hyper-V-host-cluster-in-VMM.md).

-   Use the storage pool for the rapid provisioning of virtual machines. During rapid provisioning by using storage area network \(SAN\) cloning or snapshots, [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] requests a copy of an existing logical unit through a SAN copy\-capable storage array. Therefore, you do not have to create logical units beforehand. For more information, see [Using SAN copy to rapidly provision virtual machines](../Topic/Using-SAN-copy-to-rapidly-provision-virtual-machines.md).

> [!NOTE]
> You can also allocate storage pools to a host group through the host group properties.

**Account requirements** To complete this procedure, you must be a member of the Administrator user role or a member of the Delegated Administrator user role where the management scope includes the target host group.

### To allocate storage pools to a host group

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, click **Storage**.

3.  On the **Home** tab, click **Allocate Capacity**.

    The **Allocate Storage Capacity** dialog box opens.

    > [!NOTE]
    > To allocate storage capacity if you are a delegated administrator, where your management scope is restricted to specific host groups, you must right\-click a host group that is included in your scope, click **Properties**, and then click the **Storage** tab. Then, continue to step 5.

4.  In the **Host groups** list, click the host group to which you want to allocate storage capacity.

    Total and available storage capacity information is displayed for the host group. The storage capacity information includes the total and available capacity for both local and remote storage, and total and available allocated storage.

5.  To allocate storage pools to the host group, click **Allocate Storage Pools** to open the **Allocate Storage Pools** dialog box.

6.  Optionally, select the **Display as available only storage arrays that are visible to any host in the host group** check box.

7.  For each storage pool that you want to add, under **Available storage pools**, click a storage pool that you want to allocate to the host group, and then click **Add**. When you are finished, click **OK**.

## See Also
[Configuring block storage in VMM](../Topic/Configuring-block-storage-in-VMM.md)
[Managing storage resources and capacity with VMM](../Topic/Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](../Topic/Managing-fabric-resources-with-VMM.md)

