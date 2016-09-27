---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  markgalioto
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-09-26
title:  What's new in DPM in System Center 2016
ms.technology:  data-protection-manager
ms.assetid:  a5e81bf0-43a6-4099-af2e-dfb0c1aa7ed8
---

# What's new in DPM in System Center 2016

>Applies To: System Center 2016 - Data Protection Manager


Before you begin, check the [Release Notes for System Center 2016](../../get-started/Release-Notes-for-System-Center-Technical-Preview-5.md) for last minute issues. System Center DPM 2016 adds improvements in three key areas: storage efficiency, performance, and security. Modern DPM Storage (MDS) which takes advantage of storage improvements in Windows Server 2016, improves storage space savings 30-40%. In addition to space savings, you can create storage and performance efficiency by using MDS to back up certain workloads to specific volumes. DPM performance improves due to the 70% reduction in I/O requirements, resulting in much faster backups. DPM 2016 protects shielded VMs and Hyper-V VMs deployed on third-party NAS devices that support the SMB3 protocol.

## New DPM 2016 features overview

The following features are either new to DPM, or are improved for DPM 2016.

### Modern DPM Storage
By using Resilient File System (ReFS) block-cloning technology to store incremental backups, DPM 2016 dramatically improves storage utilization and performance. The storage consumed by backups grows and shrinks with the production data source, and there is no over-allocation of storage.

### Resilient change tracking (RCT)
DPM uses the native change tracking in Hyper-V, which removes the need for time-consuming consistency checks. RCT provides better resiliency than the change tracking provided by VSS snapshot-based backups. DPM also uses RCT for incremental backup. It identifies VHD changes for virtual machines, and transfers only those blocks that are indicated by the change tracker.

### Protect data sources in mixed-mode clusters
Windows Server 2016 comes with the cluster OS rolling update, where a cluster can be upgraded to Windows Server 2016 without bringing it down. DPM 2016 continues to protect VMs during the upgrade, maintaining the backup service level agreement (SLA).

### Secure VM Backups
Shielded VMs and Guarded Fabric in Windows Server 2016 provide the ability to secure VMs on compromised hosts.  DPM 2016 backups maintain the security provided by shielded VMs, which protects enterprise resources, and help recover those VMs securely and seamlessly.

### Storage Spaces Direct
Storage Spaces Direct leverages the Storage Spaces feature introduced in Windows Server 2012 R2 which allows you to deploy highly available (HA) storage systems using local storage. Storage Spaces Direct leverages the local disks on hosts to provide a shared pool of clustered storage that can be used as primary storage for Hyper-V virtual machine files, or for secondary storage for Hyper-V Replica virtual machines files.
The primary use case for Storage Spaces Direct is private cloud storage, either on-premises for enterprises, or in hosted private clouds for service providers.
For more information about Storage Spaces Direct, see the article on [Storage Spaces Direct in Windows Server 2016](https://technet.microsoft.com/en-us/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).

DPM protects Hyper-V VMs that use Storage Spaces Direct. Most configurations are supported, including the backup of VMs using the [Storage Spaces Direct hyper-converged scenario](https://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct) with the Hyper-V (compute) and Storage Spaces Direct (storage) components on the same cluster, and the backup of virtual machines using the Storage Spaces Direct disaggregated scenario which separates out  Hyper-V servers (compute) into a separate cluster from the Storage Spaces Direct servers (storage). In this configuration virtual machines are configured to store their files on the Scale-Out File Server (SOFS) which is accessed through the network using the SMB3 protocol. In all cases virtual machine backup and recovery is seamless with no change in user experience. Note that backing up and restoring virtual machines running on a Windows Nano Server isn't supported.


### Hyper-V with ReFS SOFS Cluster
DPM 2016 can back up Hyper-V VMs deployed on ReFS-based SOFS clusters. Backup and recovery of both RCT-based VMs, and non-RCT VMs is supported.

### DPM 2016 upgrades do not require rebooting the production server
When you upgrade to DPM 2016, you are not required to reboot the production server. To avoid rebooting the production server, upgrade to DPM 2016 and upgrade the DPM agent on the production servers. Backups will continue and you can reboot the production server when you want.

## Modern DPM Storage

Modern DPM Storage is a feature that provides several benefits including:

### Improved storage savings
Modern DPM Storage (MDS) achieves 30-40% storage savings using technologies such as ReFS. Using ReFS volumes and storing backups on VHDXs means there are no Local Disk Manager (LDM) limits or storage over-allocations. DPM storage consumption is flexible - it grows and shrinks based on the production data source’s storage changes.

### Faster backups
DPM 2016 uses block cloning to store backups on Resilient File System (ReFS) volumes. Instead of using copy-on-write to store backups - which was used in DPM 2012 R2, DPM 2016's block cloning uses allocate-on-write. This change improves IOPS efficiency making backups nearly 70% faster.

### Choose the volumes for your data source to increase storage efficiency
All storage is not the same. DPM’s flexible storage feature saves costs by providing the flexibility to choose appropriate storage for a given data source. This means that DPM can use the expensive, high-performance disks for backing up workloads which require high IOPS, such as SQL or SharePoint. Low performant storage can be used for other workloads with reduced IOPS loads.

### Backup storage consumption in line with production data source
No need for over-allocation and absence of LDM limits allows the data sources to grow and shrink as many times as needed, without the need for manual intervention. Hence, DPM does not need to allocate storage to data sources beforehand, and can dynamically allow the backups to adjust as needed, thus achieving higher efficiency with lesser storage requirement.


## Hyper-V protection improvements

With Windows Server 2016, Hyper-V virtual hard disks already have built-in change tracking. As a result, in the case of a Host outage, or VM migration, change-tracking is automatically preserved. With RCT, backups:
- **are more reliable**: no requirement for consistency checks after VM migration,
- **are scalable**: more parallel backups and less storage overhead,
- **have improved performance**: lower impact on the production fabric and faster backup.

### Enabling RCT VM backup

Hyper-V VMs deployed on Windows Server 2016 and protected using DPM 2016 have Resilient Change Tracking (RCT) by default.
To upgrade older (previous versions of upgraded...) VMs to enable RCT:
1. Upgrade the Hyper-V host to Windows Server 2016.
2. To prepare the VM for RCT:
  - On the DPM 2012 R2 server, stop protection of the VM with Retain Data.
  - Migrate the VM to Windows 2016
  - Use the following PowerShell command to upgrade the VM configuration to Windows 2016 :
  ```
  Update-VMVersion <vmname>
  ```
  - In the DPM 2016 Administrator Console, click the **Protection** menu > on the tool ribbon, click **New** to start the Create Protection Wizard, select **Refresh** to update the data sources.
  - Select your VM and create a new protection group.

This backs up RCT-enabled VMs deployed in various configurations. The following sections describe the supported scenarios:

#### Meet Backup SLA during Cluster Operating System Rolling Upgrade

Cluster OS rolling upgrade is a feature of Windows Server 2016 used to upgrade the cluster nodes' operating system from Windows Server 2012 R2 to Windows Server 2016 without stopping the Hyper-V or Scale-Out File Server workloads. Cluster OS rolling upgrade ensures protection is not interrupted during operating system upgrades. This sustained protection meets the backup SLA, reinforces continuity, and provides peace of mind for backup administrators.

To enable uninterrupted protection, run the following steps for each node:

1.	Drain Roles on the node.

    This puts the node in paused state and automatically migrates any VM on that node to another cluster node.

2.	Restart the node.

3.	Evict the node.

4.	Install Windows Server 2016.

5.	Install the DPM agent.

6.	Add the node back to the cluster.

    This allows backups to occur without consistency checks, while keeping the cluster alive.

#### Seamless protection and recovery of Shielded VMs (vTPM-enabled VMs)

Trusted Platform Modules (TPM) are generally a chip in the motherboard of computers that create encryption keys to create cryptographic keys. These keys are used by BitLocker to protect the computer even if it is stolen. Virtual TPM (vTPM) is a feature in Windows Server 2016. With vTPM, you can use BitLocker and a virtual TPM chip to encrypt a VM, thereby protecting the VM. These VMs, called Shielded VMs, can only be run on healthy and approved hosts in the fabric.

DPM 2016 supports backup and recovery of Shielded VMs that have their VHDs/VHDXs protected with vTPM, providing a more secure environment for critical data. Please note that ILR is not available for this scenario.

#### Protecting VMs stored on Storage Spaces Direct

Windows Server 2016 comes with [Storage Spaces Direct (S2D)](http://technet.microsoft.com/library/mt126109.aspx), allowing the creation of highly available and scalable storage systems with local storage, eliminating the need for a shared storage and related complexities. Storage Spaced Direct integrates features such as SoFS, CSVFS, Storage Spaces, and Failover Clustering, and can be deployed as either disaggregated or hyper-converged configurations.
DPM recognizes and protects Hyper-V VMs deployed on any S2D configuration, delivering seamless backup and recovery of Virtual Machines in both the scenarios.

#### Protecting VMs stored on ReFS-based SOFS clusters

DPM 2016 can back up VMs deployed on ReFS-based SOFS clusters.

To protect VMs on SOFS clusters, add the following machine accounts to the backup operator groups and share permissions.

  - If protecting a HA VM, use host cluster name and cluster nodes.
  - If the VM is not a HA VM, use the Hyper-v host.
  - DPM server

Add the machine accounts to the backup operator groups. Run the following steps for each node in the SOFS cluster:

1. Open the command line, run **lusrmgr.msc** to open Local Users and Groups.
2. In the Local Users and Groups dialog, click **Groups**.
3. In the list of groups, right-click **Backup Operators** and select **Properties**.
4. In the **Backup Operations Properties** dialog, click **Add**
5. In the **Select Users, Computers, Services Accounts, or Groups** dialog, click **Object Types** and select **Computers** for the type of object you want to find.
6. Enter the name of the server or cluster.
7. Restart the node.


Give permissions to the share

1. On a server where the SOFS/SMB share is hosted, open **Server Manager** > **File and Storage Services** > **Shares**.
3. Right click the share with vm storage, and click **Properties**.
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
