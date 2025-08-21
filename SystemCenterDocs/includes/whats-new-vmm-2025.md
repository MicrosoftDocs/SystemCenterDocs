---
ms.assetid:
title: What's new in System Center Virtual Machine Manager
description: This article describes the new features supported in VMM
author: jyothisuri
ms.author: jsuri
ms.date: 12/18/2024
ms.topic: include
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: intro-whats-new
---

## New features in VMM 2025

See the following sections for new features and feature updates supported in VMM 2025.

### Support for Windows Server 2025

VMM 2025 supports Windows Server 2025 hosts and Virtual Machines.

### Support for management of VMs on Azure Local instances 23H2

With VMM 2025, you can manage the virtual machines running on Azure Local 23H2 instances.

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
