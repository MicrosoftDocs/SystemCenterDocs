---
description: Descriptions of the new features in DPM 2016, including Modern DPM storage and improvements to Hyper-V protection.  
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


Before you begin, check the [Release Notes for System Center 2016](../../get-started/Release-Notes-for-System-Center-Technical-Preview-5.md) for last minute issues. System Center DPM 2016 adds improvements in three key areas: storage efficiency, performance, and security. Modern DPM Storage (MDS) takes advantage of improvements in Windows Server 2016, creating storage space savings of 30-40%. In addition to space savings, you can create storage and performance efficiency by using MDS to back up designated workloads to specific volumes. Improved DPM performance reduces I/O requirements up to 70%, which results in much faster backups. DPM 2016 supports shielded VMs which promises backup and recovery of critical VMs.

## New DPM 2016 features overview

The following features are either new to DPM, or are improved for DPM 2016.

- **Modern DPM Storage** -
Using Resilient File System (ReFS) block-cloning technology to store incremental backups, DPM 2016 dramatically improves storage utilization and performance. The storage consumed by backups grows and shrinks with the production data source, and there is no over-allocation of storage.

- **Resilient change tracking (RCT)** -
DPM uses RCT (the native change tracking in Hyper-V), which removes the need for time-consuming consistency checks. RCT provides better resiliency than the change tracking provided by VSS snapshot-based backups. DPM also uses RCT for incremental backup. It identifies VHD changes for virtual machines, and transfers only those blocks that are indicated by the change tracker.

- **Continued protection during cluster aware updates** -
Windows Server 2016 comes with the cluster OS rolling update, where a cluster can be upgraded to Windows Server 2016 without bringing it down. DPM 2016 continues to protect VMs during the upgrade, maintaining the backup service level agreement (SLA).

- **Secure VM Backups** -
Shielded VMs and Guarded Fabric in Windows Server 2016 provide the ability to secure VMs on compromised hosts.  DPM 2016 backups maintain the security provided by shielded VMs, which protects enterprise resources, and help recover those VMs securely and seamlessly.

- **Hyper-V with Storage Spaces Direct** -
DPM recognizes and protects Hyper-V VMs deployed on Storage Spaces Direct, delivering seamless backup and recovery of VMs in disaggregated and hyper-converged scenarios.

- **Hyper-V with ReFS SOFS Cluster** -
DPM 2016 can back up Hyper-V VMs deployed on ReFS-based SOFS clusters. Backup and recovery of RCT-based VMs and non-RCT VMs is supported.

- **Upgrading a DPM production server to 2016 doesn't require a reboot** -
When you upgrade to DPM 2016, you are not required to reboot the production server. To avoid rebooting the production server, upgrade to DPM 2016 and upgrade the DPM agent on the production servers. Backups continue and you reboot the production server when you want.

## Modern DPM Storage

Modern DPM Storage is a feature that provides several benefits including:

### Improved storage savings
Modern DPM Storage (MDS) achieves 30-40% storage savings using technologies such as Resilient File System (ReFS). Using ReFS volumes and storing backups on VHDXs means there are no Local Disk Manager (LDM) limits or storage over-allocations. DPM storage consumption is flexible: it grows and shrinks based on the production data source’s storage changes.

### Faster backups
DPM 2016 uses block cloning to store backups on ReFS volumes. Instead of using copy-on-write to store backups (which was used by VolSnap in DPM 2012 R2), DPM 2016's block cloning uses allocate-on-write. This change improves IOPS efficiency, making backups nearly 70% faster.

### Choose the volumes for your data source to increase storage efficiency
All storage is not the same. DPM's flexible storage feature decreases costs by providing flexible storage choices for a given data source. The flexible storage feature means DPM can use expensive, high-performance disks for backing up high-IOPS workloads, such as SQL or SharePoint. Low performant storage can be used for reduced-IOPS workloads.

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

Hyper-V VMs deployed on Windows Server 2016 and protected using DPM 2016 have RCT by default. VMs deployed on Windows Server 2012 R2 or earlier do not support RCT. However, you can upgrade older VMs.
To upgrade older VMs to enable RCT:
1. Shut down the virtual machine in Hyper-V Manager.
2. In Hyper-V Manager, select **Action** > **Upgrade Configuration Version**. If this option isn't available for the virtual machine, then it's already at the highest configuration version supported by the Hyper-V host. For additional information about checking or upgrading the virtual machine configuration version, see the article, [upgrading virtual machine version to Windows Server 2016](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/deploy/upgrade-virtual-machine-version-in-hyper-v-on-windows-or-windows-server.md).

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

Cluster OS rolling upgrade is a feature of Windows Server 2016 used to upgrade the cluster nodes' operating system, from Windows Server 2012 R2 to Windows Server 2016, without stopping the Hyper-V or Scale-Out File Server (SOFS) workloads. Cluster OS rolling upgrade ensures protection is not interrupted during operating system upgrades. This sustained protection meets the backup SLA, reinforces continuity, and provides peace of mind for backup administrators.

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
For more information about Storage Spaces Direct, see the article on [Storage Spaces Direct in Windows Server 2016](https://technet.microsoft.com/en-us/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).

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
