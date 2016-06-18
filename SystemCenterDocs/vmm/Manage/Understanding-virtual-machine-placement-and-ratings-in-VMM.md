---
title: Understanding virtual machine placement and ratings in VMM
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 810f30d0-45cd-4781-aa4d-ec5cd882f3d6
---
# Understanding virtual machine placement and ratings in VMM
When you deploy or migrate a virtual machine to a host, Virtual Machine Manager \(VMM\) uses virtual machine placement \(also known as intelligent placement\) to evaluate the suitability of available hosts. The placement algorithm analyzes performance data for the workload and the host, and then rates hosts on a scale of one to five stars to indicate the best placement choice. The VMM placement process for a number of deployment scenarios is used as summarized in the following table.

|Deployment scenario|Details|
|-----------------------|-----------|
|Create a new virtual machine from a disk, existing virtual machine, or template.|When you create a new virtual machine the host rating is used to offer suggestions for selecting a host.<br /><br />If a self\-service user creates a virtual machine, or you use drag\-and\-drop to move a virtual machine to a host group, the host will be assigned automatically by VMM, based on the highest rating.|
|Convert a non\-Hyper\-V virtual machine|The conversion wizards provide ratings for hosts so that you can select the most appropriate host.|
|Migrate a virtual machine|During migration \(offline, quick migration, live migration\), VMM provides host ratings to help you select appropriate hosts.|

This topic includes the following sections:

-   [Choices you can make during placement](#BKMK_Choice)

-   [Calculating host ratings](#BKMK_Rating)

## <a name="BKMK_Choice"></a>Choices you can make during placement
Placement in VMM includes the following:

-   VMM displays hosts as they are rated, and you can select a suitable host before host rating is complete.

-   Placement on clusters includes the following choices:

    -   **Preferred owners:** You can specify preferred host owners for the virtual machine. This property is a Failover Cluster Manager setting which is used at the time of failover. When a virtual machine needs to be failed over, VMM tries to use the preferred owners first.

    -   **Possible owners:** This feature allows you to specify possible host owners for a virtual machine.  If a host is not included in the possible owners, both VMM and Failover Cluster Manager will not allow the virtual machine to be placed on that host.

    -   : This feature allows you to identify virtual machines that should be kept on separate hosts. If you create an availability set, automatic placement will place virtual machines in line with availability set settings.

-   If you use storage classifications, clouds can be scoped to restrict virtual machine deployment to specific storage classifications only.

## <a name="BKMK_Rating"></a>Calculating host ratings
VMM evaluates all hosts within a selected host group and any hosts contained in child host groups. Host ratings are calculated on a scale from 0 to 5 stars, where 5 stars indicate the highest rating. The ratings are based on default criteria. Note that host rating criteria do not include all information. For example, network connection speed is not taken into account. Ratings are based on individual hosts and not on the relative suitability of all available hosts. Ratings for one host do not change based on the ratings for other hosts. VMM calculates host ratings according to specific formulas, described in the following table.

|Rating|Formula|
|----------|-----------|
|CPU|\[ 1 – \( CPU Utilization \/ \(100 – CPU Reserve\)\) \] x CPU Weight|
|Memory \(RAM\)|\[ 1 – \( Memory Used \/ \(Total Memory – Memory Reserve\)\) \] x Memory Weight|
|Disk I\/O capacity|\[ 1 – \( Disk IOPS \/ Maximum Disk IOPS \] x Disk Weight|
|Network|\[ 1 – \( Network Utilization \/ \(100 – Network Reserve\)\) \] x Network Weight|

A host is rated only when a virtual machine needs to be placed. The information gathered about a host is compared to the information about the resources required by the virtual machine, and a rating is assigned to the host. During automatic placement, VMM attempts to use the host assigned the highest rating. During manual placement the host rating is shown so that you can select the appropriate host. You can select a host in VMM even if not all hosts have been rated. The selected host must have a positive number of stars.

VMM measures CPU, memory, disk, and network usage approximately every 10 minutes to recalculate an average rating that is an average of all the measurements taken that the last action that reset the host rating. Host ratings are reset when the following happens:

-   A new virtual machine is created

-   A virtual machine is deployed, stored, migrated or deleted

-   A virtual machine is turned on, off, or moved into a stopped, paused, or saved state.

### Zero and non\-zero ratings
A host can receive a non\-zero rating only if it meets the following criteria:

-   The host must have at least one hard disk with enough storage to hold the total hard disk space required by the virtual machine. With dynamic hard disks, the current hard disk size is used, not the maximum hard disk size.

-   On a host group or cloud, you can decide whether to limit the placement of virtual machines to stay within the aggregate capacity of that host group or cloud. For non\-replica virtual machines, it is a best practice to stay within the aggregate capacity. If you have replica virtual machines, you might want to exceed the specified capacity of a preconfigured cloud or host group. In other words, you might want to overcommit the cloud or host group as you place replica virtual machines.

    For example, on a cloud where the **Memory** setting for **Total Capacity** is 32 GB, you could uncheck the **Use Maximum** box and set the **Assigned Capacity** to 64. After that, if you were placing replica virtual machines, you could choose that cloud as a placement option even if the aggregate load was greater than 32 GB \(and less than 64 GB\).

-   If dynamic memory is enabled, note the following:

    -   If the virtual machine \(including any one of its checkpoints\) is configured to use Dynamic Memory, the host should also have Dynamic Memory enabled. If it does not, the placement of the virtual machine will be blocked during creation or migration.

    -   For placement of a new or stopped virtual machine, the host must meet at least the startup memory requirement for the virtual machine.

    -   For placement of a running virtual machine, the host must meet at least the current memory requirement for the virtual machine.

    -   For placement of a virtual machine in a saved state, the last known memory usage value of the virtual machine will be compared to the startup memory of the virtual machine.

-   The host must contain all of the virtual networks required for the virtual machine. If you use network tags, the network location tags for the virtual machine and host must be identical.

-   The host cannot be in maintenance mode. A host in maintenance mode automatically receives a zero rating.

-   If Microsoft RemoteFX 3D video adapter is enabled on the virtual machine, note the following conditions. If these conditions are not met placement is blocked during creation or migration of the virtual machine:

    -   The host must support RemoteFX.

    -   The host must have one or more RemoteFX\-capable graphics processing units \(GPUs\) with sufficient available memory. If the virtual machine is running placement will be blocked. If it is stopped or in a saved state a zero rating with a warning will be issued, but placement will not be blocked.

-   Highly available virtual machines must be placed on clustered hosts. VMM assigns zero stars to hosts that are not clustered but manual placement is not blocked. If you migrate a highly\-available virtual machine to a non\-clustered host, the virtual machine will no longer be highly available after the migration.

-   VMM blocks migration of Hyper\-V hosts to hosts running different virtualization software. Migration of a virtual machine with specific features not allowed by the virtualization software that is running on a host will be blocked. For example, Hyper\-V hosts do not allow booting up from a SCSI hard disk.

## See Also
[Creating and deploying virtual machines in VMM](Creating-and-deploying-virtual-machines-in-VMM.md)
[Managing virtual machines with VMM](Managing-virtual-machines-with-VMM.md)
[Managing tenant resources with VMM](Managing-tenant-resources-with-VMM.md)


