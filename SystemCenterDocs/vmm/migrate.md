---
ms.assetid: f6301c37-5e3d-449c-adde-952fdd2b7fee
title: Migrate virtual machines in the VMM fabric
description: This article describes how to migrate VMs in the VMM fabric
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.topic: concept-article
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: intro-migration, engagement-fy24
---


# Migration of virtual machines – overview



This article provides an overview of migrating virtual machines in the System Center Virtual Machine Manager (VMM) fabric.

You can migrate virtual machines and storage managed VMs in the VMM fabric. VMM automatically selects the type of transfer that will be used for migration. When you perform a migration in the VMM console using the Migrate VM Wizard, the migration type that will be used is displayed in the **Transfer Type** column. The types of migrations supported are summarized in the following table.

**Type** | **Use** | **Details**
--- | --- | ---
**Network migration** | Performs a network copy of the virtual machine data using BITS. |  This is the slowest type of migration. The amount of downtime is in direct proportion to the size of the data transfer.
 **Quick migration** | Also known as cluster transfer, it can be used to migrate a highly available virtual machine. It uses Windows Failover Cluster to migrate virtual machines between cluster nodes. | The running state of the virtual machine is saved to disk (the virtual machine is hibernated), the disk is failed over to the other cluster node, and then the saved state is loaded to wake up the virtual machine.<br/><br/>  Downtime is minimal because quick migration takes a snapshot of the virtual machine, and transfers data without requiring the virtual machine to be turned off.
**Quick storage migration** | Used to move VM storage from one location to another. For example, you can move the storage for a virtual machine from a Fibre Channel SAN to an iSCSI SAN. | The virtual disks of a running virtual machine can be migrated independent of the storage protocols (SCSI, Fibre Channel) or storage types (local, DAS, SAN).<br/><br/> Downtime is minimal because quick storage migration takes a snapshot of the virtual machine and transfers data without requiring the virtual machine to be turned off.
**SAN migration** | Uses SAN transfer to migrate virtual machines and highly available virtual machines in and out of a cluster. It can be used when both the source and destination hosts have access to the same storage infrastructure (LUN), and the storage can be transferred from one host to another. | For SAN migration, the files for a virtual machine aren't copied from one server to another and thus downtime is minimized. SAN migration can be used to copy a virtual machine from one host to another or copying a virtual machine to or from the library.<br/><br/> When you migrate a virtual machine into a cluster using a SAN transfer, VMM checks that each node in the cluster can see the LUN, and automatically creates a cluster disk resource for the LUN.<br/><br/> To migrate a virtual machine out of a cluster, the virtual machine must be on a dedicated LUN that isn't using CSV.<br/><br/> These SAN infrastructures are supported for migration: Fiber Channel; iSCSI SANs; N_Port ID Virtualization (NPID).
**Live migration** | Moves a virtual machine running as part of a failover cluster from one cluster to another. |  No noticeable downtime for users or network applications.

## Live migration

Using live migration provides many benefits:

-   **Increased flexibility**: Live migration features can help simplify the movement of virtual machines across hosts and clusters. Therefore, it becomes easier to manage a dynamic datacenter.
-   **Ease-of-maintenance**: Live migration alleviates the need to take standalone hosts and cluster hosts offline for maintenance and migration purposes, which helps to avoid downtime. With the ability to perform concurrent migrations and maintenance, migration timeframes can become shorter, depending on the time that is required to perform the live migration. In addition, the planning process for Hyper-V mobility is simplified.
-   **Better hardware utilization**: The distribution of virtual machines can be optimized across the infrastructure. Virtual machines and storage can be moved to standalone servers and clusters with spare capacity, without interrupting availability. Power consumption is reduced as virtual machines can be moved across hosts, and then hosts can be powered down to save energy.
:::moniker range=">=sc-vmm-2016 <=sc-vmm-2019"
-   **Failover clustering features**: VMM takes advantage of failover clustering features that were introduced in Windows Server 2012. These features include additional APIs to migrate virtual machines across cluster nodes, and improved attach/detach functionality that enables migration of virtual machines in and out of failover clusters without downtime.
:::moniker-end
:::moniker range=">=sc-vmm-2022"
-   **Failover clustering features**: VMM takes advantage of Windows Server failover clustering features. These features include additional APIs to migrate virtual machines across cluster nodes, and improved attach/detach functionality that enables migration of virtual machines in and out of failover clusters without downtime.
:::moniker-end

### Live migration support

VMM supports the following types of live migration:

- **Live migration of standalone machines**: You can run live migration between two standalone machines that aren't in a cluster.
- **Live migration within a cluster**: You can run a live migration between nodes in the same cluster.
- **Live migration between nodes in different clusters**: You can migrate between nodes in different clusters.
- **Live migration of VM storage**: You can migrate storage to update the physical storage available in Hyper-V or to mitigate bottlenecks in storage performance. You can also use storage migration to move, service, or upgrade storage resources, or for migration of a standalone or cluster virtual machine. Storage can be added to either a standalone computer or to a Hyper-V cluster. VMs can be moved to the new storage while they continue to run.
- **Live Virtual machine and storage migration**: You can use live system migration (live VSM) to migrate virtual machines and their storage together in a single action.
- **Concurrent live migration**: You can perform multiple concurrent live migrations of virtual machines and storage. The concurrent limit can be configured manually. Any concurrent live migrations exceeding of the limit will be queued.

VMM inspects and validates the configuration settings of a destination host before migration from a source host begins.

### Live VM migration support matrix

**Source** | **Destination: Standalone** | **Destination: Cluster**
--- | --- | ---
Standalone | Supported  |Supported|
Cluster | Supported | Supported<br/><br/> Source and destination can be in the same or different clusters.|

### Live storage migration support matrix

**Source** | **Destination: Local disk (standalone)** | **Destination: SMB 3.0 share (standalone/cluster)** | **Destination: CSV (cluster)**
--- | --- | --- | ---
Local disk | Supported | Supported.<br/><br/> The virtual machine will be promoted to high availability. | Not supported.
SMB 3.0 share |Supported. In a cluster, the VM will be demoted and won't be highly available after migration. | Supported | Supported
Cluster | Supported<br/><br/> In a cluster, the VM will be demoted and won't be highly available after migration. | Supported<br/><br/> The SMB share must be available from the destination cluster node. | Supported</br><br/> The CSV must be available from the destination cluster node.

### Live migration limitations

- Live migration requires two or more servers that run Hyper-V, that support hardware virtualization, and use processors from the same manufacturer, such as all AMD processors or all Intel processors.
:::moniker range=">=sc-vmm-2016 <=sc-vmm-2019"
- Live migration is supported starting with hosts running Windows Server 2012.
:::moniker-end
- Virtual machines must be configured to use virtual hard disks or virtual Fibre Channel disks, not physical disks.

- For live migration network traffic, you must use a private network.

- Source and destination servers must belong to the same Active Directory domain or to different trusted domains.

- If the source or destination virtual machine VHD has a base disk, the base disk must be in a share that is accessible (registered) from the destination host. Generally, live migration doesn't move the base disk.

- Migration between clusters is only supported on hosts running in failover clusters. Cluster Shared Volume (CSV) storage must be enabled in the cluster.

- Live migration of a virtual machine doesn't migrate virtual machine storage, specifically meaning the location that stores the virtual machine images (VHD, ISO, VFD files). To handle storage requirements, you can use one of the following options:

    - Configure the virtual machine so that the storage files are available on a file share that is accessible by both the source and destination host of the migration.
    - Run a combined live virtual machine and storage migration (live VSM) in a single action.
    - Run a separate storage migration.

-   If the source and destination hosts use shared storage, ensure the following:

    -   All files that comprise a virtual machine, such as virtual hard disks, snapshots, and configuration, must be stored on an SMB share.
    -   Permissions on the SMB share must be configured to grant access to the computer accounts of all servers that run Hyper-V.

- A storage migration moves virtual machine images (VHD, ISO, and VFD files), snapshot configurations, and data (saved state files).
- Storage migration is per virtual machine.
- Storage migration doesn't move base (parent) disks, except for snapshot disks.

### Live Virtual machine and storage migration (Live VSM)

Live VSM migrates a VM and its machine storage in a single action.

- To use live VSM, the virtual machine LUN must be masked from the destination host.
:::moniker range=">=sc-vmm-2016 <=sc-vmm-2019"
- Live VSM is supported between two standalone hosts that run Hyper-V, starting with Windows Server 2012. The transfer can occur between local disks or SMB 3.0 file shares.

- Live VSM is supported between two host clusters that run Hyper-V, starting with Windows Server 2012. The virtual machine can be transferred to either a CSV or SMB 3.0 file share on the destination host cluster.
:::moniker-end
:::moniker range=">=sc-vmm-2022"
- Live VSM is supported between two standalone hosts that run Hyper-V. The transfer can occur between local disks or SMB 3.0 file shares.

- Live VSM is supported between two host clusters that run Hyper-V. The virtual machine can be transferred to either a CSV or SMB 3.0 file share on the destination host cluster.
:::moniker-end

## Next steps

- [Migrate a virtual machine](migrate-vm.md).
- [Migrate storage](migrate-storage.md).
- [Run a live migration](migrate-live.md).
