---
title: How to create a host group structure in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a515169d-50f3-4b3f-add4-9dd7354e6208
---
# How to create a host group structure in VMM
You can use the following procedures to create a host group structure in [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)] that aligns to your organizational needs.

### To create a host group structure

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Servers**, and then do either of the following:

    -   Right\-click **All Hosts**, and then click **Create Host Group**.

    -   Click **All Hosts**. On the **Folder** tab, in the **Create** group, click **Create Host Group**.

    VMM creates a new host group that is named **New host group**, with the host group name highlighted.

3.  Type a new name, and then press ENTER.

    For example, type **Seattle**, and then press ENTER.

    > [!NOTE]
    > To rename a host group, do either of the following:
    > 
    > -   Right\-click the host group, and then click **Rename**.
    > -   On the **General** tab of the host group properties, enter the host group name in the **Name** box.

4.  Repeat the steps in this procedure to create the rest of the host group structure.

    For example, create the following host group structure. This host group structure is used in the examples throughout the documentation and is used to help demonstrate the concepts. You can adapt the examples to your test environment.

    > [!TIP]
    > To create a host group at a specific location in the tree, right\-click the desired parent node, and then click **Create Host Group**.

    **Seattle**

    **Tier0\_SEA**

    **Tier1\_SEA**

    **Tier2\_SEA**

    **New York**

    **Tier0\_NY**

    **Tier1\_NY**

    **Tier2\_NY**

    > [!NOTE]
    > This example host group structure is based on location and the capabilities of the hardware, including the level of redundancy. For example, in Tier0 you may have clustered hosts, the fastest and most reliable storage with replication, load balancing and the most network throughput. Tier1 may have clustered hosts, but lower speed storage that is not replicated. Tier2 may consist of stand\-alone hosts with the lowest speed storage, and possibly less bandwidth. This is just one example of a host group structure. In your organization you may use a different model, such as one that is based on applications or server role, type of hypervisor, business unit or delegation model.

### To move a host group to another location

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Servers**, and then expand **All Hosts**.

3.  To move a host group to another location in the tree, do any of the following:

    -   Drag the host group that you want to move to its new location in the tree.

    -   Right\-click the host group that you want to move, and then click **Move**. In the **Parent host group** list, click a parent host group, and then click **OK**.

    -   Click the host group that you want to move. On the **Folder** tab, in the **Actions** group, click **Move**. In the **Parent host group** list, click a parent host group, and then click **OK**.

## See Also
[Overview: using host groups in VMM](../Topic/Overview--using-host-groups-in-VMM.md)
[How to configure host group properties in VMM](../Topic/How-to-configure-host-group-properties-in-VMM.md)
[Managing host groups in VMM](../Topic/Managing-host-groups-in-VMM.md)
[Managing hosts and host clusters with VMM](../Topic/Managing-hosts-and-host-clusters-with-VMM.md)
[Managing fabric resources with VMM](../Topic/Managing-fabric-resources-with-VMM.md)

