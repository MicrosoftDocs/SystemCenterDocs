---
title: Overview: configuring storage using Scale-Out File Servers in VMM
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - virtual-machine-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45c93144-4ae6-41e1-874e-4216c5f4a2de
---
# Overview: configuring storage using Scale-Out File Servers in VMM
This overview describes the process for using Virtual Machine Manager (VMM) to configure storage based on Scale-Out File Server clusters. This process is similar whether your Scale-Out File Server cluster uses shared storage or the newer option, Storage Spaces Direct. Storage Spaces direct uses local storage, as described in[Storage Spaces Direct in Windows Server Technical Preview](https://technet.microsoft.com/library/mt126109.aspx). For Storage Spaces Direct, the cluster nodes must run Windows Server Technical Preview.

If you don't want overview information, and instead want a list of step-by-step procedures, see [Configuring storage using Scale-Out File Servers in VMM](Configuring-storage-using-Scale-Out-File-Servers-in-VMM.md).

To configure storage, work through these stages:

-   [Stage 1: Discover storage during creation or addition of your Scale-Out File Server](Overview--configuring-storage-using-Scale-Out-File-Servers-in-VMM.md#BKMK_discovery)

-   [Stage 2: Plan your storage classifications](Overview--configuring-storage-using-Scale-Out-File-Servers-in-VMM.md#BKMK_classifications)

-   [Stage 3: Create storage pools (in storage spaces)](Overview--configuring-storage-using-Scale-Out-File-Servers-in-VMM.md#BKMK_pools)

-   [Stage 4: Create file shares](Overview--configuring-storage-using-Scale-Out-File-Servers-in-VMM.md#BKMK_shares)

-   [Stage 5: Assign permissions so hosts can access file shares](Overview--configuring-storage-using-Scale-Out-File-Servers-in-VMM.md#BKMK_permissions)

-   [Stage 6: Make classified storage available to users of templates or private clouds](Overview--configuring-storage-using-Scale-Out-File-Servers-in-VMM.md#BKMK_templates)

-   [Stage 7: Understand how VMM evaluates placement options](Overview--configuring-storage-using-Scale-Out-File-Servers-in-VMM.md#BKMK_vhds)

-   [Stage 8: Understand how VMM copies virtual hard disk files to file shares](Overview--configuring-storage-using-Scale-Out-File-Servers-in-VMM.md#BKMK_copying)

-   [Stage 9: If needed, add nodes to the Scale-Out File Server](Overview--configuring-storage-using-Scale-Out-File-Servers-in-VMM.md#BKMK_add)

## <a name="BKMK_discovery"></a>Stage 1: Discover storage during creation or addition of your Scale-Out File Server
**What you do**: At this stage, you add or create a Scale-Out File Server in one of these ways:

-   **Add**: [How to add an existing Scale-Out File Server to storage in VMM](How-to-add-an-existing-Scale-Out-File-Server-to-storage-in-VMM.md)

-   **Create from existing**: [Creating a host cluster in VMM from existing Windows servers](Creating-a-host-cluster-in-VMM-from-existing-Windows-servers.md)

-   **Bare metal**: [Deploying Hyper-V hosts or host clusters from bare metal with VMM](Deploying-Hyper-V-hosts-or-host-clusters-from-bare-metal-with-VMM.md) (for an overview of this process, see [Overview: creating hosts or host clusters from bare metal with VMM](Overview--creating-hosts-or-host-clusters-from-bare-metal-with-VMM.md))

If you need to specify a disk witness, see [How to set a disk witness for a Scale-Out File Server quorum in VMM](How-to-set-a-disk-witness-for-a-Scale-Out-File-Server-quorum-in-VMM.md).

**How VMM responds**: Through the Storage Spaces provider on the Scale-Out File Server,  VMM discovers the storage. VMM discovers all physical disks that are managed within the cluster, and any storage pools and file shares that are already configured.

## <a name="BKMK_classifications"></a>Stage 2: Plan your storage classifications
**What you do**: In VMM, to simplify the assignment of storage to users and virtual machines, you can create and use *storage classifications* that fit your environment. You can create classifications in the midst of the process, for example, when you're running a wizard such as the New Storage Pool Wizard. Or you can create the storage classification as a separate action: in the **Fabric** workspace, click **Create Storage Classification**.

For example, you could plan to create these classifications:

-   **Bldg1Gold**: A set of solid-state drives (SSDs) that you will make available to users in building 1.

-   **Bldg1Silver**: A set of SSDs and hard disk drives (HDDs) that you will make available to users in building 1.

-   **Bldg2Gold**: A set of SSDs that you will make available to users in building 2.

-   **Bldg2Silver**: A set of SSDs and HDDs that you will make available to users in building 2.

After you plan your classifications, you will know which classification to assign to each of your storage pools. When you create file shares in a pool, they inherit the pool's classification, but you can adjust file share classifications individually, if needed.

Later, you can use these classifications to provide the classified storage to a particular set of virtual machines or cloud users, avoiding the need to assign each individual unit of storage (such as a storage pool or a share) manually. This is described in [Stage 6: Make classified storage available to users of templates or private clouds](Overview--configuring-storage-using-Scale-Out-File-Servers-in-VMM.md#BKMK_templates), later in this topic.

**How VMM responds**: As you proceed with configuring your storage, VMM keeps track of the classification in which you place each unit of storage (for example, a storage pool, or an individual file share). Later, when users are creating virtual machines using templates or a private cloud, VMM will place the virtual hard disks according to the classifications that you have configured.

## <a name="BKMK_pools"></a>Stage 3: Create storage pools (in storage spaces)
**What you do**: At this stage, you use VMM to place disks in storage pools (unless they're already in storage pools). You assign a classification to each storage pool (or use the default classification, RemoteStorage). See [How to create or modify a storage pool on a Scale-Out File Server in VMM](How-to-create-or-modify-a-storage-pool-on-a-Scale-Out-File-Server-in-VMM.md).

**How VMM responds**: VMM creates the storage pools and places the disks in them. The storage pools are given the classification that you assigned.

## <a name="BKMK_shares"></a>Stage 4: Create file shares
**What you do**: At this stage, if you just created a storage pool, you can create a file share in that pool. Or, if a CSV already exists on the file server, you can specify that CSV for the file share.

For more information, see [How to create a file share on a Scale-Out File Server in VMM](How-to-create-a-file-share-on-a-Scale-Out-File-Server-in-VMM.md).

**How VMM responds**: If you specify a storage pool in which you want to create the file share, VMM uses the Storage Management API to create a new Cluster Shared Volume (CSV) and file share. Specifically, if you are creating the file share on a storage pool, VMM does the following:

1.  Creates a storage space (also called a Virtual Disk) and adds it to the cluster. This storage space is similar to a LUN that is exposed to a cluster through a SAN.

2.  On each storage space, configures the level of resiliency you specify: two-way mirror, three-way mirror, single-parity, or dual-parity.

3.  Enables additional options, if you choose them: data deduplication, storage tiers, or both.

4.  Initializes, partitions, and formats volumes.

5.  Converts the disks to CSV.

6.  Creates the SMB 3.0 file share.

If a CSV already exists, you can select the CSV, and VMM will create the file folder structure and file share, but will not change other options such as resiliency. If the folder (path) already exists, you can specify the path, and VMM will create the file share. (For example, if the file share was accidently deleted, you can recreate the file share using an existing folder path.)

File shares created in a storage pool inherit the pool's classification, but you can adjust file share classifications individually, if needed.

## <a name="BKMK_permissions"></a>Stage 5: Assign permissions so hosts can access file shares
**What you do**: Open the properties of a Hyper-V host or host cluster, and on the appropriate tab (on a host cluster, the **File Share Storage** tab), assign one or more file shares on a Scale-Out File Server to the host or host cluster. For more information, see [How to assign file shares on a Scale-Out File Server to a Hyper-V host or cluster in VMM](How-to-assign-file-shares-on-a-Scale-Out-File-Server-to-a-Hyper-V-host-or-cluster-in-VMM.md).

**How VMM responds**: VMM configures permissions to folders and file shares on the Scale-Out File Server so that the host or host cluster can access them. Later, if you use VMM to add or remove nodes from the Scale-Out File Server, VMM makes the corresponding changes to permissions for those nodes.

## <a name="BKMK_templates"></a>Stage 6: Make classified storage available to users of templates or private clouds
**What you do**: When you create private clouds or virtual machine templates, you can specify the classification of the storage that will be assigned when virtual machines are created from the templates, or within the private clouds. (This is after you've created storage classifications that match your environment, as described in [Stage 2: Create storage classifications](Overview--configuring-storage-using-Scale-Out-File-Servers-in-VMM.md#BKMK_classifications), earlier in this topic).

**How VMM responds**: VMM makes note of the storage classification that you specified in a virtual machine template, or in a private cloud, and will respond by creating virtual hard disks on the set of storage that you intended. Users will not need to know the structure of the storage that underlies the classifications—for example, they don't need to know a share name or a mount point.

## <a name="BKMK_vhds"></a>Stage 7: Understand how VMM evaluates placement options
**What users do**: Users request that VMM deploy one or more virtual machines, for example, by using a virtual machine template.

**How VMM responds**: When a user or VM administrator requests deployment of one or more virtual machines, VMM evaluates placement options, that is, hosts or host clusters on which virtual machines might be placed. VMM takes into account the amount and classification of storage available to a given host or host cluster, and the classification that was specified (in the VM template or private cloud). VMM displays possible placements, with ratings, to indicate how closely the placements match what was specified.

## <a name="BKMK_copying"></a>Stage 8: Understand how VMM copies virtual hard disk files to file shares
**What users do**: Users use VMM to initiate the deployment of one or more virtual machines.

**How VMM responds**: When a virtual machine is deployed, the virtual hard disk file (or files) must be copied from the VMM library to the appropriate file share (volume). For this copying process, VMM attempts to use the most efficient method available. For Storage Area Networks (SANs) that support Windows Offloaded Data Transfers (ODX), this is the method used. (See [Windows Offloaded Data Transfers Overview](https://technet.microsoft.com/library/hh831628.aspx).) If no offloads are available, the copy process uses a regular Server Message Block (SMB) copy over the network. If that transfer fails for any reason (for example, a network issue), VMM restarts the file copy job using Background Intelligent Transfer Service (BITS).

If the VMM library server and Hyper-V host management accounts are not set correctly for the most efficient transfer methods, VMM defaults to BITS transfer.

## <a name="BKMK_add"></a>Stage 9: If needed, add nodes to the Scale-Out File Server
**What you do**: If needed, you can add nodes to the Scale-Out File Server:

-   **Existing**: [How to add an existing server to a host cluster in VMM](How-to-add-an-existing-server-to-a-host-cluster-in-VMM.md)

-   **Bare metal**: [How to add a bare-metal computer to a host cluster in VMM](How-to-add-a-bare-metal-computer-to-a-host-cluster-in-VMM.md)

If you are using Storage Spaces Direct (which requires Windows Server Technical Preview), adding a node also adds disks, so you must also modify your storage pool to include the additional disks:

-   [How to create or modify a storage pool on a Scale-Out File Server in VMM](How-to-create-or-modify-a-storage-pool-on-a-Scale-Out-File-Server-in-VMM.md)

**How VMM responds**: VMM adds the selected node.

With Storage Spaces Direct, when you add the node, VMM discovers any disks associated with that node. Then, when you modify a storage pool and select the new disks to add, VMM makes those disks available to the hosts and virtual machines that use the share supported by that pool.

## See Also
[Deploying Hyper-V hosts or host clusters from bare metal with VMM](Deploying-Hyper-V-hosts-or-host-clusters-from-bare-metal-with-VMM.md)
[Configuring storage using Scale-Out File Servers in VMM](Configuring-storage-using-Scale-Out-File-Servers-in-VMM.md)
[How to set a disk witness for a Scale-Out File Server quorum in VMM](How-to-set-a-disk-witness-for-a-Scale-Out-File-Server-quorum-in-VMM.md)


