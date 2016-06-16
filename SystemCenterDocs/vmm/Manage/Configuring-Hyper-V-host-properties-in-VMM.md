---
title: Configuring Hyper-V host properties in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d1fd2d69-d9c6-4e40-9ffe-bd3723a2f5ac
---
# Configuring Hyper-V host properties in VMM
After you've added Hyper-V hosts and servers in the VMM fabric there are a number of properties you can configure for standalone hosts and clusters. 

## Properties for Hyper-V hosts

|Tab|Settings|
|-------|------------|
|**General**|-   View identity and system information for the host. This includes information such as processor information, total and available memory and storage, the operating system, the type of hypervisor, and the [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] agent version.<br />-   Enter a host description.<br />-   Configure whether the host is available for placement.<br />-   Configure the remote connection port. By default, the port is set to 2179.|
|**Hardware**|View or modify settings for CPU, memory, graphics processing units \(GPUs\), storage \(including whether the storage is available for placement\), network adapters, DVD\/CD\-ROM drives and Baseboard Management Controller \(BMC\) settings.
|**Status**|Lists health status information for the host. Includes areas such as overall health, Hyper\-V role health and [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] agent health. In the **Status** pane, you can also do the following:<br /><br />-   View error details.<br />-   Refresh the health status.<br />-   Click **Repair all**. [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)] will try to automatically fix any errors.|
|**Virtual Machine Paths**\/**Virtual Machines**|Shows the virtual machines that reside on the host, together with status information. Also enables you to register virtual machines on the host.|
|**Reserves**|Enables you to override host reserve settings from the parent host group, and configure reserved resources for the host. Configurable resources include CPU, memory, disk space, disk I\/O and network capacity.|
|**Storage**|Shows storage allocated to a host, and enables you to add and remove storage logical units or file shares. |
|**Virtual Switches**|Enables you to configure virtual switches. |
|**Placement Paths**\/**Placement**|Enables you to configure the default virtual machine paths and default parent disk paths that will be used during virtual machine placement on the host.|
|**Servicing Windows**|Enables you to select servicing windows.|
|**Custom Properties**|Enables you to assign and manage custom properties.|

## Properties for Hyper-V clusters

|Tab|Settings|
|-------|------------|
|**General**|View the name, host group and description. You can also configure the **Cluster reserve \(nodes\)** setting, and view the cluster reserve state.<br /><br />The **Cluster reserve \(nodes\)** setting specifies the number of node failures a cluster must be able to sustain while still supporting all virtual machines deployed on the host cluster. If the cluster cannot withstand the specified number of node failures and still keep all of the virtual machines running, the cluster is placed in an over\-committed state. When over\-committed, the clustered hosts receive a zero rating during virtual machine placement. An administrator can override the rating and place a highly\-available virtual machine on an over\-committed cluster during a manual placement.|
|**Status**|View detailed status information for the host cluster:<br /><br />-   Cluster validation test runs and successes. Includes a link to the latest validation report \(if available\). **Note:**     Accessing the report requires administrative permissions on the cluster node where the report is located. **Tip:**     For host clusters, you can perform an on\-demand cluster validation through [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)]. To do this, in the **Fabric** workspace, locate and click the host cluster. Then, on the **Host Cluster** tab, click **Validate Cluster**. Cluster validation begins immediately.<br />-   Online elements in the cluster: cluster core resources, disk witness in quorum, and the cluster service on each node.|
|**Available Storage**|Shows available storage, that is, storage logical units that are assigned to the host cluster but are not Cluster Shared Volumes \(CSV\).<br /><br />You can also do the following:<br /><br />-   Add and remove storage logical units that are managed by [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)].<br />-   Convert available storage to shared storage \(CSV\).|
|**Shared Volumes**|Shows the shared volumes \(CSVs\) that are allocated to the host cluster. You can also do the following:<br /><br />-   Add and remove CSVs that are managed by [!INCLUDE[vmm12short](../../includes/vmm12short_md.md)].<br />-   Convert CSVs to available \(non\-CSV\) storage.|
|**Custom Properties**|Custom properties that you manage.|


