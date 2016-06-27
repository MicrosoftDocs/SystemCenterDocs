---
title: How to remove a node from a Hyper-V host cluster in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7a309623-f597-4fb5-8bfa-728b50dfb334
---
# How to remove a node from a Hyper-V host cluster in VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

This topic contains procedures for removing one or more nodes from a host cluster that is managed by Virtual Machine Manager (VMM). At the start of the procedure, the cluster must have at least two nodes.

With a host cluster, the host that you remove becomes a stand-alone host managed in VMM.

### To remove a node from a Hyper-V host cluster

1.  Ensure that the node that you want to remove is in maintenance mode:

    1.  In the **Fabric** workspace, expand **Servers** > **All Hosts**.

    2.  Locate and click the cluster node that you want to remove, and view the status in the **Hosts** pane.

    3.  If the node is not already in maintenance mode, right-click it and click **Start Maintenance Mode**. Click **Move all virtual machines to other hosts in the cluster**, and then click **OK**.

    4.  In the **Hosts** pane, verify that the host status is **In Maintenance Mode**.

2.  Right-click the host, and then click **Remove Cluster Node**. When prompted, click **Yes**.

    VMM removes the node from the cluster. Open the **Jobs** workspace to view the job status.

    > [!NOTE]
    > As part of the job, any shared storage that is managed through VMM is unregistered from the node that is being removed. If you are using storage management tools other than VMM for the storage, we recommend that you use those tools to unregister the shared storage from the node.

## See Also
[Modifying Hyper-V host clusters in VMM](Modifying-Hyper-V-host-clusters-in-VMM.md)
[Managing Hyper-V hosts and host clusters with VMM](Managing-Hyper-V-hosts-and-host-clusters-with-VMM.md)
[Managing hosts and host clusters with VMM](Managing-hosts-and-host-clusters-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)



