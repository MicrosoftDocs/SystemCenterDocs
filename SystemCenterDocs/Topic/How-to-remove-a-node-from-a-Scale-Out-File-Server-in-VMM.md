---
title: How to remove a node from a Scale-Out File Server in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 87ba7da6-b80d-431b-90e6-c11b25c84bcb
---
# How to remove a node from a Scale-Out File Server in VMM
This topic contains procedures for removing one or more nodes from a Scale\-Out File Server that is managed by [!INCLUDE[vmm12sp1_long](../Token/vmm12sp1_long_md.md)]. At the start of the procedure, the Scale\-Out File Server must have at least two nodes.

### To remove a node from a Scale\-Out File Server

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Storage** > **File Servers**.

3.  In the **File Servers** pane, right\-click the Scale\-Out File Server cluster, and then click **Properties**.

4.  Click the **Cluster Nodes** tab. In the **File server nodes** list, select the nodes that you want to remove, and click **Remove**.

5.  Open the **Jobs** workspace to view the job status. To verify that [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] removed the node from the cluster, in the [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] console, make sure that it is no longer listed as part of the file server.

    > [!NOTE]
    > A file server cluster can have storage logical units from a storage area network \(SAN\) unmasked to it. When you remove a node from the cluster, [!INCLUDE[vmm12short](../Token/vmm12short_md.md)] does not mask such storage. If the array is managed by [!INCLUDE[vmm12short](../Token/vmm12short_md.md)], you can open the **Properties** dialog box of the storage logical unit, and mask storage as necessary. If it is not managed by [!INCLUDE[vmm12short](../Token/vmm12short_md.md)], use your storage vendor's management tools.

## See Also
[Modifying Scale-Out File Servers in VMM](../Topic/Modifying-Scale-Out-File-Servers-in-VMM.md)
[Managing Scale-Out File Servers with VMM](../Topic/Managing-Scale-Out-File-Servers-with-VMM.md)
[Managing storage resources and capacity with VMM](../Topic/Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](../Topic/Managing-fabric-resources-with-VMM.md)

