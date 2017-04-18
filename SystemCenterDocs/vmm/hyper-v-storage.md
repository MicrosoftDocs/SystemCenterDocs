---
ms.assetid: 0cb44190-98ff-47d8-a53e-b199895bc410
title: Add storage to Hyper-V hosts and clusters
description: This article provides information about managing your Hyper-V environment in the VMM fabric
author:  rayne-wiselman
ms.author: raynew
manager:  cfreeman
ms.date:  01/23/2016
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---


# Add storage to Hyper-V hosts and clusters

>Applies To: System Center 2016 - Virtual Machine Manager

Read this article to allocate provisioned storage to Hyper-V hosts and clusters in the System Center 2016 - Virtual Machine Manager (VMM) fabric.



## Before you start

Before you can allocate provisioned storage to hosts and cluster, it should be discovered and classified in the VMM fabric:

1. Discover and classify storage:
    - [Add and classify block storage devices](manage/manage-storage-add-device.md). Learn about [classification](manage/manage-storage-classifications.md).
    - [Add file storage](manage/manage-storage-file.md#add-a-file-share-to-the-vmm-fabric)
2. [Allocate block storage to host groups](manage/manage-storage-host-groups.md). You can allocate an entire storage pool, or a specific logical unit (LUN).
3. Make sure you've completed these steps before you allocate storage to hosts:
    - **MPIO**: If you're using fiber channel or iSCSI storage, the Multipath I/O (MPIO) feature must be enabled on each host.
        - If MPIO is already enabled before you add the host, VMM will automatically enable it for supported storage arrays using Microsoft DSM. If you have vendor specific DSMs these will be used.
        - If you add a host to VMM and enable MPIO later, you need to configure it manually to add the discover device hardware IDs.
    - **HBA and zoning**: If you're using Fiber Channel storage array network (SAN), each host must have a host bus adapter (HBA) installed, and zoning must be correctly configured.
    - **iSCSI**: If you are using an iSCSI SAN, make sure that iSCSI portals have been added, and that the iSCSI initiator is logged into the array.<br/><br/> Make sure that the Microsoft iSCSI Initiator Service on each host is started and set to **Automatic**
    - **Storage group**: Explain to your storage administrator how VMM manages storage.
        - In VMM a storage group binds together host initiators, target ports, and logical units.
        - A storage group contains one or more host initiator IDs (IQN or WWN) (WWN).
        - A storage group also contains one or more target ports and one or more logical units. Logical units are exposed to the host initiators through the target ports.
        - By default, when VMM manages the assignment of logical units, VMM creates one storage group per host, either a standalone host or a host cluster node.
        - For some storage arrays, it is preferable to use one storage group for the entire cluster, where host initiators for all cluster nodes are contained in a single storage group. To do this, you need to set the CreateStorageGroupsPerCluster property to $true by using the Set-SCStorageArray cmdlet.



## Allocating storage

- You can allocate file storage directly to hosts and clusters.
- You can add LUNs to hosts and clusters:
- If you already provisioned LUNs on a host group, you can assign these to hosts and clusters.
- If you provisioned a storage pool on a host group, you can create LUNs during the procedure to add storage to a cluster.
- If you want to use shared storage that isn't managed by VMM, the storage disks must be available to all hosts or nodes before you can add them. You need to provision one or more LUNs to all hosts you want to cluster, and then mount and format the storage disks on one of the nodes. Note that VMM doesn't support or block the use of asymmetric storage, where a workload can use disks that are shared between a subset of the cluster nodes. Each cluster node must be a possible owner of the cluster disk.
- After adding iSCSI storage to a host, you need to create a new session to the storage.



## Allocate file storage to a standalone host

You can assign file shares on any host on which you want to create VMs that will use the file share as storage.

1. Click Fabric > **Servers** > **All Hosts**, and select the host or cluster node you want to configure.
2. Click **Host** > **Properties** >  **Host Access**. Specify a Run As account. By default the Run As account that was used to add the host to VMM is listed. In the **Run As** account box, configure the account settings. You can't use the account that you use for the VMM service. Note that:
    - If you used a domain account for the VMM service account, add the domain account to the local Administrators group on the file server.
    - If you used the local system account for the VMM service account, add the computer account for the VMM management server to the local Administrators group on the file server. For example, for a VMM management server that is named VMMServer01, add the computer account VMMServer01$.
    - Any host or host cluster that accesses the SMB 3.0 file share must have been added to VMM using a Run As account. VMM automatically uses this Run As account to access the SMB 3.0 file share.
    - If you specified explicit user credentials when you added a host or host cluster, you can remove the host or cluster from VMM, and then add it again by using a Run As account.
3. Click **Host Name Properties** > **Storage** > **Add File Share**.
4. In **File share path**, select the required SMB 3.0 file share, and then click **OK**.
5. To confirm that the host has access, open the **Jobs** workspace to view the job status. Or, open the host properties again, and then click the **Storage** tab. Under **File Shares**, click the SMB 3.0 file share. Verify that a green check mark appears next to **Access to file share**.
6. Repeat this procedure for any standalone host that you want to access the SMB 3.0 file share, or for all nodes in a cluster

### Assign a logical unit to a standalone host

Either assign an existing unit, or create a new one and assign it.


1.  In **Fabric** > **Servers** > **All Hosts**, right-click the host that you want to configure > **Properties**.
2. If you want to create a new logical unit:
    - On the toolbar, next to **Disk**, click **Add**. Next to **Logical unit** click **Create Logical Unit**.
    - In Create Logical Unit > **Storage pool** choose the pool from which the create the logical unit. Specify a name (alphanumeric only), a description and the unit size. Click **OK** to finish.

3.  To assign an existing logical unit to the host, on the toolbar, next to **Disk**, click **Add**, and select the logical unit you want to assign.
4. In the **Logical unit** list, verify that the logical unit that you just created is selected.
5. In **Format new disk**, if you want to format the disk, select **Format this volume as NTFS volume with the following settings**, and specify the settings. Note that if you select **Force format even if a file system is found** all existing data on the volume will be overwritten. If the logical unit has existing data, and you do not use the **Force Format** option, the VMM job to assign the logical unit will complete with a warning. VMM assigns the logical unit to the host. You can format the disk later.
6. In **Mount Point**, select the mount options. Then click **OK** to assign the logical unit to the host.
7. VMM registers the storage logical unit to the host and mounts the storage disk.
    - To view the associated job information, open the **Jobs** workspace.
    - To verify that the logical unit was assigned, view the information on the **Storage** tab in the **Host Name** > **Properties** dialog box. The newly assigned logical unit appears under **Disk**. Click the new disk to view the disk details.
    - If the **Array** field is populated in the disk details, this indicates that the storage array is under VMM management.
8. To configure additional disk settings open Disk Management on the host. To open Disk Management, click **Start**, type **diskmgmt.msc** in the search box, and then press ENTER. The new disk appears in the list of disks as a basic disk. If you chose to format the disk, the disk is already formatted and online. You can right-click the disk to see the available options, such as **Format** and **Change Drive Letter and Paths**.

## Configure storage for a Hyper-V cluster

1. Click **Fabric** **Servers** > **All Hosts**. Right-click the cluster you want to configure > **Properties**.
In **Host Cluster Name** >  **Properties** click a tab:

    - **Available Storage**: for adding available storage, converting available storage to shared storage (CSV), or removing available storage.
    - **Shared Volumes**: for adding cluster shared volumes (CSVs), converting CSVs to available storage, or removing CSVs. The cluster must run at least Windows Server 2012 to support CSVs.

2.  Configure storage for the host cluster. Note that:
    - If you add available storage for CSVs, use only alphanumeric characters for a LUN. Note that you can't change the partition style of a disk that has already been initialized.
    - If you're converting available storage to CSVs, make sure there are no VMs on the cluster that have their associated .vhd or .vhdx files located on the storage that you want to convert.<br/><br/> Convert volumes one at a time. After conversion, confirm that the logical unit appears on the **Shared Volumes** tab.<br/><br/> **Caution**: If you convert shared to available storage, and the storage is being used by virtual machines, serious data loss can result.
    - You can only remove storage if there are no VMs in the cluster currently using the storage for their vhds.

3.  When you're ready to commit the changes, click **OK**.


## Create an iSCSI session

1.  On the target host, in the Services snap-in, make sure that the Microsoft iSCSI Initiator Service is started and set to Automatic.
2.  In **Fabric** > **Servers** > **All Hosts** **Hosts**, right-click the host that you want to configure > **Properties**.
3.  Under **iSCSI Arrays**, see if the storage array is already listed. If it is not, on the toolbar, next to **iSCSI Array**, click **Add**.
4.  In the Create New iSCSI Session > **Array** , click the storage array you want to use.
5.  Click **Create** to create a new session. Click Use advanced settings if you want to modify customized settings, including target listener, name, or the host NIC that you want to use.
6.  The array that you added appears under **iSCSI Arrays**. Click the array to view more details.
