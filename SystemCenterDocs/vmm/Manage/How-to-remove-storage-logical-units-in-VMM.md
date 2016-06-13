---
title: How to remove storage logical units in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 27d1eac7-6467-4dc1-b9f5-77a3d09ce3d0
---
# How to remove storage logical units in VMM
Use the following procedure to delete a logical unit that is under [!INCLUDE[vmm12sp1_long](../../includes/vmm12sp1_long_md.md)] management.

## Prerequisites
Ensure that the logical unit that you want to delete is not currently assigned to a server that is running Hyper\-V or is assigned as storage to a virtual machine. For information about how to remove an assigned logical unit from a server that is running Hyper\-V or a server in a host cluster, see [How to configure storage on a Hyper-V host in VMM](How-to-configure-storage-on-a-Hyper-V-host-in-VMM.md) and [How to configure storage on a Hyper-V host cluster in VMM](How-to-configure-storage-on-a-Hyper-V-host-cluster-in-VMM.md).

**Account requirements** You must be a member of the Administrator user role or a member of the Delegated Administrator user role to complete this procedure.

#### To delete a logical unit

1.  Open the **Fabric** workspace.

2.  In the **Fabric** workspace, expand **Storage**, and then click **Classifications and Pools**.

3.  On the **Home** tab, in the **Show** group, click **Fabric Resources**.

4.  In the **Classifications, Storage Pools, and Logical Units** pane, expand the storage classification that is assigned to the storage pool where the logical unit resides. Expand the storage pool, and then click the logical unit that you want to remove.

5.  On the **Home** tab, in the **Remove** group, click **Remove**.

6.  Review the warning message.

    > [!CAUTION]
    > If you continue, the data on the logical unit is permanently deleted.

7.  Click **OK** to continue and delete the logical unit. Open the **Jobs** workspace to view the job status.

    If removal is successful, the logical unit is deleted and is removed from the list in the **Classifications, Storage Pools, and Logical Units** pane.

## See Also
[Configuring block storage in VMM](Configuring-block-storage-in-VMM.md)
[Managing storage resources and capacity with VMM](Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


