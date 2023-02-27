---
description: This article provides the new features and feature updates supported by System Center DPM 2022.
manager: mkluck
ms.topic: include
author: jyothisuri
ms.prod: system-center
ms.date: 11/10/2022
title: What's new in System Center DPM
ms.technology: data-protection-manager
ms.assetid:
ms.author: jsuri
ms.custom: intro-whats-new
---

## New features in DPM 2022

See the following sections for detailed information about the new features/feature updates supported in DPM 2022.

### Windows Server 2022 support

DPM 2022 supports the installation of DPM 2022 on Windows Server 2022 and the protection of Windows Server 2022 workloads. For more information on supported versions for Windows Servers, see system requirements.

### Removed File Catalog dependency for online backup of file/folder workloads

DPM 2022 removes the dependency on File Catalog, which was needed to restore individual files and folders from the Online recovery points. DPM now uses the iSCSI mount method to provide individual file restoration. This also improves backup time as upload of file catalog metadata isn't needed anymore

> [!NOTE]
> The MARS agent version you're using must be 2.0.9236.0 or later.

### Private endpoint support
With DPM 2022, you can use a private endpoint to take online backup to the Azure Backup Recovery Services vault. [Learn more](/azure/backup/private-endpoints-overview).

### Support for VMware vSphere 7.0

DPM 2022 adds support for protecting virtual machines running on VMware 7.0. [Learn more](/system-center/dpm/back-up-vmware).

### Parallel restore for VMware and Hyper-V virtual machines

DPM 2022 supports [parallel restore of VMware](/system-center/dpm/back-up-vmware#vmware-parallel-restore-in-dpm-2022) and [Hyper-V virtual machines](/system-center/dpm/back-up-hyper-v-virtual-machines#recover-backed-up-virtual-machines). With earlier versions of DPM, restore of VMware VM and Hyper-V virtual machine was restricted to only one restore job at a time. With DPM 2022, by default you can restore 8 VMs in parallel and this number can be increased using a registry key.

## New features in DPM 2022 UR1

See the following sections for information about the new features/feature updates supported in DPM 2022 UR1.

For issues fixed and the installation instructions for UR1, see [KB article](https://support.microsoft.com/topic/update-rollup-1-for-system-center-2022-data-protection-manager-81543e78-69c2-4b75-9780-0ac1b98debf1) for Update Rollup 1.

### Support for SQL Server 2022

DPM 2022 UR1 supports SQL Server 2022 both as a protected workload and DPM database. [Learn more](/system-center/dpm/prepare-environment-for-dpm#sql-server-database).

### SQL Self Service Recovery Tool

DPM 2022 UR1 supports DPM SQL Self Service Recovery tool, which isn't available in DPM 2022 RTM. [Learn more](/system-center/dpm/back-up-sql-server?view=sc-dpm-2022#allow-sql-server-admins-to-restore-data).

### Support for O365 SMTP

DPM 2022 UR1 supports sending alert and report emails using O365 SMTP directly without a relay agent. [Learn more](/system-center/dpm/monitor-dpm?view=sc-dpm-2022#configure-email-for-dpm).

### End of Support for vSphere 6.0

vSphere 6.0 has reached [end of general support](https://blogs.vmware.com/vsphere/2019/10/vsphere-6-0-reaches-end-of-general-support-eogs-in-march-2020.html). DPM 2022 UR1 and later don't support backups for VMWare VMs on vSphere 6.0. Ensure to upgrade to newer vSphere versions.