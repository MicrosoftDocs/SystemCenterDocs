---
description: Descriptions of the new features in System Center DPM 2016, 1801, 1807 and 2019
manager: carmonm
ms.topic: article
author: rayne-wiselman
ms.prod: system-center
keywords:
ms.date: 06/10/2020
title: What's new in System Center DPM 2016, 1801, 1807 and 2019
ms.technology: data-protection-manager
ms.assetid: a5e81bf0-43a6-4099-af2e-dfb0c1aa7ed8
ms.author: raynew
---

# What's new in System Center Data Protection Manager

::: moniker range="sc-dpm-2019"

This article details the new features supported in System Center 2019 and 2019 UR1 - Data Protection Manager (DPM).

::: moniker-end

::: moniker range="sc-dpm-1807"

DPM 1807 is the latest release in the System Center Semi Annual Channel (SAC). You can update to System Center Data Protection Manager (DPM) version 1807 only from DPM 1801. If you're upgrading to DPM 1807, see the [Release Notes for 1807](dpm-release-notes.md#dpm-1807-release-notes).

::: moniker-end

::: moniker range="sc-dpm-1801"

System Center DPM 1801 provides the following new features:

::: moniker-end

::: moniker range="sc-dpm-2016"

System Center DPM 2016 adds improvements in three key areas: storage efficiency, performance, and security. Modern Backup Storage takes advantage of improvements in Windows Server 2016, creating storage space savings of 30-40%. In addition to space savings, you can create storage and performance efficiency by using MBS to back up designated workloads to specific volumes. Improved DPM performance reduces I/O requirements up to 70%, resulting in faster backups. DPM 2016 supports shielded VMs.

::: moniker-end

::: moniker range="sc-dpm-2019"

## New features in DPM 2019

 See the following sections for detailed information about the new features/feature updates supported in DPM 2019.

::: moniker-end

::: moniker range="sc-dpm-2019"

### Windows Server 2019 support
DPM 2019 can be installed on Windows Server 2019 and Windows Server 2016.

### SQL 2017 support as DPM database
DPM 2019 support SQL 2017 as its database.

You can install SQL Server on a remote server, or on the DPM server. The database must be installed and running before you install DPM.

### Support for newer workloads backups
With DPM 2019, you can back up newer versions of workloads, listed below:
-	Hyper-V VMs 2019
-	Windows Server 2019
-	Exchange 2019
-	SharePoint 2019
-	VMWare [vSphere 6.7](back-up-vmware.md#vmware-vsphere-67)
-	System Center Virtual Machine Manager 2019. [Learn more](dpm-protection-matrix.md).

### Faster backups with Tiered storage using SSDs
DPM 2016 introduced [Modern Backup Storage](https://docs.microsoft.com/system-center/dpm/add-storage?view=sc-dpm-2016), improving storage utilization and performance. MBS uses ReFS as underlying file system and is designed to make use of hybrid storage such as tiered storage.

To achieve the scale and performance by MBS we recommend using a small percentage (4% of overall storage) of flash storage (SSD) with DPM 2019 as a tiered volume in combination with DPM HDD storage. DPM 2019 with tiered storage delivers 50-70% faster backups. [Learn more](add-storage.md#set-up-mbs-with-tiered-storage).

### Support for Central Monitoring
With DPM 2019, all DPM-A customers (customer connected to Azure) have the flexibility of using Central Monitoring, a monitoring solution provided by Microsoft Azure Backup.

You can monitor both on-premises and cloud backups, using Log Analytics with central monitoring capability.  [Learn more](monitor-dpm.md#central-monitoring).

### VMware backup to tape
For long term retention on VMware backup data on-premises, you can now enable VMware backups to tape. The backup frequency can be selected based on the retention range (which will vary from 1-99 years) on tape drives. The data on tape drives could be both compressed and encrypted.

DPM 2019 supports both Original Location Recovery (OLR)) and Alternate Location Recovery (ALR)) for restoring the protected VM. [Learn more](back-up-vmware.md).

### VMWare parallel backups
With DPM 2019, all your VMWare VMs backup within a single protection group would be parallel, leading to 25% faster VM backups.

With earlier versions of DPM, parallel backups were performed only across protection groups. With DPM 2019, VMWare delta replication jobs run in parallel. By default, number of jobs to run in parallel is set to 8. [Learn more](back-up-vmware.md#vmware-parallel-backups).

## New features in DPM 2019 UR1

See the following sections for information about the new features/feature updates supported in DPM 2019 UR1.   

For issues fixed in 2019 UR1, see the [KB article](https://support.microsoft.com/help/4533416/update-rollup-1-for-system-center-2019-data-protection-manager).

### Support for ReFS volumes and ReFS volumes with Deduplication enabled

With DPM 2019 UR1, you can backup the ReFS volumes and workloads deployed on the ReFS volume. You can back up the following workloads deployed on the ReFS volumes:

 - **Operating System (64 bit)**: Windows Server 2019, 2016, 2012 R2, 2012.
 - **SQL Server**: SQL Server 2019, SQL Server 2017, 2016.
 - **Exchange**: Exchange 2019, 2016.
 - **SharePoint**: SharePoint 2019, 2016 with latest SP.

 > [!NOTE]
 > Backup of Hyper-V VMs stored on ReFS volume is supported with DPM 2019 RTM.

### Windows Server Core support
You can install DPM 2019 UR1 on Windows Server Core 2019 and 2016.

> [!NOTE]
> Installation of MARS agent on Windows Server Core is not supported. With this limitation, DPM cannot be connected to Azure Recovery Services Vault when it is installed on Windows Server Core.

### Disk exclusion for VMware VM backup
With DPM 2019 UR1, you can exclude the specific disk from a VMware VM backup. [Learn more](back-up-vmware.md).

### Support for additional layer of authentication to delete online backup
With DPM 2019 UR1, an  additional a layer of authentication is added for  critical operations. You will be prompted to enter a security PIN when you perform *Stop Protection* with *Delete data* operations.

### New cmdlet parameter

DPM 2019 UR1 includes a new parameter **[-CheckReplicaFragmentation]**. The new parameter, calculates the fragmentation percentage for a replica, and is included in the **Copy-DPMDatasourceReplica** cmdlet.

## New features in DPM 2019 UR2

See the following sections for information about the new features/feature updates supported in DPM 2019 UR2.

For issues fixed in 2019 UR2, see the [KB article](Link to detailed content).

### Support for SQL Server Failover Cluster Instance (FCI) using Cluster Shared Volume (CSV)

DPM 2019 UR2 supports SQL Server Failover Cluster Instance (FCI) using Cluster Shared Volume (CSV). With CSV, the management of your SQL Server Instance is simplified. You will be able to manage the underlying storage from any node as there is an abstraction to which node owns the disk. [Learn more](Link to detailed content).

### Optimized Volume to Volume Migration

DPM 2019 UR2 supports optimized Volume to Volume Migration. The optimized Volume to Volume Migration allows you to move data sources to the new volume much faster. The enhanced migration process migrates only active backup copy (Active Replica) to the new volume. All the new recovery points are created on the new volume while existing recovery points are maintained on the existing volume and are purged as per the retention policy. [Learn more](add-storage.md#optimized-volume-to-volume-migration).

### Offline Backup using Azure Data Box (Preview)

DPM 2019 UR2 supports Offline backup using Azure Data Box. With [Microsoft Azure Data Box](https://azure.microsoft.com/services/databox/) integration, you can overcome the challenge of moving terabytes of backup data from on-premises to Azure storage. Azure Data Box saves the effort required to procure your own Azure-compatible disks and connectors or to provision temporary storage as a staging location. Microsoft also handles the end-to-end transfer logistics, which you can track through the Azure portal. [Learn more](offline-seeding-azure-data-box.md).

### SQL Server 2019 support as DPM database

DPM 2019 supports SQL server 2019 as DPM database. You can install SQL Server on a remote server, or on the DPM server. The database must be installed and running before you install DPM. [Learn more](prepare-environment-for-dpm.md#sql-server-database).

::: moniker-end

::: moniker range="sc-dpm-1807"

## What's new in DPM 1807

DPM 1807 provides a number of bug fixes to improve the performance.

To view the list of bugs fixed and the installation instructions for DPM 1807, see [KB article 4339950](https://support.microsoft.com/help/4339950).

::: moniker-end

::: moniker range="sc-dpm-1801"

## New features in DPM 1801

System Center DPM 1801 supports [back up and restore of VMware virtual machines](https://blogs.technet.microsoft.com/dpm/2018/02/27/faster-vmware-backups-with-sc-1801-dpm/) (VMs), and extends the benefits of Modern Backup Storage to your VMware backups. For detailed information on how to back up VMware VMs, see [this article](back-up-vmware.md).

* Up to 50% storage savings
* Three times faster backups
* Workload-volume affinity

::: moniker-end

::: moniker range="sc-dpm-2016"

## New features in DPM 2016

The following features are either new to DPM, or are improved for DPM 2016.

- **Modern Backup Storage** -
Using Resilient File System (ReFS) block-cloning technology to store incremental backups, DPM 2016 improves storage utilization and performance. Backup storage grows and shrinks with the production data source. There is no over-allocation of storage.

- **Resilient change tracking (RCT)** -
DPM uses RCT (the native change tracking in Hyper-V), which removes the need for time-consuming consistency checks. RCT provides better resiliency than the change tracking provided by VSS snapshot-based backups. DPM also uses RCT for incremental backup. It identifies VHD changes for virtual machines, and transfers only those blocks that are indicated by the change tracker.

- **Continued protection during cluster aware updates** -
Windows Server 2016 comes with the cluster OS rolling update, where a cluster can be upgraded to Windows Server 2016 without bringing it down. DPM 2016 continues to protect VMs during the upgrade, maintaining the backup service level agreement (SLA).

- **Shielded VM Backups** -
Shielded VMs in Windows Server 2016 help protect sensitive VMs from inspection, tampering, and data theft by malware and malicious administrators.  DPM 2016 backups retain the protections provided by shielded VMs to ensure they can be recovered seamlessly and securely.

- **Hyper-V with Storage Spaces Direct** -
DPM recognizes and protects Hyper-V VMs deployed on Storage Spaces Direct, delivering seamless backup and recovery of VMs in disaggregated and hyper-converged scenarios.

- **Hyper-V with ReFS SOFS Cluster** -
DPM 2016 can back up Hyper-V VMs deployed on ReFS-based SOFS clusters. Backup and recovery of RCT-based VMs and non-RCT VMs is supported.

- **Upgrading a DPM production server to 2016 doesn't require a reboot** -
When you upgrade to DPM 2016, you are not required to reboot the production server. To avoid rebooting the production server, upgrade to DPM 2016 and upgrade the DPM agent on the production servers. Backups continue and you reboot the production server when you want.

## Modern Backup Storage

Modern Backup Storage is a feature that provides several benefits including:

### Improved storage savings

Modern Backup Storage achieves 30-40% storage savings using technologies such as Resilient File System (ReFS). Using ReFS volumes and storing backups on VHDXs means there are no Local Disk Manager (LDM) limits or storage over-allocations. DPM storage consumption is flexible: it grows and shrinks based on the production data source’s storage changes.

### Faster backups
DPM 2016 uses block cloning to store backups on ReFS volumes. Instead of using copy-on-write to store backups (which was used by VolSnap in DPM 2012 R2), DPM 2016's block cloning uses allocate-on-write. This change improves IOPS efficiency, making backups nearly 70% faster.

### Choose the volumes for your data source to increase storage efficiency
DPM's workload-aware storage feature decreases costs by providing flexible storage choices for a given data source. This means DPM can use expensive, high-performance disks for backing up high-IOPS workloads, such as SQL or SharePoint. Low performant storage can be used for reduced-IOPS workloads.

### Backup storage consumption in line with production data source
Without Logical Disk Manager (LDM) limits, data sources grow and shrink as needed, without the need for manual intervention. DPM doesn't need to allocate storage to data sources beforehand, and can dynamically allow the backups to adjust as needed, thus achieving higher efficiency with less storage required.


## Hyper-V protection improvements

The following information touches on the improvements to protecting VMs with DPM 2016.

### Resilient Change Tracking (RCT)
In Windows Server 2016, Hyper-V virtual hard disks have built-in change tracking. As a result, in the case of a Host outage, or VM migration, change-tracking is automatically preserved. With RCT, backups:
- **are more reliable**: consistency checks aren't required after VM migration,
- **are scalable**: more parallel backups and less storage overhead,
- **have improved performance**: lower impact on the production fabric and faster backup.

#### Enabling RCT VM backup

Hyper-V VMs deployed on Windows Server 2016 and protected using DPM 2016 have RCT by default. VMs deployed on Windows Server 2012 R2 or earlier do not support RCT. However, you can upgrade older VMs. To upgrade older VMs to enable RCT:


1. In Hyper-V Manager, shut down the virtual machine.

2. In Hyper-V Manager, select **Action** > **Upgrade Configuration Version**.

   If this option isn't available for the virtual machine, then it's already at the highest configuration version supported by the Hyper-V host. For additional information about checking or upgrading the virtual machine configuration version, see the article, [upgrading virtual machine version to Windows Server 2016](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/deploy/upgrade-virtual-machine-version-in-hyper-v-on-windows-or-windows-server/).

   If you want to use Windows PowerShell to upgrade the virtual machine configuration, run the following command where vmname is the name of the virtual machine.

   ```
   Update-VMVersion <vmname>
   ```

3. On the DPM 2016 server:
   - Stop protection of the VM and select **Retain Data**.
   - In the DPM 2016 Administrator Console, click **Protection** > on the tool ribbon, click **New** to start the Create Protection Wizard. Go through the wizard and select **Refresh** to update the data sources.
   - Select your VM and create a new protection group.
   - Delete the old VM's retained data once the retention range has expired.

This backs up RCT-enabled VMs deployed in various configurations. The following sections describe the supported scenarios:

#### Meet backup SLA during cluster operating system rolling upgrade

Cluster OS rolling upgrade is a feature of Windows Server 2016 used to upgrade the cluster nodes' operating system, from Windows Server 2012 R2 to Windows Server 2016, without stopping the Hyper-V or Scale-Out File Server (SOFS) workloads. Cluster OS rolling upgrade ensures protection is not interrupted during operating system upgrades. This sustained protection meets the backup SLA, reinforces continuity, and provides peace of mind for backup administrators. For detailed information on the cluster OS rolling upgrade process, see the article, [Cluster OS Rolling Upgrade Process](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade#cluster-os-rolling-upgrade-process).

To enable uninterrupted protection, run the following steps for each node:

1.	Drain Roles on the node.

    This puts the node in a paused state and automatically migrates any VM on that node to another cluster node.

2.	Restart the node.

3.	Evict the node.

4.	Install Windows Server 2016.

5.	Install the DPM agent.

6.	Add the node back to the cluster.

    This allows backups to occur without consistency checks, while keeping the cluster alive.

#### Seamless protection and recovery of Shielded VMs (vTPM-enabled VMs)

Trusted Platform Modules (TPM) are a chip in the motherboard of computers that help integrate cryptographic keys. These keys are used by BitLocker to protect the computer even if it is stolen. Virtual TPM (vTPM) is a feature in Windows Server 2016. With vTPM, you can use BitLocker and a virtual TPM chip to encrypt a VM, thereby protecting the VM. These VMs, called Shielded VMs, can only be run on healthy and approved hosts in the fabric.

DPM 2016 supports backup and recovery of Shielded VMs that have their VHDs/VHDXs protected with vTPM. Note that Item Level Recovery (ILR) and Alternate Location Recovery (ALR) to a location outside the guarded fabric is not available for this scenario.

#### Protecting VMs stored on Storage Spaces Direct

Storage Spaces Direct leverages the Storage Spaces feature introduced in Windows Server 2012 R2 which allows you to deploy highly available (HA) storage systems using local storage. Storage Spaces Direct leverages the local disks on hosts to provide a shared pool of clustered storage that can be used as primary storage for Hyper-V virtual machine files, or for secondary storage for Hyper-V Replica virtual machines files.
The primary use case for Storage Spaces Direct is private cloud storage, either on-premises for enterprises, or in hosted private clouds for service providers.
For more information about Storage Spaces Direct, see the article on [Storage Spaces Direct in Windows Server 2016](https://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).

DPM protects Hyper-V VMs that use Storage Spaces Direct. Most configurations are supported, including the backup of VMs using the [Storage Spaces Direct hyper-converged scenario](https://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct) with the Hyper-V (compute) and Storage Spaces Direct (storage) components on the same cluster. Note that backing up and restoring virtual machines running on a Windows Nano Server isn't supported.

#### Protecting VMs stored on ReFS-based SOFS clusters

DPM 2016 can back up VMs deployed on ReFS-based SOFS clusters.

To protect VMs on SOFS clusters, add the following machine accounts to the backup operator groups and share permissions.

  - If protecting a highly available (HA) VM, provide the machine account name of the host cluster and cluster nodes, and DPM server.
  - If protecting a non-HA VM, provide the machine name of the Hyper-V host and the DPM server.

To add the machine accounts to the backup operator groups, run the following steps for each node in the SOFS cluster:

1. Open the command prompt, and type, **lusrmgr.msc** to open Local Users and Groups.
2. In the Local Users and Groups dialog, click **Groups**.
3. In the list of groups, right-click **Backup Operators** and select **Properties**.

    The **Backup Operators Properties** dialog opens.
4. In the **Backup Operators Properties** dialog, click **Add**.
5. In the **Select Users, Computers, Services Accounts, or Groups** dialog, click **Object Types**.
    The **Object Types** dialog opens.
6. In the **Object Types** dialog, select **Computers** and click **OK**.
    The **Object Types** dialog closes.
7. In the **Select Users, Computers, Service Accounts, or Groups** dialog, enter the name of the server or cluster, and click **Check Names**.
8. Once you have identified the computers, restart the node.


To give permissions to the share

1. On a server where the SOFS/SMB share is hosted, open **Server Manager** > **File and Storage Services** > **Shares**.
2. Right click the VM storage share, and then click **Properties**.
4. In the **Properties** dialog, on the left navigation menu, click **Permissions**.
5. Click **Customize permissions** to open the Advanced Security Settings dialog.
6. On the **Permissions** tab, click **Add**.
7. Click **Select a Principal**.
8. In the **Select User, Computer, Services Account, or Group** dialog, click **Object Types**.
9. In the **Object Types** dialog, select **Computers**, and click **OK**.
10. In the **Select User, Computer, Service Account, or Group** dialog, enter the name of the Hyper-V node or cluster name you want to have permission.
11. Click **Check Names** to resolve the name, and click **OK**.
12. In the **Permission Entry for Share** dialog, select **Full Control**,  and click **OK**.
13. In the **Advanced Security Settings for Share** dialog, click the **Share** tab and repeat steps 6-11 for the **Share** tab instead of the **Permissions** tab.
14. When you are finished adding permissions for the servers, click **Apply**.

    This prepares the VMs on SOFS shares for the backup process.

::: moniker-end

## Next steps
- [Install DPM](install-dpm.md)
- [Upgrade your DPM installation](upgrade-dpm.md)
