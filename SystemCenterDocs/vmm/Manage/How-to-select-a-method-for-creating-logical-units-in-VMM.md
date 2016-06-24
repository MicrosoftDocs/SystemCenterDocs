---
title: How to select a method for creating logical units in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7926fd47-a33a-46fa-8adb-a797d52f0d20
---
# How to select a method for creating logical units in VMM
You can use the following procedure to configure the preferred capacity allocation method for a managed storage array in Virtual Machine Manager (VMM). This setting defines how new logical units are allocated when you rapid provision virtual machines by using storage area network (SAN) copy technology. You can either create logical units by using the snapshot capability or by using the cloning capability.

> [!NOTE]
> The storage array must support the selected allocation method, and the functionality for the selected method must be enabled on the array. Also, realize that the selected allocation method might require additional licensing from your storage vendor.

### To configure the allocation method for a storage array

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Storage**, and then click **Arrays**.

3.  On the **Home** tab, in the **Show** group, click **Fabric Resources**.

4.  In the **Arrays** pane, right-click the array that you want to configure, and then click **Properties**.

5.  In the **Properties** dialog box, click the **Settings** tab.

6.  Under **Storage array settings**, click one of the following options, and then click **OK**:

    -   **Use snapshots** (the default)

    -   **Clone logical units**

## See Also
[Configuring block storage in VMM](Configuring-block-storage-in-VMM.md)
[Managing storage resources and capacity with VMM](Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


