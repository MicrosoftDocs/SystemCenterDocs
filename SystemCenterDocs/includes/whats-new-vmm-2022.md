---
ms.assetid:
title: What's new in System Center Virtual Machine Manager
description: This article describes the new features supported in VMM
ms.date: 04/14/2025
author: Jeronika-MS
ms.author: v-gajeronika
ms.topic: include
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: intro-whats-new
ms.update-cycle: 1095-days
---

## New features in VMM 2022

See the following sections for new features and feature updates supported in VMM 2022. 

### Compute

### Windows Server 2022 and Windows Server 2022 Guest OS support

VMM 2022 can be used to manage on Windows Server 2022 hosts and Windows Server 2022 Guest OS hosts.

### Windows 11 support

VMM 2022 supports Windows 11 as guest operating system.

### Support for Azure Stack HCI clusters 21H2

With VMM 2022, you can manage Azure Stack HCI, 21H2 clusters.

Azure Stack HCI, version 21H2 is the newly introduced hyper-converged infrastructure (HCI) Operating system that runs on on-premises clusters with virtualized workloads.

Most of the operations to manage Azure Local instances in VMM are similar to managing Windows Server clusters.

>[!NOTE]
> Management of Azure Local stretched clusters is currently not supported in VMM.

See [Deploy and manage Azure Local instances in VMM](../vmm/deploy-manage-azure-stack-hci.md).

### Register and unregister Azure Local instance using PowerShell cmdlets

VMM 2022 supports **register** and **unregister** PowerShell cmdlets for Azure Local instance. See [Register-SCAzStackHCI](/powershell/module/virtualmachinemanager/register-scazstackhci?preserve-view=true&view=systemcenter-ps-2022) and [Unregister-SCAzStackHCI](/powershell/module/virtualmachinemanager/unregister-scazstackhci?preserve-view=true&view=systemcenter-ps-2022).

### Support for dual stack SDN deployment

VMM 2022 supports dual stack SDN deployment.  

In VMM 2019 UR2, we introduced support for Ipv6 based SDN deployment. VMM 2022 supports dual stack (Ipv4 + Ipv6) for SDN components.  

To enable Ipv6 for SDN deployment, do the required changes in the network controller, gateway, and SLB setup.   

For more information about these updates, see [Network controller](../vmm/sdn-controller.md), [Gateway](../vmm/sdn-gateway.md), [SLB](../vmm/sdn-slb.md), and [Set up NAT](../vmm/sdn-set-up-nat.md).

## New features in VMM 2022 UR1

The following sections introduce the new features and feature updates supported in VMM 2022 Update Rollup 1 (UR1).

For problems fixed in VMM 2022 UR1, and installation instructions for UR1, see the [KB article](https://support.microsoft.com/topic/update-rollup-1-for-system-center-2022-virtual-machine-manager-90163a7e-1515-4cba-8647-a22c441830b7).

### Support for Azure Local instances 22H2

With VMM 2022 UR1, you can manage Azure Local, 22H2 instances.

Azure Stack HCI, version 22H2 is the newly introduced hyper-converged infrastructure (HCI) Operating system that runs on on-premises clusters with virtualized workloads.

Most of the operations to manage Azure Local instances in VMM are similar to managing Windows Server clusters.

See [Deploy and manage Azure Local instances in VMM](../vmm/deploy-manage-azure-stack-hci.md).

### Support for VMware vSphere 7.0, 8.0 and ESXi 7.0, 8.0

VMM 2022 UR1 supports VMware vSphere 7.0, 8.0 and ESXi 7.0, 8.0. [Learn more](/system-center/vmm/system-requirements?view=sc-vmm-2022&preserve-view=true).

### Support for SQL Server 2022

VMM 2022 UR1 supports SQL Server 2022. [Learn more](/system-center/vmm/system-requirements?view=sc-vmm-2022&preserve-view=true).

### Support for Smart card sign in in SCVMM Console

VMM 2022 UR1 supports Smart card sign in with enhanced session mode in SCVMM Console. 

### SR-IOV support for Network Controller managed NICs

With VMM 2022 UR1, SR-IOV supports Network Controller managed NICs.

### Removed VMM dependencies on deprecated Operations Manager Management Pack

With VMM 2022 UR1, removed VMM dependencies on deprecated SCOM Management Packs. If you have an active SCOM - VMM integration, follow the steps listed in [KB article](https://support.microsoft.com/topic/update-rollup-1-for-system-center-2022-virtual-machine-manager-90163a7e-1515-4cba-8647-a22c441830b7) before you upgrade to VMM 2022 UR1. 

### Discover Arc-enabled SCVMM from VMM console

VMM 2022 UR1 allows you to discover Arc-enabled SCVMM from console and manage your Hybrid environment and perform self-service VM operations through Azure portal. [Learn more](/system-center/vmm/about-arc-enabled-system-center-virtual-machine-manager?view=sc-vmm-2022&preserve-view=true).

### Support for 64 virtual networks for Windows Server 2019 or later
VMM 2022 UR1 supports 64 virtual networks for Windows Server 2019 or later.

## New features in VMM 2022 UR2

The following sections introduce the new features and feature updates supported in VMM 2022 Update Rollup 2 (UR2).

For problems fixed in VMM 2022 UR2, and installation instructions for UR2, see the [KB article](https://support.microsoft.com/topic/update-rollup-2-for-system-center-2022-virtual-machine-manager-a9ece9b5-a73f-42c2-9d03-427243a8f210).

### Improved V2V conversion performance of VMware VMs to Hyper-V VMs

You can now convert your VMware VMs to Hyper-V with close to four times faster conversion speed and support for VMware VMs with disk sizes greater than 2 TB. [Learn more about how to use this enhancement](../vmm/vm-convert-vmware.md#convert-vmware-vms-to-hyper-v-faster).

### Improved Arc-enabled SCVMM Discovery tab

The **Azure Arc** tab now highlights the latest feature additions to Arc-enabled SCVMM which includes support for Azure management services such as Microsoft Defender for Cloud, Azure Update Manager, Azure Monitor, Microsoft Sentinel, and more. [Learn more](https://techcommunity.microsoft.com/t5/azure-arc-blog/introducing-azure-management-capabilities-for-azure-arc-enabled/ba-p/3947253).  

If you are running WS 2012 and 2012R2 host and guest operating systems, the Azure Arc blade now provides guidance to continue remaining in support state.  

### Support for latest Linux Guest Operating Systems

With VMM 2022 UR2, you can run Ubuntu Linux 22, Debian 11, Oracle Linux 8 and 9 based Linux VMs.


## New features in VMM 2022 UR3

The following sections introduce the new features and feature updates supported in VMM 2022 Update Rollup 3 (UR3).

For problems fixed in VMM 2022 UR1, and installation instructions for UR1, see the KB article.

### Support for latest guest Operating Systems

With VMM 2022 UR3, you can run Windows Server 2025 VMs and Ubuntu Linux 24.04, RHEL 9, Debian 12, Rocky Linux 8 and 9 based Linux VMs.
