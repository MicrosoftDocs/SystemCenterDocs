---
title: How to provision storage logical units in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 435cbfad-3cc6-465a-aee9-ca78c02d525f
---
# How to provision storage logical units in VMM
You can use the following procedure to create logical units from storage pools that are managed by [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)].

> [!NOTE]
> If you allocate a storage pool to a host group, you can also create and assign logical units directly from managed servers that are running Hyper\-V in the host group. For more information, see [How to configure storage on a Hyper-V host in VMM](../Topic/How-to-configure-storage-on-a-Hyper-V-host-in-VMM.md) and [How to configure storage on a Hyper-V host cluster in VMM](../Topic/How-to-configure-storage-on-a-Hyper-V-host-cluster-in-VMM.md).

Before you begin this procedure, ensure that one or more storage pools are defined in [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] management. For more information, see [Overview: configuring block storage VMM](../Topic/Overview--configuring-block-storage-VMM.md) and [How to add and classify SMI-S and SMP storage devices in VMM](../Topic/How-to-add-and-classify-SMI-S-and-SMP-storage-devices-in-VMM.md).

**Account requirements** To complete this procedure, you must be member of the Administrator user role or a member of the Delegated Administrator user role.

### To create logical units

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, click **Storage**.

3.  Right\-click **Classification and Pools**, and then click **Create Logical Unit**.

4.  To create a logical unit, in the **Create Logical Unit** dialog box, do the following:

    1.  In the **Storage pool** list, click the storage pool that you want to use.

    2.  In the **Name** box, enter a name for the logical unit. Use only alphanumeric characters.

    3.  Optionally, in the **Description** box, enter a description for the logical unit.

    4.  In the **Size \(GB\)** box, enter the size of the logical unit, in gigabytes.

    5.  When you are finished, click **OK**.

    To view the job status, open the **Jobs** workspace.

5.  To verify that the logical unit was created, follow these steps:

    1.  In the **Fabric** workspace, expand **Storage**, and then click **Classifications and Pools**.

    2.  On the **Home** tab, in the **Show** group, click **Fabric Resources**.

    3.  In the **Classifications, Storage Pools, and Logical Units** pane, expand the storage classification for the pool where you created the logical unit, and then expand the storage pool.

    4.  In the list of logical units, verify that the new logical unit appears.

You can now assign the logical unit to a host group. For more information, see [How to allocate storage logical units to a host group in VMM](../Topic/How-to-allocate-storage-logical-units-to-a-host-group-in-VMM.md).

## See Also
[Configuring block storage in VMM](../Topic/Configuring-block-storage-in-VMM.md)
[Managing storage resources and capacity with VMM](../Topic/Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](../Topic/Managing-fabric-resources-with-VMM.md)

