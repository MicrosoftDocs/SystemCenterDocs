---
title: Manage Storage Replica in VMM
description: This article describes how to set up Storage Replica in the VMM fabric
author:  rayne-wiselman
ms.author: raynew
manager:  cfreeman
ms.date:  2016-09-22
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---

# Manage Storage Replica in VMM

>Applies To: System Center 2016 - Virtual Machine Manager


Storage Replica is a new feature in Windows Server 2016. It enables storage-agnostic, block-level, synchronous replication between clusters or servers for disaster preparedness and recovery, as well as stretching of a failover cluster across sites for high availability. Synchronous replication enables mirroring of data in physical sites with crash-consistent volumes, ensuring zero data loss at the file system level. Asynchronous replication allows site extension beyond metropolitan ranges with the possibility of data loss.

[Learn more](https://aka.ms/storagereplica) and review the [FAQ](https://technet.microsoft.com/library/mt126107.aspx).

The article provides explains how Storage Replica integrates with System Center 2016 - Virtual Machine Manager (VMM),  and describes how to set up Storage Replica using PowerShell to replicate storage in the VMM fabric.


## Storage Replica in VMM

You can use Storage Replica to replicate Hyper-V cluster data or file data. Using Storage Replica in VMM provides a number a business advantages:

- Eliminates the cost and complexity associated with synchronous replication solutions such as SAN.
- Synchronous replication minimizes downtime and data loss. It provides a RPO of 0 (zero data loss). RTO (data unavailability) only occurs during the time in which a primary site fails and a secondary site starts.
- Source and destination storage hardware doesn't need to be identical.

## Before you start

* VMM must be running on System Center 2016 Datacenter Edition.
* Hyper-V must be running on Windows Server 2016 Datacenter, Server Core, or Nano.
* Only synchronous replication is supported. Asynchronous isn't supported.
* You need two sets of storage, either volume or file storage. Both the source and destination locations must have the same type of storage (file or volume) but the actual storage can be mixed. For example you could have Fibre Channel SAN at one end and Spaces Direct (in hyper-converged or disaggregated mode) at the other.
* Each set of storage should be available in each of the clusters. Cluster storage shouldn't be shared.
* Source and destination volumes (including log volumes) need to be identical in size and block size. This is because Storage Replica uses block replication.
* You need at least one 1GbE connection on each storage server, preferably 10GbE, iWARP, or InfiniBand.
* Each file server or cluster node needs firewall rules that allow ICMP, SMB (port 445, plus 5445 for SMB Direct) and WS-MAN (port 5985) bi-directional traffic between all nodes.
* You need to be a member of the Administrator group on each cluster node.
* Storage Replica can only be set up using Windows PowerShell at present.
* Source and destination storage must be managed by the same VMM server.
* Integrating VMM with Azure Site Recovery isn't supported.
* Setting write order and consistency groups isn't supported.


## Deployment steps

1.  **Identify storage**: Identify the source and destination storage you want to use.
2.  **Discover and classify**: If your storage isn't currently in the VMM fabric, you need to discover it with VMM. Both the source and desintation storage must be managed by the same VMM server. After discovery you create a storage pool for it, and a storage classification for it. [Learn more](https://technet.microsoft.com/library/gg610600.aspx).
3.  **Pair**: Pair the source and destination storage array.
4.  **Provision**: After your storage is paired you'll need to provision identical data and log volumes from the source and destination storage pools created on the respective storage arrays. In addition to provisioning a volume for data that will be replicated, you also need to provision a volume for replication transaction logs. As data is updated on source storage, the transaction log is appended and delta changes are synchronized (using synchronous replication) with destination storage.
5.  **Create replication groups**: After the volumes are in place you create replication groups. Replication groups are logical groups containing multiple volumes. The replication groups need to be identical, containing the data and log volumes for the source and destination sites respectively.
6.  **Enable replication**: Now you can enable replication between the source and destination replication groups.
7.  **Refresh**: To finalize creation of replication groups and to trigger the initial data replication, you need to refresh the primary and secondary storage provider. Data replicates to destination storage.
8.  **Verify status**: Now you can check the status of the primary replication group. It should be in the Replicating state.
9.  **Add VMs**: When delta replication is up and running you can add VMs that use storage contained in the replication group. When you add the VMs they'll be detected and will begin replicating automatically.
10. **Run failover**: After replication is in a Synchronizing state, you can run a failover to check it's working as expected. There isn't a test failover mechanism right now, so you'll run a manual failover in response to planned or unplanned outages. After failover you can delete the VM on the source site (if it still exists) and create a VM on the destination site using the replicated data.
11. **Run failback**: After failover is complete and replica VMs are up and running, you can fail back as you need to. Note that:

    - If you run an unplanned failover and your source location isn't available, you'll run a failover to failback from the secondary to primary location, and then create the VM in the primary location.
    - If you run a planned failover and the source VM is still available, you need to stop replication, remove the source VM, create the VM in the secondary location, and then restart replication. Then at the primary site you can create the VM with the same settings as the original VM.


## Retrieve PowerShell objects

1. Before you start retrieve the name of the PowerShell objects you want to use.
2. Get the name of the primary storage array and assign to variable.

        $PriArray = Get-SCStorageArray - Name $PriArrayName

3. Get the name of the secondary storage array and assign to variable.

        RecArray = Get-SCStorageArray - Name $RecArrayName

4. Get the name of the primary storage pool and assign to variable.

        $ $ PriPoolName $RecPool = Get-SCStoragePool -Name $



5. Get the name of the secondary storage pool and assign to variable.

        $ $PriPoolName $RecPool = Get-SCStoragePool -Name $


## Pair the storage arrays

Pair the primary and secondary storage arrays using the variables for the storage array names. Note that the array name should be the same as the cluster name.

        Set-SCStorageArray -StorageArray $PriArray -PeerStorageArrayName $RecArray.name

If you created the cluster outside VMM and you do need to rename the array name to match the cluster name use:

        Get-SCStorageArray -Name "existing-name" | Set-SCStorageArray -Name "new-name"


## Provision LUNs and create the storage groups

Provision a LUN from the storage pool for data and for the log. Then create replication groups.

1. Provision and create on the source.

        Set-SCStorageArray -StorageArray $PriArray -PeerStorageArrayName $RecArray.name

        $PrimaryVol = New-SCStorageVolume -StorageArray $PriArray -StoragePool $PriPool -Name PrimaryVol -SizeInBytes $VolSize -RunAsynchronously -PhysicalDiskRedundancy "1" -FileSystem "CSVFS_NTFS" -DedupMode "Disabled"

        $PrimaryLogVol = New-SCStorageVolume -StorageArray $PriArray -StoragePool $PriPool -Name PrimaryLogVol -SizeInBytes $LogVolSize -GuidPartitionTable -RunAsynchronously -FileSystem "NTFS"

        $PriRG = New-SCReplicationGroup -Name PriRG -StorageVolume $PrimaryVol -LogStorageVolume $PrimaryLogVol

2. Provision and create on the destination.

        $RecoveryVol = New-SCStorageVolume -StorageArray $RecArray -StoragePool $RecPool -Name RecoveryVol -SizeInBytes $VolSize -RunAsynchronously -PhysicalDiskRedundancy "1" -FileSystem "CSVFS_NTFS" -DedupMode "Disabled"

        $RecoveryLogVol = New-SCStorageVolume -StorageArray $RecArray -StoragePool $RecPool -Name RecoveryLogVol -SizeInBytes $LogVolSize -GuidPartitionTable -RunAsynchronously -FileSystem "NTFS"

        $RecRG = New-SCReplicationGroup -Name RecRG -CreateOnArray -ProtectionMode Synchronous -StorageVolume $RecoveryVol -LogStorageVolume $RecoveryLogVol

## Enable replication

Now enable synchronous replication between the source and destination replication groups.

    Set-SCReplicationGroup -ReplicationGroup $PriRG -Operation EnableProtection -TargetReplicationGroup $RecRG -EnableProtectionMode Synchronous

## Refresh the storage providers

1. Open the  VMM console.
2. Click **Fabric Resources** > **Providers**. Right-click the provider > **Refresh**.

## Verify replication status

Retrieve the replication status for the source replication group to make sure that replication is working as expected.

    Get replication status Get-SCReplicationGroup | where {($_.Name.EndsWith("PriRG")) -or ($_.Name.EndsWith("RecRG"))}  | fl Name, IsPrimary, ReplicationState, ReplicationHealth

## Create a VM

Create a VM using a LUN in the source replication group. Alternatively you can create a VM in the VMM console.

    New-SCVirtualMachine -Name "DemoVM" -VMHost <HostName> -Path $PrimaryVol -VMTemplate <VMTemplate>


## Run a failover
Run failover.

    Set-SCReplicationGroup -ReplicationGroup $PriRG -Operation PrepareForFailover

    Set-SCReplicationGroup -ReplicationGroup SRecRG -Operation Failover

## Run failback

Before you fail back, in the VMM console, remove the source VMs if they"re still available. You can't fail back to the same VM.

Now run failback:

    Set-SCReplicationGroup -ReplicationGroup $PriRG -Operation ReverseRoles -EnableProtectionMode Synchronous -TargetReplicationGroup $RecRG

After running failback you can create VMs at the source site using the failed back VHD/configuration files.

## Stop replication

If you want to stop replication you'll need to run this cmdlet at the source and destination.

    Set-SCReplicationGroup -ReplicationGroup $RecRG -Operation TearDown  Tear down need to be done on both RGs



## See Also

- [Storage replica overview](https://aka.ms/storagereplica)
