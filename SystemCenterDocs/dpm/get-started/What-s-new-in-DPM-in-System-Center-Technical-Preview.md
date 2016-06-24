---
title: What&#39;s new in DPM in System Center Technical Preview
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - data-protection-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a5e81bf0-43a6-4099-af2e-dfb0c1aa7ed8
---
# What&#39;s new in DPM in System Center Technical Preview
Here's what's new in Data Protection Manager (DPM) in System Center Technical Preview 5. Before you begin, check the [Release Notes for System Center Technical Preview 5](../../get-started/Release-Notes-for-System-Center-Technical-Preview-5.md) for last minute issues.

## Protect data sources in mixed-mode clusters
Windows Server Technical Preview introduced [rolling upgrade support for clusters](https://technet.microsoft.com/library/dn850430.aspx), which means that in a cluster you can deploy servers running both Windows Server 2012 R2 and Windows Server Technical Preview. DPM can protect data sources in these mixed clusters, and will protect them seamlessly and without interruption during a cluster upgrade. Note that DPM doesn't support backup and recovery of data from Windows Nano Server.

## Resilient change tracking (RCT)
Hyper-V backup has been enhanced with resilient change tracking (RCT). RCT is a new form of built-in changing tracking for Hyper-V VM virtual hard disks. RCT provides better resiliency than the change tracking provided by VSS snapshot-based backups.  DPM now uses RCT for incremental backup. It identifies VHD changes for virtual machines, and transfers only those blocks that are indicated by the change tracker. [Read more](http://www.aidanfinn.com/?p=17505) about RCT on Aidan Finn's blog.

## Storage Spaces Direct
Storage Spaces Direct (S2D) leverages the Storage Spaces feature that was introduced in Windows Server 2012 R2, without the need for shared storage, allowing you to deploy highly available (HA) storage systems using local storage. It leverages the local disks on hosts to provide a shared pool of clustered storage that can be used as primary storage of Hyper-V virtual machine files, or for secondary storage for Hyper-V Replica virtual machines files. 
 The primary use case for Storage Spaces Direct is private cloud storage, either on-prem for enterprises, or in hosted private clouds for service providers. 
 Get an [overview](https://channel9.msdn.com/Events/Ignite/2015/BRK3474) .

DPM protects Hyper-V virtual machines that use  Storage Spaces Direct. Most configurations are supported, including the backup of virtual machines using the S2D hyper-converged scenario with the Hyper-V (compute) and Storage Spaces Direct (storage) components on the same cluster, and the backup of virtual machines using the S2D disaggregated scenario which separates out  Hyper-V servers (compute) into a separate cluster from the Storage Spaces Direct servers (storage). In this configuration virtual machines are configured to store their files on the Scale-Out File Server which is accessed through the network using the SMB3 protocol. In all cases virtual machine backup and recovery is seamless with no change in user experience. Note that backing up and restoring virtual machines running on a Windows Nano Server isn't supported.

## Virtual TPM
With virtual TPM support
In Windows Server 2016 Hyper-V you can add a virtual TPM chip to a virtual machine, and encrypt it using Windows Server BitLocker to protect virtual machine volumes.  DPM can back up and recover virtual TPM enabled virtual machines that have their VHDs/VHDXs encrypted with BitLocker. Note that item-level recovery (ILR) isn't available in this scenario.


