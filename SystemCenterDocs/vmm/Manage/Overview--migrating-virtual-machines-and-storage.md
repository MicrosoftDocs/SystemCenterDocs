---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  Overview  migrating virtual machines and storage
ms.technology:  virtual-machine-manager
ms.assetid:  475c98de-5ea0-49f4-b739-adb6c1746ffd
---

# Overview: migrating virtual machines and storage

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

Virtual Machine Manager (VMM) supports the following types of migration:

-   **Network migration**�This is the slowest type of migration and performs a network copy of the virtual machine data using BITS. The amount of downtime is in direct proportion to the size of the data transfer.

-   **Quick migration**�This type of migration is also known as cluster transfer, and can be used to migrate a highly available virtual machine. It leverages Windows Failover Cluster to migrate virtual machines between cluster nodes. The running state of the virtual machine is saved to disk (the virtual machine is hibernated), the disk is failed over to the other cluster node, and then the saved state is loaded to wake up the virtual machine.  Downtime is minimal because quick migration takes a snapshot of the virtual machine and transfers data without requiring the virtual machine to be turned off.

-   **Quick storage migration**�Quick storage migration allows you to move virtual machine storage from one location to another. For example, you can move the storage for a virtual machine from a Fibre Channel SAN to an iSCSI SAN. The virtual disks of a running virtual machine can be migrated independent of storage protocols (SCSI, Fibre Channel) or storage types (local, DAS, SAN). Downtime is minimal because quick storage migration takes a snapshot of the virtual machine and transfers data without requiring the virtual machine to be turned off.

-   **SAN migration**�This type of migration uses SAN transfer to migrate virtual machines, and highly available virtual machines, into and out of a cluster. It can be used when both the source and destination hosts have access to the same storage infrastructure (LUN), and the storage can be transferred from one host to another. For SAN migration, the files for a virtual machine are not copied from one server to another and thus downtime is minimized. SAN migration can be used to copy a virtual machine from one host to another, or copying a virtual machine to or from the library. Note the following:

    1.  When you migrate a virtual machine into a cluster by using a SAN transfer, VMM checks that each node in the cluster can see the LUN, and automatically creates a cluster disk resource for the LUN.

    2.  To migrate a virtual machine out of a cluster, the virtual machine must be on a dedicated LUN that is not using CSV.

    3.  The following SAN infrastructures are supported for migration: Fiber Channel; iSCSI SANs; N_Port ID Virtualization (NPID).

-   **Live migration**�This type of migration moves a virtual machine running as part of a failover cluster from one cluster to another with no noticeable downtime for users or network applications.

VMM automatically selects the type of transfer that will be used for migration. When you perform a migration in the VMM console using the Migrate VM Wizard, the migration type that will be used is displayed in the Transfer Type column.

## Live migration features
VMM provides a number of live migration features based on migration capabilities introduced in Windows Server 2012. These features include:

-   Live migration outside a cluster�In addition to performing live migration within a cluster, you can perform live migration between two standalone computers that are not cluster nodes.

-   Live migration between nodes in two different clusters� You can migrate between nodes within a cluster, or between nodes in different clusters.

-   Live migration of virtual machine storage �You can migrate storage in order to update the physical storage that is available in Hyper-V, or to mitigate bottlenecks in storage performance. Storage can be added to either a stand-alone computer or to a Hyper-V cluster, and then virtual machines can be moved to the new storage while they continue to run.

-   Live VSM�By using live system migration (live VSM), you can migrate virtual machines and their storage together in a single action.

-   Concurrent live migration� You can perform multiple concurrent live migrations of virtual machines and storage. The concurrent limit can be configured manually. Any concurrent live migrations in excess of the limit will be queued.

VMM inspects and validates the configuration settings of a destination host before migration from a source host begins.

### Business benefits
The live migration features provide a number of business benefits:

-   **Increased flexibility**�Live migration features can help to simplify the movement of virtual machines across hosts and clusters. Therefore, it becomes easier to manage a dynamic datacenter.

-   **Ease-of-maintenance**�Live migration alleviates the need to take standalone hosts and cluster hosts offline for maintenance and migration purposes, which helps to avoid downtime. With the ability to perform concurrent migrations and maintenance, migration timeframes can become shorter, depending on the time that is required to perform the live migration. In addition, the planning process for Hyper-V mobility is simplified.

-   **Better hardware utilization**�The distribution of virtual machines can be optimized across the infrastructure. Virtual machines and storage can be moved to stand-alone servers and clusters with spare capacity, without interrupting availability. Power consumption is reduced as virtual machines can be moved across hosts, and then hosts can be powered down to save energy.

-   **Failover clustering features**�VMM takes advantage of failover clustering features that were introduced in Windows Server 2012. These features include additional APIs to migrate virtual machines across cluster nodes, and improved attach/detach functionality that enables migration of virtual machines in and out of failover clusters without downtime.

### Virtual machine live migration support
The following table summarizes the support matrix for live migration of virtual machines.

|Source|Destination|
|----------|---------------|
||**Destination: Stand-alone**|**Destination: Cluster node**|
|**Source: Stand-alone**|Supported|Supported|
|**Source: Cluster node**|Supported|Supported. Source and destination can be in the same cluster or in different clusters.|

### Live storage migration
With virtual machine storage migration, you can move storage from one location to another without interrupting the workload of the virtual machine, if it is running. You can also use storage migration to move, service, or upgrade storage resources, or for migration of a standalone or cluster virtual machine. The following table summarizes the support matrix for storage migration.

|Source|Destination|
|----------|---------------|
||**Destination: Local disk (stand-alone)**|**Destination: SMB 3.0 share (standalone or cluster)**|**Destination: CSV (cluster)**|
|**Source: Local disk (stand-alone)**|Supported|Supported. The virtual machine will be promoted to high availability.|Not supported.|
|**Source: SMB 3.0 share**|Supported. In a cluster configuration the virtual machine will be demoted, and will no longer be highly available after migration to the local disk.|Supported|Supported|
|**Source: CSV (cluster)**|In a cluster configuration the virtual machine will be demoted, and will no longer be highly available after migration to the local disk.|Supported. The SMB share must be available from the destination cluster node.|Supported. CSV must be available from the destination cluster node.|

### Live migration limitations
Note the following requirements and limitations when performing a live migration of virtual machines and storage:

-   Live migration requires two or more servers that run Hyper-V, that support hardware virtualization, and use processors from the same manufacturer, such as all AMD processors or all Intel processors, for example.

-   Live migration is supported starting with hosts running Windows Server 2012. There is no backward compatibility to support migration between hosts that run Windows Server 2008 R2 and Windows Server 2012.

-   Virtual machines must be configured to use virtual hard disks or virtual Fibre Channel disks, not physical disks.

-   For live migration network traffic you should use a private network.

-   Source and destination servers must belong to the same Active Directory domain, or to different trusted domains.

-   If the source or destination virtual machine VHD has a base disk, the base disk must be in a share that is accessible (registered) from the destination host. Generally, live migration does not move the base disk.

-   Migration between clusters is only supported on hosts running in failover clusters. Cluster Shared Volume (CSV) storage should be enabled in the cluster.

-   Live migration of a virtual machine does not migrate virtual machine storage, specifically meaning the location that stores the virtual machine images (VHD, ISO, VFD files). To handle storage requirements, you can use one of the following options:

    -   Configure the virtual machine so that the storage files are available on a file share that is accessible by both the source and destination host of the migration.

    -   Run a combined live virtual machine and storage migration (live VSM) in a single action.

    -   Run a separate storage migration.

-   If the source and destination hosts use shared storage, note the following:

    -   All files that comprise a virtual machine, such as virtual hard disks, snapshots, and configuration, should be stored on an SMB share.

    -   Permissions on the SMB share should be configured to grant access to the computer accounts of all servers that run Hyper-V.

-   A storage migration moves virtual machine images (VHD, ISO, and VFD files), snapshot configurations, and data (saved state files).

-   Storage migration is per virtual machine.

-   Storage migration does not move base (parent) disks, with the exception of snapshot disks.

### Live virtual machine and storage migration (live VSM)
You can perform a live VSM to migrate both a virtual machine, and the virtual machine storage in a single action.

-   To use live VSM, the virtual machine LUN must be masked from the destination host.

-   Live VSM is supported between two stand-alone hosts that run Hyper-V, starting with Windows Server 2012. The transfer can occur between local disks or SMB 3.0 file shares.

-   Live VSM is supported between two host clusters that run Hyper-V, starting with Windows Server 2012. The virtual machine can be transferred to either a CSV or SMB 3.0 file share on the destination host cluster.





