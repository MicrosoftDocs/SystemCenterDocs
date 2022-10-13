---
description: This article provides the new features and feature updates supported by System Center DPM 2022.
manager:
ms.topic: article
author: jyothisuri
ms.prod: system-center
ms.date: 05/02/2022
title: What's new in System Center DPM
ms.technology: data-protection-manager
ms.assetid:
ms.author: jsuri
ms.custom: intro-whats-new
---

## New features in DPM 2022

See the following sections for detailed information about the new features/feature updates supported in DPM 2022.

### Windows Server 2022 support

DPM 2022 supports installation of DPM 2022 on Windows Server 2022 and protection of Windows Server 2022 workloads. For more information on supported versions for Windows Servers, see system requirements.

### Removed File Catalog dependency for online backup of file/folder workloads

DPM 2022 removes the dependency on File Catalog which was needed to restore individual files and folders from the Online recovery points. DPM now uses iSCSI mount method to provide individual file restore. This also improves the backups time as upload of file catalog metadata is not needed anymore

> [!NOTE]
> The MARS agent version you are using must be 2.0.9236.0 or later.

### Private endpoint support
With DPM 2022, you can use private endpoint to take online backup to Azure Backup Recovery Services vault. [Learn more](/azure/backup/private-endpoints-overview).

### Support for VMware vSphere 7.0

DPM 2022 adds support for protecting virtual machines running on VMware 7.0. [Learn more](/system-center/dpm/back-up-vmware).

### Parallel restore for VMware and Hyper-V virtual machines

DPM 2022 supports [parallel restore of VMware](/system-center/dpm/back-up-vmware#vmware-parallel-restore-in-dpm-2022) and [Hyper-V virtual machines](/system-center/dpm/back-up-hyper-v-virtual-machines#recover-backed-up-virtual-machines). With earlier versions of DPM, restore of VMware VM and Hyper-V virtual machine was restricted to only one restore job at a time. With DPM 2022, by default you can restore 8 VMs in parallel and this number can be increased using a registry key.

## New features in DPM 2022 UR1

See the following sections for information about the new features/feature updates supported in DPM 2022 UR1.

For issues fixed and the installation instructions for UR1, see KB article for Update Rollup 1.

### Support for SQL Server 2022

DPM 2022 UR1 supports SQL Server 2022. [Learn more](/system-center/dpm/prepare-environment-for-dpm#sql-server-database).

### Support for Virtual Disk Development kit 7.0

DPM 2022 UR1 supports VDDK 7.0