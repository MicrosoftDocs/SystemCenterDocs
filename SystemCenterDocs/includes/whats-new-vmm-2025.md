---
ms.assetid:
title: What's new in System Center Virtual Machine Manager
description: This article describes the new features supported in VMM
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 10/01/2024
ms.topic: include
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: intro-whats-new
---

## New features in VMM 2025

See the following sections for new features and feature updates supported in VMM 2025.

### Support for Windows Server 2025

VMM 2025 supports Windows Server 2025 hosts and Virtual Machines.

### Support for Azure Stack HCI clusters 23H2

With VMM 2025, you can manage Azure Stack HCI 23H2 clusters.

### Enhanced security posture

VMM 2025 works with TLS 1.3, and the dependency on legacy authentication protocols, such as NTLM and CredSSP, has reduced significantly.

All VMs created with VMM 2025 will default to Generation 2, which is UEFI firmware-based and is more secure than BIOS firmware-based Generation 1 VMs.

### Support for the latest Linux Guest OSes

With VMM 2025, you can run Ubuntu Linux 24.04, RHEL 9, Debian 13 and 12, SUSE Linux 15, Oracle Linux 9, and Rocky Linux 9 and 8.

### Switch to Arc-enabled SCVMM for Azure integration capabilities

In VMM 2025, Azure integration capabilities – Azure VM management from VMM and Azure update management v1 on VMM managed VMs – aren't supported. Azure Arc-enabled System Center Virtual Machine Manager is the alternative for these capabilities.

### System Center Service Provider Foundation (SPF) is discontinued

Starting from System Center 2025, Service Provider Foundation (SPF) will be discontinued as its capabilities are now built into Azure Arc-enabled System Center Virtual Machine Manager.
