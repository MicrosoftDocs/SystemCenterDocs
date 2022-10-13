---
ms.assetid:
title: What's new in System Center Virtual Machine Manager
description: This article describes the new features supported in VMM
author: jyothisuri
ms.author: jsuri
manager: evansma
ms.date: 11/29/2021
ms.topic: article
ms.prod: system-center
ms.technology: virtual-machine-manager
ms.custom: intro-whats-new
---

## New features in VMM 2022

See the following sections for new features and feature updates supported in VMM 2022. 

## Compute

### Windows Server 2022 and Windows Server 2022 Guest OS support

VMM 2022 can be used to manage on Windows Server 2022 hosts and Windows Server 2022 Guest OS hosts.

### Windows 11 support

VMM 2022 supports Windows 11 as guest operating system.

### Support for Azure Stack HCI clusters 21H2

With VMM 2022 you can manage Azure Stack HCI, 21H2 clusters.

Azure Stack HCI, version 21H2 is the newly introduced hyper-converged infrastructure (HCI) Operating system that runs on on-premises clusters with virtualized workloads.

Most of the operations to manage Azure Stack clusters in VMM are similar to managing Windows Server clusters. 

>[!NOTE]
> Management of Azure Stack HCI stretched clusters is currently not supported in VMM.

See [Deploy and manage Azure Stack HCI clusters in VMM](/system-center/vmm/deploy-manage-azure-stack-hci).

### Register and unregister Azure Stack HCI cluster using PowerShell cmdlets

VMM 2022 supports **register** and **unregister** PowerShell cmdlets for Azure Stack HCI cluster. See [Register-SCAzStackHCI](/powershell/module/virtualmachinemanager/register-scazstackhci?preserve-view=true&view=systemcenter-ps-2022) and [Unregister-SCAzStackHCI](/powershell/module/virtualmachinemanager/unregister-scazstackhci?preserve-view=true&view=systemcenter-ps-2022).

### Support for dual stack SDN deployment

VMM 2022 supports dual stack SDN deployment.  

In VMM 2019 UR2, we introduced support for Ipv6 based SDN deployment. VMM 2022 supports dual stack (Ipv4 + Ipv6) for SDN components.  

To enable Ipv6 for SDN deployment, do the required changes in the network controller, gateway, and SLB setup.   

For more information about these updates, see [Network controller](/system-center/vmm/sdn-controller), [Gateway](/system-center/vmm/sdn-gateway), [SLB](/system-center/vmm/sdn-slb), and [Set up NAT](/system-center/vmm/sdn-set-up-nat).


## New features in VMM 2022 UR1

The following sections introduce the new features and feature updates supported in VMM 2022 Update Rollup 1 (UR1).

For problems fixed in VMM 2022 UR1, and installation instructions for UR1, see the KB article.

### Support for Azure Stack HCI clusters 22H2

With VMM 2022 UR1 you can manage Azure Stack HCI, 22H2 clusters.

Azure Stack HCI, version 22H2 is the newly introduced hyper-converged infrastructure (HCI) Operating system that runs on on-premises clusters with virtualized workloads.

Most of the operations to manage Azure Stack clusters in VMM are similar to managing Windows Server clusters. 

See [Deploy and manage Azure Stack HCI clusters in VMM](/system-center/vmm/deploy-manage-azure-stack-hci)

### Support for VMware Vsphere 7.0

VMM 2022 UR1 supports VMware Vsphere 7.0

### Support for SQL Server 2022

VMM 2022 UR1 supports SQL Server 2022