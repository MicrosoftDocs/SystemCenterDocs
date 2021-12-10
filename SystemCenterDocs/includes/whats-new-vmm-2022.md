---
ms.assetid:
title: What's new in System Center Virtual Machine Manager
description: This article describes the new features supported in VMM
author: v-jysur
ms.author: v-jysur
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

### Windows Server 2022 support

VMM 2022 can be installed on Windows Server 2022.

### Supported scenarios to manage Windows Server 2022

The following are the supported scenarios:

1. Addition, creation, and management of Windows Server 2022 virtualization servers.  

1. Ability to provision and deploy VMs on the Azure Stack HCI clusters and perform VM life cycle operations. VMs can be provisioned using VHD files, templates or from an existing VM.  

1. Setting up LAN based network.  

1. Management of storage pool settings, creation of virtual disks, creation of cluster shared volumes (CSVs) and application of QOS settings.

1. Create, deploy, and manage VMM private cloud.

### Support for Azure Stack HCI clusters 21H2

With VMM 2022 you can manage Azure Stack HCI clusters in VMM. In addition to the current SKU of the server operating system, VMM expands its support to Azure Stack HCI, version 21H2.

Azure Stack HCI, version 21H2 is the newly introduced hyper-converged infrastructure (HCI) Operating system that runs on on-premises clusters with virtualized workloads.

Most of the operations to manage Azure Stack clusters in VMM are similar to managing Windows Server clusters. 

>[!NOTE]
> Management of Azure Stack HCI stretched clusters is currently not supported in VMM.

### Register and unregister Azure Stack HCI cluster using PowerShell cmdlets

VMM 2022 supports **register** and **unregister** PowerShell cmdlets for Azure Stack HCI cluster. Learn more.

### Support for dual stack SDN deployment

VMM 2022 supports dual stack SDN deployment.  

In VMM 2019 UR2, we introduced support for Ipv6 based SDN deployment. VMM 2022 supports dual stack (Ipv4 + Ipv6) for SDN components.  

To enable Ipv6 for SDN deployment, do the required changes in the network controller, gateway, and SLB set up.   
