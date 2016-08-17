---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  markgalioto
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-08-17
title:  What's new in DPM in System Center 2016
ms.technology:  data-protection-manager
ms.assetid:  a5e81bf0-43a6-4099-af2e-dfb0c1aa7ed8
---

# What's new in DPM in System Center 2016

>Applies To: System Center 2016 Technical Preview - Data Protection Manager


Before you begin, check the [Release Notes for System Center Technical Preview 5](../../get-started/Release-Notes-for-System-Center-Technical-Preview-5.md) for last minute issues. System Center DPM 2016 adds improvements in three key areas: storage efficiency, performance, and security. Modern DPM Storage (MDS) achieves 30-40% improvements in storage space requirement. The flexible storage feature, which allows selection of volumes for backing up certain workloads, makes storage and performance more efficient. Performance is also improved since there is a 70% reduction in I/O requirements, resulting in much faster backups. With support for Shielded VMs, DPM promises secure and seamless backups, and recovery of critical VMs. DPM 2016 adds support for protecting Hyper-V VMs deployed on SMBv3-compliant, 3rd Party NAS devices.

Here is an overview of the new DPM 2016 features:


## Modern DPM Storage
DPM 2016 achieves huge storage and performance improvements by storing incremental backups using ReFS Block Cloning technology.  Hence, the storage consumed by backups grows and shrinks as many times as needed, with the production data source, and there is no more over-allocation of storage.

## Protect data sources in mixed-mode clusters
Windows Server Technical Preview introduced [rolling upgrade support for clusters](https://technet.microsoft.com/en-us/windows-server-docs/storage/what-s-new-in-file-and-storage-services-in-windows-server-2016-technical-preview#a-name-bkmk-dedup5-a-support-for-cluster-rolling-upgrades), which means that in a cluster you can deploy servers running both Windows Server 2012 R2 and Windows Server Technical Preview. DPM can protect data sources in these mixed clusters, and will protect them seamlessly and without interruption during a cluster upgrade. Note that DPM doesn't support backup and recovery of data from Windows Nano Server.

## Resilient change tracking (RCT)
Hyper-V backup has been enhanced with resilient change tracking (RCT). DPM relies on Hyper-V's native change tracking, which removes the need for time-consuming consistency checks. RCT provides better resiliency than the change tracking provided by VSS snapshot-based backups. DPM also uses RCT for incremental backup. It identifies VHD changes for virtual machines, and transfers only those blocks that are indicated by the change tracker.

## Uninterrupted Protection during Cluster-Aware Updates
Windows 2016 comes with the Cluster OS Rolling update, where a cluster can be upgraded to Windows 2016 without bringing it down. DPM 2016 backs up VMs during the upgrade, maintaining the backup SLA.

## Secure VM Backups
Shielded VMs and Guarded Fabric in Windows 2016 provide the ability to secure VMs from compromised hosts.  DPM 2016 backups maintain the security provided by shielded VMs, which protects enterprise resources, and help recover those VMs securely and seamlessly.

## Storage Spaces Direct
Storage Spaces Direct (S2D) leverages the Storage Spaces feature that was introduced in Windows Server 2012 R2, without the need for shared storage, which allows you to deploy highly available (HA) storage systems using local storage. Storage Spaces Direct leverages the local disks on hosts to provide a shared pool of clustered storage that can be used as primary storage for Hyper-V virtual machine files, or for secondary storage for Hyper-V Replica virtual machines files.
 The primary use case for Storage Spaces Direct is private cloud storage, either on-prem for enterprises, or in hosted private clouds for service providers.
 Get an [overview](https://technet.microsoft.com/en-us/windows-server-docs/storage/storage-spaces/storage-spaces-direct-in-windows-server-2016-technical-preview).

DPM protects Hyper-V virtual machines that use  Storage Spaces Direct. Most configurations are supported, including the backup of virtual machines using the S2D hyper-converged scenario with the Hyper-V (compute) and Storage Spaces Direct (storage) components on the same cluster, and the backup of virtual machines using the S2D disaggregated scenario which separates out  Hyper-V servers (compute) into a separate cluster from the Storage Spaces Direct servers (storage). In this configuration virtual machines are configured to store their files on the Scale-Out File Server which is accessed through the network using the SMB3 protocol. In all cases virtual machine backup and recovery is seamless with no change in user experience. Note that backing up and restoring virtual machines running on a Windows Nano Server isn't supported.

## Virtual TPM
With virtual TPM support in Windows Server 2016 Hyper-V, you can add a virtual TPM chip to a virtual machine, and encrypt it using Windows Server BitLocker to protect virtual machine volumes.  DPM can back up and recover virtual TPM-enabled virtual machines that have their VHDs/VHDXs encrypted with BitLocker. Note that item-level recovery (ILR) isn't available in this scenario.

## Hyper-V with Storage Spaces Direct
DPM recognizes and protects Hyper-V VMs deployed on Storage Spaces Direct, delivering seamless backup and recovery of Virtual Machines in both disaggregated, and Hyper-converged scenarios.

## Hyper-V with ReFS SOFS Cluster
DPM 2016 can now back-up Hyper-V VMs deployed on ReFS-based SOFS Clusters. Backup and recovery of both RCT-based VMs, and non-RCT VMs is supported.

## DPM 2016 upgrades do not need require rebooting the production server
When you upgrading to DPM 2016, you are not required to reboot the production server. To avoid the production server reboot, upgrade to DPM 2016 and upgrade the DPM agent on the production servers. Backups will continue and you can reboot the production server when you want.
