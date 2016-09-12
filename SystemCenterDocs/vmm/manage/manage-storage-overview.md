---
title: Set up the VMM storage fabric
description: This article describes how to set up the VMM storage fabric
author:  rayne-wiselman
manager:  cfreemanwa
ms.date:  2016-08-31
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---

# Set up the VMM storage fabric

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager


You can use System Center 2016 - Virtual Machine Manager (VMM) to manage your physical and virtualized infrastructure. As part of that management VMM can manage storage that you assign to virtual hosts and clusters, and VMs.

- **Local and remote**: VMM recognizes both local and remote storage. Local is storage located on the VMM server or directly attached to it, commonly a disk drive on the server that's connected with inbuilt RAID or SAS JBOD connectivity. Obviously this type of dedicated host storage isn't shared, and doesn't provide resilience or high availability.
- **Block and file-based**: VMM can manage block storage devices and file-based storage.


## Block storage

**Feature** | **Details**
---|---
**Connection** | VMM can manage block storage devices that connect using Fibre Channel, Serial Attached SCSI (SAS), or iSCSI (Internet SCSI).<br/><br/> VMM can discover and manage iSCSI arrays with static, dynamic, or manual targets.<br/><br/>You can use a Microsoft iSCSI target server as a storage device by installing its provider.
**Protocols** | VMM provides support for storage devices that use the SMI-S and and SMP protocols.<br/><br/> VMM uses Window Storage Management API (SMAPI) to manage block-based storage devices compliant with SMI-S or SMP specifications.<br/><br/> VMM combines SMAPI and SMP to manage directly attached storage and external storage arrays.<br/><br/> VMM combines SMAPI and the Storage Management service (which functions as an SMI-S client) to manage SMI-S storage devices.<br/><br/> Vendors of storage devices with the SMI-S standard create SMI-S provides for their devices.
**Virtualization hosts** | Storage configured in VMM can only be used for Hyper-V hosts and clusters.
**Supported storage arrays** | Specific storage arrays are supported in VMM 2016. You can use other arrays, but there's no guarantee that you'll be able to manage all storage tasks in VMM. We recommend that you chat to your storage provider to determine VMM support.
**Virtual fibre channel** | If you want to use virtual fibre channel to give VMs direct access to fibre channel storage, you can manage this storage with VMM in these configurations.<br/><br/> Single storage array connected to a single fabric (comprised of single or multiple switches) connected to a single vSAN.<br/><br/> Single storage array connected to multiple fabrics (comprised of single or multiple switches per fabric) connected to a single vSAN.<br/><br/> Multiple storage arrays connected to a single fabric (comprised of single or multiple switches) connected to a single vSAN.<br/><br/> Multiple storage arrays connected to multiple fabrics (comprised of single or multiple switches per fabric) connected to multiple vSANs. This configuration provides dual-redundant paths to storage arrays.<br/><br/> A vSAN can only include HBAs from a single fabric.

## Set up block storage

The general process for setting up block-based storage in the VMM fabric is as follows:

1. [Create storage classifications](manage-storage-classifications.md): You create storage classifications to group storage based on shared characteristics, often performance and availability. Then instead of assigning specific storage devices to them, you assign storage to VMM host groups you assign a specific classification so that host groups can use any available storage device with the assigned classification. You don't have to create classifications before you add storage devices. You can create them during storage device discovery.
2. [Add the storage](manage-storage-add-device.md): You add the storage as a resource in the VMM fabric. When you add the device VMM automatically discovers any existing storage pools and logical units on the device. You can classify storage as you add it.
3. [Configure storage and allocate capacity](manage-storage-host-groups.md): After a storage array is managed by VMM you can configure settings. You can specify how you want to use rapid provisioning on the device (snapshots or cloning). You can add and modify storage pools and storage logical units (LUNs) in the pools. You can allocate capacity (either entire storage pools) or specific LUNs to one or more host groups.
4. [Use the storage](manage-compute-add-storage-hyper-v.md): After storage is allocated to a host group you can use the storage for a specific host or cluster. When you add a host or cluster to a host group the host and cluster can use storage associated with the group.

## File storage

VMM can manage file storage that supports the SMB 3.0 protocol. SMB is supported by file shares on computers running Windows Server 2012 or higher, and by third-party vendors of network-attached storage (NAS) devices.

- **Windows file server**:  You can add a remote file server as a storage device or you can scale file-based storage Scale-Out File Server (SOFS).
- **Scaled-out file server (SOFS)**: SOFS provides a file server cluster in which storage is shared between the cluster nodes. Storage for SOFS could be a SAN (SAS, iSCSI, Fibre Channel) or could integrate with Storage Spaces Direct.
- **Storage Spaces Direct (S2D)**: S2D is the next evolution of Microsoft Storage Spaces, which virtualizes storage by grouping disks into storage pools and creating virtual disks (storage spaces) from the pool capacity. In S2D you can build highly available storage using local storage. This removes the need for remote SAN storage devices and enables use the storage devices that weren't previously available, such as SATA SSD or NVMe flash. [Learn more](https://technet.microsoft.com/library/mt126109.aspx).
- **Storage replication**: VMM supports Windows Storage Replica for protecting data in a primary storage volume that replicating it to a secondary volume. [Learn more](https://technet.microsoft.com/library/mt126183.aspx).
- **Storage resources**: You can control access to shared storage on an SOFS or VM by setting storage quality-of-service (QoS) policies. These policies set maximum and minimum bandwidth for storage resources. [Learn more](https://technet.microsoft.com/library/mt126108.aspx)

## Set up file storage

The general process for setting up file storage in the VMM fabric is as follows:

1. **Add and discover storage**: You add the file server as a resource in the VMM fabric. When you add the device VMM automatically discovers any file shares on the device. You can classify storage as you add it.
2. **Create storage classifications**: You create storage classifications to group file shares based on shared characteristics, often performance and availability. Then instead of assigning specific storage devices to VMM host groups you assign a specific classification so that host groups can use any available storage with the assigned classification. You don't have to create classifications before you add storage devices. You can create them during storage device discovery.
3. **Provision storage**: After a file server is managed by VMM you can configure settings. For example you can modify storage pools on an SOFS or create a file share.
4. **Allocate capacity**: After you have the storage set up you can allocate capacity from the array. You allocate capacity by assigning file shares to one or more host groups.
5. **Use the storage**: After storage is allocated to a host group you can use the storage for a specific host or cluster. When you add a host or cluster to a host group the host and cluster can use storage associated with the group.
6. **Decommission storage**: VMM can decommission the storage it manages.

[Learn more](manage-storage-file.md) about setting up file storage in VMM.

## Storage classifications

Storage classifications provide a layer of abstraction over specific storage devices. You group storage devices together based on their characteristics. For example you could create:

- Bldg1Gold: A set of solid-state drives (SSDs) that you will make available to users in building 1.
- Bldg1Silver: A set of SSDs and hard disk drives (HDDs) that you will make available to users in building 1.
- Bldg2Gold: A set of SSDs that you will make available to users in building 2.
- Bldg2Silver: A set of SSDs and HDDs that you will make available to users in building 2.

After you've created classifications you assign them to storage pools that include block or file-based storage. You can tweak classification settings for file shares within pools as required.

## Next steps

[Set up storage classifications](manage-storage-classifications.md) in the VMM fabric
