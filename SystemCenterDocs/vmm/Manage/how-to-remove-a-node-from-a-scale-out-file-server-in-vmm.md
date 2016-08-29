---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  How to remove a node from a Scale Out File Server in VMM
ms.technology:  virtual-machine-manager
ms.assetid:  87ba7da6-b80d-431b-90e6-c11b25c84bcb
---

# How to remove a node from a Scale-Out File Server in VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

This topic contains procedures for removing one or more nodes from a Scale-Out File Server that is managed by Virtual Machine Manager (VMM). At the start of the procedure, the Scale-Out File Server must have at least two nodes.

### To remove a node from a Scale-Out File Server

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Storage** > **File Servers**.

3.  In the **File Servers** pane, right-click the Scale-Out File Server cluster, and then click **Properties**.

4.  Click the **Cluster Nodes** tab. In the **File server nodes** list, select the nodes that you want to remove, and click **Remove**.

5.  Open the **Jobs** workspace to view the job status. To verify that VMM removed the node from the cluster, in the VMM console, make sure that it is no longer listed as part of the file server.

    > [!NOTE]
    > A file server cluster can have storage logical units from a storage area network (SAN) unmasked to it. When you remove a node from the cluster, VMM does not mask such storage. If the array is managed by VMM, you can open the **Properties** dialog box of the storage logical unit, and mask storage as necessary. If it is not managed by VMM, use your storage vendor's management tools.

## See Also
[Modifying Scale-Out File Servers in VMM](Modifying-Scale-Out-File-Servers-in-VMM.md)
[Managing Scale-Out File Servers with VMM](Managing-Scale-Out-File-Servers-with-VMM.md)
[Managing storage resources and capacity with VMM](Managing-storage-resources-and-capacity-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)



