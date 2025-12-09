---
description: This article provides the new features and feature updates supported by System Center DPM 2025.
ms.topic: include
author: Jeronika-MS
ms.author: v-gajeronika
ms.service: system-center
ms.date: 12/09/2025
title: What's new in System Center DPM
ms.subservice: data-protection-manager
ms.assetid:
ms.custom: intro-whats-new
---

## New features in DPM 2025

See the following sections for detailed information about the new features/feature updates supported in DPM 2025.

### Windows Server 2025 support

DPM 2025 supports the installation of DPM 2025 on Windows Server 2025 and the protection of Windows Server 2025 workloads. You can now Backup system state, file, folder and volume, and applications supported by DPM 2025. [Learn more](/system-center/dpm/prepare-environment-for-dpm?view=sc-dpm-2025&preserve-view=true)

### Enhanced Passphrase save mechanism for MARS Agent

Save passphrases to the Azure Key vault to reduce the risk of losing them due to server corruption, compromise, or accidental file deletion. Warnings are displayed when saved locally.

### DPM database Backup notifications

Backup the DPM database to disk and Azure to mitigate and reconstruct the DPM server after the original server is lost. Use the `DPMSync` Tool to resynchronize the database.

### Support for SharePoint subscription edition

Use the `ConfigureSharepoint.exe` command line tool to support the SharePoint subscription edition.

### Support for VMs with vTPM device configured

Backup and restore vTPM configured VMs, preserving vTPM device settings during the restoration process. The Alternate Location Restore (ALR) flow for vTPM VMs assumes that the selected target vCenter has access to the same Key Provider.

### Support for SQL OLEDB 19

DPM 2025 uses OLEDB 19 driver to communicate and backup SQL instances. This is applicable for SharePoint backups also.

## New features in DPM 2025 UR1
 
See the following sections for information about the new features/feature updates supported in DPM 2025 UR1. 
 
For issues fixed and the installation instructions for UR1, see [KB article](https://support.microsoft.com/help/5068307) for Update Rollup 1.
 
### Hyper-V select disk exclusion

DPM 2025 UR1 allows administrators to exclude specific disks from a Hyper-V VM backup.
 
The backup omits the excluded disk contents from the restore points. As a result, when the VM gets restored, the excluded disks wouldn't be overwritten by backup data. [Learn more](/system-center/dpm/back-up-hyper-v-virtual-machines?view=sc-dpm-2025#exclude-disk-from-hyper-v-vm-backup).

### Support for SQL Server 2025

DPM 2025 UR1 supports SQL Server 2025 both as a protected workload and DPM database. [Learn more](https://learn.microsoft.com/system-center/dpm/prepare-environment-for-dpm#sql-server-database).
 
### Runtime dependent version is compliant and secure

DPM 2025 UR1 requires the latest Visual C++ Redistributable 2013, 2015-2022 (latest) x64 packages.

>[!NOTE]
>A fresh installation of DPM agent requires Visual C++ Redistributable 2013 X64 as the RTM version of agent is built using the same. Post DPM installation, uninstall Visual C++ 2013 Redistributable.
 
### Support for Exchange Subscription Edition

DPM 2025 UR1 supports Exchange Subscription Edition as an application aware backup. [Learn More](/system-center/dpm/dpm-protection-matrix?view=sc-dpm-2025#applications-backup-1).
