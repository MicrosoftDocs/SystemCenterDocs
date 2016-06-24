---
title: How to uncluster a Hyper-V host cluster in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 40844392-4a5e-4b27-9ef1-06c4b4ccaa4f
---
# How to uncluster a Hyper-V host cluster in VMM
You can use the following procedures to uncluster or remove a host cluster that is being managed in Virtual Machine Manager (VMM).

### To uncluster a Hyper-V host cluster

1.  Open the **Fabric** workspace.

2.  In the **Fabric** pane, expand **Servers** > **All Hosts**.

3.  Make sure that the host cluster is not supporting any highly-available virtual machines or any other clustered services or applications.

4.  Locate and right-click the host cluster, and then click **Uncluster**.

5.  Review the warning message, and then click **Yes** to continue.

6.  Open the **Jobs** workspace to monitor the job status.

    When the job is completed, the hosts appear as stand-alone hosts in the **Fabric** workspace.

    > [!NOTE]
    > As part of the job, VMM unregisters the shared storage that is managed through VMM from the cluster nodes. If the cluster had shared storage assigned that was not managed by VMM, we recommend that you unregister the shared storage by using your storage array vendor’s management tools.

## See Also
[Modifying Hyper-V host clusters in VMM](Modifying-Hyper-V-host-clusters-in-VMM.md)
[Managing Hyper-V hosts and host clusters with VMM](Managing-Hyper-V-hosts-and-host-clusters-with-VMM.md)
[Managing hosts and host clusters with VMM](Managing-hosts-and-host-clusters-with-VMM.md)
[Managing fabric resources with VMM](Managing-fabric-resources-with-VMM.md)


