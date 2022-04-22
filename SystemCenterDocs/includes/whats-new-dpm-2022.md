---
description: Descriptions of the new features in System Center DPM
manager:
ms.topic: include
author: jyothisuri
ms.prod: system-center
ms.date: 04/22/2022
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

### Support for VMware vSphere 7.0

DPM 2022 adds support for protecting virtual machines running on VMware 7.0.

### Parallel restore for VMware and Hyper-V virtual machines

DPM 2022 supports parallel restore of VMware and Hyper-V virtual machines. With earlier versions of DPM, restore of VMware VM and Hyper-V virtual machine was restricted to only one restore job at a time. With DPM 2022, by default you can restore 8 VMs in parallel and this number can be increased using a registry key.
