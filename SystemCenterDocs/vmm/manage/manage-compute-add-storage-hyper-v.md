---
ms.assetid: 0cb44190-98ff-47d8-a53e-b199895bc410
title: Add storage to Hyper-V hosts and clusters
description: This article provides about managing your Hyper-V environment in the VMM fabric
author:  rayne-wiselman
ms.author: raynew
manager:  cfreemanwa
ms.date:  2016-09-22
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---


# Add storage to Hyper-V hosts and clusters

>Applies To: System Center 2016 - Virtual Machine Manager

Read this article to allocate provisioned storage to Hyper-V hosts and clusters in the System Center 2016 - Virtual Machine Manager (VMM) fabric.

## Before you start

**Storage type** | **Prerequisite** | **Details**
--- | --- | ---
**Fibre channel or iSCSI** |  Storage array access | **Multipath I/O**: The Multipath I/O (MPIO) feature must be added on each host that will access the Fibre Channel or iSCSI storage array. You can add the MPIO feature through Server Manager. If MPIO is already enabled before you add the host, VMM will automatically enable it for supported storage arrays using Microsoft DSM. If you have vendor specific DSMs these will be used. If you add a host before you add MPIO, after adding MPIO you'll manually configure it to add the discover device hardware IDs.<br/><br/> **Fibre Channel**: If you are using a Fibre Channel storage array network (SAN), each host must have a host bus adapter (HBA) installed, and zoning must be correctly configured.<br/><br/> **iSCSI**: If you are using an iSCSI SAN, make sure that iSCSI portals have been added and that the iSCSI initiator is logged into the array. Additionally, make sure that the Microsoft iSCSI Initiator Service on each host is started and set to Automatic.<br/><br/> **Storage group**: In VMM a storage group binds together host initiators, target ports, and logical units. A storage group contains one or more host initiator IDs (IQN or WWN) (WWN). A storage group also contains one or more target ports and one or more logical units. Logical units are exposed to the host initiators through the target ports.<br/><br/> By default, when VMM manages the assignment of logical units, VMM creates one storage group per host, either a stand-alone host or a host cluster node. However, for some storage arrays, it is preferable to use one storage group for the entire cluster, where host initiators for all cluster nodes are contained in a single storage group. To support this configuration, you must set the CreateStorageGroupsPerCluster property to $true by using the Set-SCStorageArray cmdlet.
**Shared storage managed by VMM** | Discovery and classification | To use shared storage that is under VMM management, storage must already be discovered and classified in the Fabric workspace of the VMM console. Then, either storage pools, logical units (or file shares), or both must be allocated to the host group or the parent host group chosen for your set of hosts.<br/><br/> If you allocate storage pools to host groups, you can wait until after the host cluster is created to create logical units (within the storage pools) on the cluster. For more information, see How to configure storage on a Hyper-V host cluster in VMM.
**Shared storage not managed by VMM** | Disk availability | To use shared storage that is not under VMM management, disks must be available to all nodes in the cluster before you can add them. Therefore, you must provision one or more logical units to all hosts that you want to cluster, and mount and format the storage disks on one of the hosts.<br/><br/> VMM is agnostic regarding the use of asymmetric storage, where a workload can use disks that are shared between a subset of the cluster nodes. VMM does not support or block this storage configuration. Note that to work correctly with VMM, each cluster node must be a possible owner of the cluster disk.


## Create and assign logical units to a standalone host

You create logical units and assign them to the Hyper-V host or cluster. To complete these procedures, you must be a member of the Administrator user role or a member of the Delegated Administrator user role where the management scope includes the host group where the Hyper-V host is located.


### Create a logical unit

1. In **Fabric** > **Servers** > **All Hosts**, right-click the host that you want to configure > **Properties**.
2. On the toolbar, next to **Disk**, click **Add**. Next to **Logical unit** click **Create Logical Unit**.
3. In Create Logical Unit > **Storage pool** choose the pool from which the create the logical unit. Specify a name (alphanumeric only), a description and the unit size.
4. Verify that the unit is selected in **Logical unit** and in **Format new disk** area, if you want to format the disk, select **Format this volume as NTFS volume with the following settings**. Specify the format volume settings. Note that if you select **Force format even if a file system is found** all existing data on the volume will be overwritten.
5. VMM registers the storage logical unit to the host and mounts the storage disk. To view the associated job information, open the **Jobs** workspace.
6. To verify that the logical unit was assigned, view the information on the **Storage** tab in the **Host Name** > **Properties** dialog box. The newly assigned logical unit appears under **Disk**. Click the new disk to view the disk details. If the **Array** field is populated in the disk details, this indicates that the storage array is under VMM management.
7. To configure additional disk settings open Disk Management on the host. To open Disk Management, click **Start**, type **diskmgmt.msc** in the search box, and then press ENTER. The new disk appears in the list of disks as a basic disk. If you chose to format the disk, the disk is already formatted and online. You can right-click the disk to see the available options, such as **Format** and **Change Drive Letter and Paths**.

### Assign the logical unit to a host


1.  In **Fabric** > **Servers** > **All Hosts**, right-click the host that you want to configure > **Properties**.

2.  To assign an existing logical unit to the host, on the toolbar, next to **Disk**, click **Add**. Select the logical unit you want to assign. Configure the format and mount point options, and then click **OK** to assign the logical unit to the host. Note that if the logical unit has existing data, and you do not use the **Force Format** option, the VMM job to assign the logical unit will complete with a warning. VMM assigns the logical unit to the host. You can format the disk later.



### Create an iSCSI session on a host


1.  On the target host, in the Services snap-in, make sure that the Microsoft iSCSI Initiator Service is started and set to Automatic.
2.  In **Fabric** > **Servers** > **All Hosts** **Hosts**, right-click the host that you want to configure > **Properties**.
3.  Under **iSCSI Arrays**, see if the storage array is already listed. If it is not, on the toolbar, next to **iSCSI Array**, click **Add**.
4.  In the Create New iSCSI Session > **Array** , click the storage array you want to use.
5.  Click **Create** to create a new session. Click Use advanced settings if you want to modify customized settings, including target listener, name, or the host NIC that you want to use.
6.  The array that you added appears under **iSCSI Arrays**. Click the array to view more details.

## Configure storage for a Hyper-V cluster

1. Click **Fabric** **Servers** > **All Hosts**. Right-click the cluster you want to configure > **Properties**.
In **Host Cluster Name** >  **Properties** click a tab:

    - **Available Storage**: for adding available storage, converting available storage to shared storage (CSV), or removing available storage.

    - **Shared Volumes**: for adding cluster shared volumes (CSVs), converting CSVs to available storage, or removing CSVs. The cluster must run at least Windows Server 2012 to support CSVs.

2.  Configure storage for the host cluster, using the notes in the following table:

    **Action** | **Notes**
    ---|---
    Add available storage or CSVs | For a logical unit name, use only alphanumeric characters.<br/><br/> You can't change the partition style of a disk that has already been initialized.
    Convert available storage to CSVs | Make sure that there are no virtual machines on the cluster that have their associated .vhd or .vhdx files located on the storage that you want to convert.<br/><br/> Convert volumes one at a time.<br/><br/> After conversion, confirm that the logical unit appears on the **Shared Volumes** tab.
    Convert CSVs to available storage | Make sure that there are no virtual machines on the cluster that have their associated .vhd or .vhdx files located on the storage that you want to convert. **Caution:**     If you convert shared to available storage, and the storage is being used by virtual machines, serious data loss can result.<br/><br/>  Convert volumes one at a time. After conversion, confirm that the logical unit appears on the **Available Storage** tab.
    Remove available storage or CSVs | If there are virtual machines on the cluster that currently use the storage for their associated .vhd or .vhdx files, the **Remove** option is disabled.

3.  When you're ready to commit the changes, click **OK**.
