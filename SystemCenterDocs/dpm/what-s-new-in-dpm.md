---
description: Descriptions of the new features in System Center DPM
ms.topic: article
ms.service: system-center
ms.date: 11/01/2024
title: What's new in System Center DPM
ms.subservice: data-protection-manager
ms.assetid: a5e81bf0-43a6-4099-af2e-dfb0c1aa7ed8
author: jyothisuri
ms.author: jsuri
ms.custom: UpdateFrequency.5, intro-whats-new, engagement-fy23, engagement-fy24
---

# What's new in System Center Data Protection Manager

::: moniker range="sc-dpm-2025"

[!INCLUDE [discontinue-spf-2025.md](../includes/discontinue-spf-2025.md)]

This article gives details of the new features supported in System Center - Data Protection Manager (DPM) 2025.

[!INCLUDE [whats-new-dpm-2025.md](../includes/whats-new-dpm-2025.md)]

::: moniker-end

::: moniker range="sc-dpm-2022"

This article gives details of the new features supported in System Center - Data Protection Manager (DPM) 2022. It also provides details of the new features in DPM 2022 UR1 and UR2.

[!INCLUDE [whats-new-dpm-2022.md](../includes/whats-new-dpm-2022.md)]

::: moniker-end

::: moniker range="sc-dpm-2019"

This article provides details of the new features supported in System Center - Data Protection Manager (DPM) and also includes the new features/feature updates supported in [DPM 2019](#new-features-in-dpm-2019) , [2019 UR1](#new-features-in-dpm-2019-ur1), [2019 UR2](#new-features-in-dpm-2019-ur2), [2019 UR3](#new-features-in-dpm-2019-ur3), [2019 UR4](#new-features-in-dpm-2019-ur4), [2019 UR5](#new-features-in-dpm-2019-ur5) and [2019 UR6](#new-features-in-dpm-2019-ur6).

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

You can install SQL Server on a remote server or on the DPM server. The database must be installed and running before you install DPM.

### Support for newer workloads backups

With DPM 2019, you can back up newer versions of workloads, as following:

- Hyper-V VMs 2019
- Windows Server 2019
- Exchange 2019
- SharePoint 2019
- VMware [vSphere 6.7 and 7.0](back-up-vmware.md#vmware-vsphere-67-and-70)
- System Center Virtual Machine Manager 2019. [Learn more.](dpm-protection-matrix.md)

### Faster backups with Tiered storage using SSDs

DPM 2016 introduced [Modern Backup Storage](./add-storage.md?preserve-view=true&view=sc-dpm-2016), improving storage utilization and performance. MBS uses ReFS as the underlying file system and is designed to make use of hybrid storage such as tiered storage.

To achieve the scale and performance by MBS, we recommend using a small percentage (4% of the overall storage) of flash storage (SSD) with DPM 2019 as a tiered volume in combination with DPM HDD storage. DPM 2019 with tiered storage delivers 50-70% faster backups. [Learn more](add-storage.md#set-up-mbs-with-tiered-storage).

### Support for Central Monitoring

With DPM 2019, all DPM-A customers (customer connected to Azure) have the flexibility of using Central Monitoring, a monitoring solution provided by Microsoft Azure Backup.

You can monitor both on-premises and cloud backups, using Log Analytics with central monitoring capability.  [Learn more](monitor-dpm.md#central-monitoring).

### VMware backup to tape

For long-term retention on VMware backup data on-premises, you can now enable VMware backups to tape. The backup frequency can be selected based on the retention range (which will vary from 1-99 years) on tape drives. The data on tape drives could be both compressed and encrypted.

DPM 2019 supports both Original Location Recovery (OLR) and Alternate Location Recovery (ALR) for restoring the protected VM. [Learn more](back-up-vmware.md).

### VMware parallel backups

With DPM 2019, all your VMware VMs back up within a single protection group would be parallel, leading to 25% faster VM backups.

With earlier versions of DPM, parallel backups were performed only across protection groups. With DPM 2019, VMware delta replication jobs run in parallel. By default, the number of jobs to run in parallel is set to 8. [Learn more](back-up-vmware.md#vmware-parallel-backups).

## New features in DPM 2019 UR1

See the following sections for information about the new features/feature updates supported in DPM 2019 UR1.

For issues fixed and the installation instructions for UR1, see [KB article for Update Rollup 1](https://support.microsoft.com/help/4533416/update-rollup-1-for-system-center-2019-data-protection-manager).

### Support for ReFS volumes

With DPM 2019 UR1, you can back up the ReFS volumes and workloads deployed on the ReFS volumes. You can back up the following workloads:

 - **Operating System (64 bit)**: Windows Server 2019, 2016, 2012 R2, 2012.
 - **SQL Server**: SQL Server 2019, SQL Server 2017, 2016.
 - **Exchange**: Exchange 2019, 2016.
 - **SharePoint**: SharePoint 2019, 2016 with latest SP.

 > [!NOTE]
 > Backup of Hyper-V VMs stored on ReFS volume is supported with DPM 2019 RTM.
 >
> We have identified a few issues with the backup of deduplicated ReFS volumes. We are working on fixing these and will update this section as soon as we have a fix available. Until then, we are removing the support for backup of deduplicated ReFS volumes from 2019 UR1.

### Windows Server Core support

You can install DPM 2019 UR1 on Windows Server Core 2019 and 2016.

> [!NOTE]
> Installation of MARS agent on Windows Server Core isn't supported. With this limitation, DPM cannot be connected to Azure Recovery Services Vault when it's installed on Windows Server Core.

### Disk exclusion for VMware VM backup

With DPM 2019 UR1, you can exclude the specific disk from a VMware VM backup. [Learn more](back-up-vmware.md).

### Support for another layer of authentication to delete online backup

With DPM 2019 UR1, another layer of authentication is added for critical operations. You'll be prompted to enter a security PIN when you perform *Stop Protection* with *Delete data* operations.

### New cmdlet parameter

DPM 2019 UR1 includes a new parameter **[-CheckReplicaFragmentation]**. The new parameter calculates the fragmentation percentage for a replica and is included in the **Copy-DPMDatasourceReplica** cmdlet.

## New features in DPM 2019 UR2

See the following sections for information about the new features/feature updates supported in DPM 2019 UR2.

For issues fixed in UR2 and the installation instructions for UR2, see the [KB article](https://support.microsoft.com/help/4563392/update-rollup-2-for-system-center-2019-data-protection-manager).

### Support for SQL Server Failover Cluster Instance (FCI) using Cluster Shared Volume (CSV)

DPM 2019 UR2 supports SQL Server Failover Cluster Instance (FCI) using Cluster Shared Volume (CSV). With CSV, the management of your SQL Server Instance is simplified. You'll be able to manage the underlying storage from any node as there's an abstraction to which node owns the disk. [Learn more](back-up-sql-server.md).

### Optimized Volume-to-Volume Migration

DPM 2019 UR2 supports optimized Volume-to-Volume Migration. The optimized Volume-to-Volume Migration allows you to move data sources to the new volume faster. The enhanced migration process migrates only active backup copy (Active Replica) to the new volume. All the new recovery points are created on the new volume while the existing recovery points are maintained on the existing volume and are purged as per the retention policy. [Learn more](volume-to-volume-migration.md).

### Offline Backup using Azure Data Box (Preview)

DPM 2019 UR2 supports Offline backup using Azure Data Box. With [Microsoft Azure Data Box](https://azure.microsoft.com/services/databox/) integration, you can overcome the challenge of moving terabytes of backup data from on-premises to Azure storage. Azure Data Box saves the effort required to procure your own Azure-compatible disks and connectors or to provision temporary storage as a staging location. Microsoft also handles the end-to-end transfer logistics, which you can track through the Azure portal. [Learn more](offline-seeding-azure-data-box.md).

### SQL Server 2019 support as DPM database

DPM 2019 supports SQL server 2019 as DPM database. You can install SQL Server on a remote server or on the DPM server. The database must be installed and running before you install DPM. [Learn more](prepare-environment-for-dpm.md#sql-server-database).

## New features in DPM 2019 UR3

DPM 2019 UR3 has only bug fixes. See [the KB article](https://support.microsoft.com/topic/fa5eb310-1886-43fb-be5d-c7829bfaf63d) for details about the issues fixed.

## New features in DPM 2019 UR4

See the following sections for information about the new features/feature updates supported in DPM 2019 UR4.

For issues fixed in UR4 and the installation instructions for UR4, see [the KB article](https://support.microsoft.com/topic/update-rollup-4-for-system-center-2019-data-protection-manager-1f4a13ed-9750-49bb-b312-9def71bc31da).

### Removed File Catalog dependency for online backup of file/folder workloads

DPM 2019 UR4 removes the dependency on File Catalog, which was needed to restore individual files and folders from the online recovery points. DPM now uses the iSCSI mount method to provide individual file restore. This also improves backup time as the upload of file catalog metadata isn't needed anymore.

### Private endpoint support

With DPM 2019 UR4, you can use a private endpoint to take online backup to Azure Backup Recovery Services vault. [Learn more](/azure/backup/private-endpoints-overview).

### Improvements VHDX mounting and unmounting

Improvements done for VHDX file mounting and unmounting. To mount or unmount VHDX files, we now use Win32 APIs by default. This is a change from our previous approach, which leveraged WMI. If you want to continue using the old (WMI) approach, see  this [documentation](/system-center/dpm/dpm-support-issues?view=sc-dpm-2019&preserve-view=true).

### Improved DPM reliability after DPM agent uninstallation 

With DPM 2019 UR4, you can restore previously backed up data even after DPM agent uninstallation.

## New features in DPM 2019 UR5

See the following sections for information about the new features/feature updates supported in DPM 2019 UR5.

For issues fixed and the installation instructions for UR5, see the [KB article](https://support.microsoft.com/help/5024231).

### Support for SQL Server 2022

DPM 2019 UR5 supports backup of SQL Server 2022. [Learn more](/system-center/dpm/dpm-protection-matrix?view=sc-dpm-2019&preserve-view=true).

### Back up support for Windows Server 2022

DPM 2019 UR5 supports backup of Windows Server 2022. [Learn more](/system-center/dpm/dpm-protection-matrix?view=sc-dpm-2019&preserve-view=true).

### End of support for vSphere 5.5

vSphere 5.5 has reached [end of general support](https://blogs.vmware.com/vsphere/2018/02/vsphere-5-5-vsan-5-5-end-general-support-reminder.html), DPM 2019 UR5 and later don't support backups for VMware VMs on vSphere 5.5. Ensure to upgrade to newer vSphere versions.

### Support for vSphere 7.0

DPM 2019 UR5 support backups for VMware VMs on vSphere 7.0. [Learn more](/system-center/dpm/back-up-vmware?view=sc-dpm-2019&preserve-view=true).

### Support for Microsoft 365 SMTP

DPM 2019 UR5 supports sending alert and report emails using Microsoft 365 SMTP directly without a relay agent. [Learn more](/system-center/dpm/monitor-dpm?view=sc-dpm-2019#configure-email-for-dpm&preserve-view=true).

### Increase maximum parallel online backups

With DPM 2019 UR5 and MARS agent version 9249 and later, you can increase the number of maximum parallel online backup jobs from the default eight to a configurable number using the following registry keys (if your underlying hardware and network bandwidth can support it).
  
The following example increases the limit to 12 jobs:

```
[HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\DbgSettings\OnlineBackup]
“MaxParallelBackupJobs”=dword:0000000C 

[HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft Data Protection Manager\Configuration\DPMTaskController\MaxRunningTasksThreshold] 
"6e7c76f4-a832-4418-a772-8e58fd7466cb"=dword:0000000C
```

## New features in DPM 2019 UR6

See the following sections for information about the new features/feature updates supported in DPM 2019 UR6.

For issues fixed and the installation instructions for UR6, see [KB article](https://support.microsoft.com/help/5035307).  

### Support for Windows and Basic SMTP Authentication for DPM email reports and alerts  

DPM 2019 UR6 supports Windows and Basic SMTP authentication to send reports and alerts via email. [Learn more](/system-center/dpm/monitor-dpm).

>[!NOTE]
>If you have been using M365 SMTP with DPM 2019 UR5, you must re-enter the credentials using Basic Authentication.

### Experience improvements for DPM backups to Azure

DPM 2019 UR6 supports listing of online recovery points for a data source along with the expiry time. Right-click a data source and select **List recovery points** to view the list of recovery points along with their expiration dates.

DPM 2019 UR6 supports stopping protection and retaining data by the policy duration for immutable vaults directly from the UI. This helps you save backup costs when stopping protection for a data source backed up to an immutable vault. [Learn more](/azure/backup/backup-azure-security-feature#immutability-support).

::: moniker-end

::: moniker range="sc-dpm-2016"

## New features in DPM 2016

The following features are either new to DPM or are improved for DPM 2016.

- **Modern Backup Storage** -
Using Resilient File System (ReFS) block-cloning technology to store incremental backups, DPM 2016 improves storage utilization and performance. Backup storage grows and shrinks with production data source. There's no over-allocation of storage.

- **Resilient change tracking (RCT)** -
DPM uses RCT (the native change tracking in Hyper-V), which removes the need for time-consuming consistency checks. RCT provides better resiliency than the change tracking provided by VSS snapshot-based backups. DPM also uses RCT for incremental backup. It identifies VHD changes for virtual machines and transfers only those blocks that are indicated by the change tracker.

- **Continued protection during cluster aware updates** -
Windows Server 2016 comes with the cluster OS rolling update, where a cluster can be upgraded to Windows Server 2016 without bringing it down. DPM 2016 continues to protect VMs during the upgrade, maintaining the backup service-level agreement (SLA).

- **Shielded VM Backups** -
Shielded VMs in Windows Server 2016 help protect sensitive VMs from inspection, tampering, and data theft by malware and malicious administrators. DPM 2016 backups retain the protections provided by shielded VMs to ensure they can be recovered seamlessly and securely.

- **Hyper-V with Storage Spaces Direct** -
DPM recognizes and protects Hyper-V VMs deployed on Storage Spaces Direct, delivering seamless backup and recovery of VMs in disaggregated and hyper-converged scenarios.

- **Hyper-V with ReFS SOFS Cluster** -
DPM 2016 can back up Hyper-V VMs deployed on ReFS-based SOFS clusters. Backup and recovery of RCT-based VMs and non-RCT VMs is supported.

- **Upgrading a DPM production server to 2016 doesn't require a reboot** -
When you upgrade to DPM 2016, you aren't required to reboot the production server. To avoid rebooting the production server, upgrade to DPM 2016 and upgrade the DPM agent on the production servers. Backups continue and you reboot the production server when you want.

### Modern Backup Storage

Modern Backup Storage is a feature that provides several benefits including:

#### Improved storage savings

Modern Backup Storage achieves 30-40% storage savings using technologies such as Resilient File System (ReFS). Using ReFS volumes and storing backups on VHDXs means there are no Local Disk Manager (LDM) limits or storage over-allocations. DPM storage consumption is flexible: it grows and shrinks based on the production data source’s storage changes.

#### Faster backups

DPM 2016 uses block cloning to store backups on ReFS volumes. Instead of using copy-on-write to store backups (which was used by VolSnap in DPM 2012 R2), DPM 2016's block cloning uses allocate-on-write. This change improves IOPS efficiency, making backups nearly 70% faster.

#### Choose the volumes for your data source to increase storage efficiency

DPM's workload-aware storage feature decreases costs by providing flexible storage choices for a given data source. This means DPM can use expensive, high-performance disks for backing up high-IOPS workloads, such as SQL or SharePoint. Low-performance storage can be used for reduced-IOPS workloads.

#### Back up storage consumption in line with production data source

Without Logical Disk Manager (LDM) limits, data sources grow and shrink as needed, without the need for manual intervention. DPM doesn't need to allocate storage to data sources beforehand and can dynamically allow the backups to adjust as needed, thus achieving higher efficiency with less storage requirement.

### Hyper-V protection improvements

The following information touches on the improvements for protecting VMs with DPM 2016.

#### Resilient Change Tracking (RCT)

In Windows Server 2016, Hyper-V virtual hard disks have built-in change tracking. As a result, in case of a host outage or VM migration, change-tracking is automatically preserved. With RCT, backups:
- **are more reliable**: Consistency checks aren't required after VM migration.
- **are scalable**: More parallel backups and less storage overhead.
- **have improved performance**: Lower impact on the production fabric and faster backup.

##### Enabling RCT VM backup

Hyper-V VMs deployed on Windows Server 2016 and protected using DPM 2016 have RCT by default. VMs deployed on Windows Server 2012 R2 or earlier don't support RCT. However, you can upgrade older VMs. To upgrade older VMs to enable RCT:

1. In Hyper-V Manager, shut down the virtual machine.

2. In Hyper-V Manager, select **Action** > **Upgrade Configuration Version**.

   If this option isn't available for the virtual machine, then it's already at the highest configuration version supported by the Hyper-V host. For more information about checking or upgrading the virtual machine configuration version, see the article, [upgrading virtual machine version to Windows Server 2016](/windows-server/virtualization/hyper-v/deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server).

   If you want to use Windows PowerShell to upgrade the virtual machine configuration, run the following command where vmname is the name of the virtual machine.

   ```powershell
   Update-VMVersion <vmname>
   ```

3. On the DPM 2016 server:
   - Stop protection of the VM and select **Retain Data**.
   - In the DPM 2016 Administrator Console, select **Protection** > on the tool ribbon, select **New** to start the Create Protection Wizard. Go through the wizard and select **Refresh** to update the data sources.
   - Select your VM and create a new protection group.
   - Delete the old VM's retained data once the retention range has expired.

This backs up RCT-enabled VMs deployed in various configurations. The following sections describe the supported scenarios:

##### Meet backup SLA during cluster operating system rolling upgrade

Cluster OS rolling upgrade is a feature of Windows Server 2016 used to upgrade the cluster nodes' operating system, from Windows Server 2012 R2 to Windows Server 2016, without stopping the Hyper-V or Scale-Out File Server (SOFS) workloads. Cluster OS rolling upgrade ensures protection isn't interrupted during operating system upgrades. This sustained protection meets the backup SLA, reinforces continuity, and provides peace of mind for backup administrators. For detailed information on the cluster OS rolling upgrade process, see the article, [Cluster OS Rolling Upgrade Process](/windows-server/failover-clustering/cluster-operating-system-rolling-upgrade#cluster-os-rolling-upgrade-process).

To enable uninterrupted protection, run the following steps for each node:

1. Drain Roles on the node.

    This puts the node in a paused state and automatically migrates any VM on that node to another cluster node.

2. Restart the node.

3. Evict the node.

4. Install Windows Server 2016.

5. Install the DPM agent.

6. Add the node back to the cluster.

    This allows backups to occur without consistency checks while keeping the cluster alive.

##### Seamless protection and recovery of Shielded VMs (vTPM-enabled VMs)

Trusted Platform Module (TPM) is a chip in the motherboard of a computer that helps to integrate cryptographic keys. These keys are used by BitLocker to protect the computer even if it's stolen. Virtual TPM (vTPM) is a feature in Windows Server 2016. With vTPM, you can use BitLocker and a virtual TPM chip to encrypt a VM, thereby protecting the VM. These VMs, called Shielded VMs, can only be run on healthy and approved hosts in the fabric.

DPM 2016 supports the backup and recovery of Shielded VMs that have their VHDs/VHDXs protected with vTPM. Note that Item Level Recovery (ILR) and Alternate Location Recovery (ALR) to a location outside the guarded fabric isn't available for this scenario.

##### Protecting VMs stored on Storage Spaces Direct

Storage Spaces Direct leverages the Storage Spaces feature introduced in Windows Server 2012 R2, which allows you to deploy highly available (HA) storage systems using local storage. Storage Spaces Direct leverages the local disks on hosts to provide a shared pool of clustered storage that can be used as primary storage for Hyper-V virtual machine files or for secondary storage for Hyper-V Replica virtual machine files.
The primary use case for Storage Spaces Direct is private cloud storage, either on-premises for enterprises or in hosted private clouds for service providers.
For more information about Storage Spaces Direct, see the article [Storage Spaces Direct in Windows Server 2016](/windows-server/storage/storage-spaces/storage-spaces-direct-overview).

DPM protects Hyper-V VMs that use Storage Spaces Direct. Most configurations are supported, including the backup of VMs using the [Storage Spaces Direct hyper-converged scenario](/windows-server/storage/storage-spaces/deploy-storage-spaces-direct) with the Hyper-V (compute) and Storage Spaces Direct (storage) components on the same cluster. Note that backing up and restoring virtual machines running on a Windows Nano Server isn't supported.

##### Protecting VMs stored on NTFS and ReFS-based SOFS clusters

DPM 2016 can back up VMs deployed on both NTFS and ReFS-based SOFS clusters.

To protect VMs on SOFS clusters, add the following machine accounts to the backup operator groups and share permissions:

  - If protecting a highly available (HA) VM, provide the machine account name of the host cluster and cluster nodes and the DPM server.
  - If protecting a non-HA VM, provide the machine name of the Hyper-V host and the DPM server.

To add the machine accounts to the backup operator groups, run the following steps for each node in the SOFS cluster:

1. Open the command prompt, and type **lusrmgr.msc** to open Local Users and Groups.
2. In the Local Users and Groups dialog, select **Groups**.
3. In the list of groups, right-click **Backup Operators** and select **Properties**.

    The **Backup Operators Properties** dialog opens.
4. In the **Backup Operators Properties** dialog, select **Add**.
5. In the **Select Users, Computers, Services Accounts, or Groups** dialog, select **Object Types**.
    The **Object Types** dialog opens.
6. In the **Object Types** dialog, select **Computers** and select **OK**.
    The **Object Types** dialog closes.
7. In the **Select Users, Computers, Service Accounts, or Groups** dialog, enter the name of the server or cluster and select **Check Names**.
8. Once you've identified the computers, restart the node.

To give permissions to the share

1. On a server where the SOFS/SMB share is hosted, open **Server Manager** > **File and Storage Services** > **Shares**.
2. Right-click the VM storage share and then select **Properties**.
4. In the **Properties** dialog, on the left navigation menu, select **Permissions**.
5. Select **Customize permissions** to open the Advanced Security Settings dialog.
6. On the **Permissions** tab, select **Add**.
7. Select **Select a Principal**.
8. In the **Select User, Computer, Services Account, or Group** dialog, select **Object Types**.
9. In the **Object Types** dialog, select **Computers** and select **OK**.
10. In the **Select User, Computer, Service Account, or Group** dialog, enter the name of the Hyper-V node or cluster name you want to have permission for.
11. Select **Check Names** to resolve the name and select **OK**.
12. In the **Permission Entry for Share** dialog, select **Full Control**  and select **OK**.
13. In the **Advanced Security Settings for Share** dialog, select the **Share** tab and repeat steps 6-11 for the **Share** tab instead of the **Permissions** tab.
14. When you've finished adding permissions for the servers, select **Apply**.

    This prepares the VMs on SOFS shares for the backup process.

## New features in DPM 2016 UR10 Hotfix

DPM 2016 UR10 Hotfix contains the enhancement below to improve backup times. For more information and the installation instructions, see the [KB article](https://support.microsoft.com/help/5031798).

### Removed File Catalog dependency for online backup of file/folder workloads

This update rollup hotfix removes the dependency on File Catalog (list of files in a recovery point, maintained in the cloud), which was needed to restore individual files and folders from the Online recovery points. With this hotfix, DPM 2016 now uses a modern iSCSI mount method to provide individual file restoration.

The new method has the following advantages:

- Reduces backup time up to 15% since file catalog metadata (list of files in a recovery point) isn't generated during backup.

- Item level recovery errors due to inconsistent file catalog metadata is avoided, since iSCSI mounts are used.

- After the recovery point is mounted, file browsing during item level recovery is faster for recovery points with many files and folders.

We recommended you to update your DPM 2016 installation to Hotfix for Update Rollup 10 to benefit from the enhancement. Ensure that you also [update your MARS Agent](/azure/backup/upgrade-mars-agent) to the latest version (2.0.9262.0 or later).

::: moniker-end

## Next steps

- [Install DPM](install-dpm.md)
- [Upgrade your DPM installation](upgrade-dpm.md)
- [Know about deploying and managing Update Rollups](update-rollups.md)
