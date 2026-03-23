---
ms.assetid:
title: What's new in System Center Virtual Machine Manager
description: This article describes the new features supported in VMM
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 03/23/2026
ms.topic: include
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: intro-whats-new
ms.update-cycle: 1095-days
---

## New features in VMM 2025

See the following sections for new features and feature updates supported in VMM 2025.

### Support for Windows Server 2025

VMM 2025 supports Windows Server 2025 hosts and Virtual Machines.

### Support for management of VMs on Azure Local instances

With VMM 2025, you can manage the virtual machines running on Azure Local instances.

### Enhanced security posture

VMM 2025 works with TLS 1.3, and the dependency on legacy authentication protocols, such as NTLM and CredSSP, has reduced significantly.

All VMs created with VMM 2025 will default to Generation 2, which is UEFI firmware-based and is more secure than BIOS firmware-based Generation 1 VMs.

### Support for the latest Linux Guest Operating Systems

With VMM 2025, you can run Ubuntu Linux 24.04, RHEL 9, Debian 13 and 12, Oracle Linux 9, and Rocky Linux 9 and 8.

### Enhanced VMware to Hyper-V VM conversion performance

VMM 2025 comes with faster [ESXi to Hyper-V VM conversion](../vmm/vm-convert-vmware.md) performance by default.

### Switch to Arc-enabled SCVMM for Azure integration capabilities

In VMM 2025, the following Azure integration capabilities aren't supported:
- Azure VM management from VMM
- Azure update management v1 on VMM managed VMs

Azure Arc-enabled System Center Virtual Machine Manager is the alternative for these capabilities.

### System Center Service Provider Foundation (SPF) is discontinued

Starting from System Center 2025, Service Provider Foundation (SPF) will be discontinued as its capabilities are now built into Azure Arc-enabled System Center Virtual Machine Manager.

## New features in VMM 2025 UR1

The following sections introduce the new enhancements shipped with VMM 2025 Update Rollup 1 (UR1).

For problems fixed in VMM 2025 UR1, and installation instructions for UR1, see the [KB article](https://support.microsoft.com/topic/update-rollup-1-for-system-center-2022-virtual-machine-manager-90163a7e-1515-4cba-8647-a22c441830b7).

### Support for virtual Trusted Platform Module (vTPM)

VMM 2025 UR1 provides GUI and PowerShell experience to run vTPM-enabled virtual machines. You can enable vTPM while creating a new virtual machine and while modifying the properties of an existing virtual machine, and thus improving your security posture. 

### Support for SQL 2025 and SQL Contained Availability Group

You can use SQL 2025 for VMM 2025's database. To improve your resiliency posture, you can choose to use a SQL Contained Availability Group.

### Support for the latest Linux Guest Operating Systems and Linux network settings file format

With VMM 2025 UR1, you can manage RHEL 10, SUSE Linux 15, Oracle Linux 10, Rocky Linux 10, and OpenEuler 24.03 flavored Linux virtual machines. Along with the updated Operating Systems support, VMM recognizes and supports storing network settings of Linux machines in _keyfile_ format. 

### Support for management of VMs on latest versions of Azure Local instances

VMM 2025 UR1 comes with updated support to manage VMs running on the latest versions of Azure Local instances.
