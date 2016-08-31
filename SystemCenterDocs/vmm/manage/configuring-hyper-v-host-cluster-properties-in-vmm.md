---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  Configuring Hyper V host cluster properties in VMM
ms.technology:  virtual-machine-manager
ms.assetid:  2215b794-d6ac-4c47-b490-21bfc66470da
---

# Configuring Hyper-V host cluster properties in VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

After you add a Hyper-V host cluster to Virtual Machine Manager (VMM), you can view and configure the host cluster properties that are described in the following table. (For information about configuring individual hosts, see the links at the end of this topic.)

|Tab|Settings|
|-------|------------|
|**General**|View the name, host group and description. You can also configure the **Cluster reserve (nodes)** setting, and view the cluster reserve state.<br /><br />The **Cluster reserve (nodes)** setting specifies the number of node failures a cluster must be able to sustain while still supporting all virtual machines deployed on the host cluster. If the cluster cannot withstand the specified number of node failures and still keep all of the virtual machines running, the cluster is placed in an over-committed state. When over-committed, the clustered hosts receive a zero rating during virtual machine placement. An administrator can override the rating and place a highly-available virtual machine on an over-committed cluster during a manual placement.|
|**Status**|View detailed status information for the host cluster:<br /><br />-   Cluster validation test runs and successes. Includes a link to the latest validation report (if available). **Note:**     Accessing the report requires administrative permissions on the cluster node where the report is located. **Tip:**     For host clusters, you can perform an on-demand cluster validation through VMM. To do this, in the **Fabric** workspace, locate and click the host cluster. Then, on the **Host Cluster** tab, click **Validate Cluster**. Cluster validation begins immediately.<br />-   Online elements in the cluster: cluster core resources, disk witness in quorum, and the cluster service on each node.|
|**Available Storage**|Shows available storage, that is, storage logical units that are assigned to the host cluster but are not Cluster Shared Volumes (CSV).<br /><br />You can also do the following:<br /><br />-   Add and remove storage logical units that are managed by VMM.<br />-   Convert available storage to shared storage (CSV).<br /><br />For more information, see [How to configure storage on a Hyper-V host cluster in VMM](How-to-configure-storage-on-a-Hyper-V-host-cluster-in-VMM.md).|
|**Shared Volumes**|Shows the shared volumes (CSVs) that are allocated to the host cluster. You can also do the following:<br /><br />-   Add and remove CSVs that are managed by VMM.<br />-   Convert CSVs to available (non-CSV) storage.<br /><br />For more information, see [How to configure storage on a Hyper-V host cluster in VMM](How-to-configure-storage-on-a-Hyper-V-host-cluster-in-VMM.md).|
|**Custom Properties**|Custom properties that you manage.|

## See Also
[Modifying Hyper-V host clusters in VMM](Modifying-Hyper-V-host-clusters-in-VMM.md)
[Configuring Hyper-V host properties in VMM](Configuring-Hyper-V-host-properties-in-VMM.md)
[Managing Hyper-V hosts and host clusters with VMM](Managing-Hyper-V-hosts-and-host-clusters-with-VMM.md)



