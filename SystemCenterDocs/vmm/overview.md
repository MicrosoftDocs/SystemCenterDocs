---
ms.assetid: 0492a730-365e-4d72-bf83-f1fd990b7ba1
title: What is Virtual Machine Manager?
description: This article provides an overview of System Center VMM and a summary of what it can do for your business.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 06/27/2024
ms.topic: article
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: UpdateFrequency.5, intro-overview, engagement-fy24
---

# What is Virtual Machine Manager?

::: moniker range=">= sc-vmm-1801 <= sc-vmm-1807"

[!INCLUDE [eos-notes-virtual-machine-manager.md](../includes/eos-notes-virtual-machine-manager.md)]

::: moniker-end

Welcome to System Center Virtual Machine Manager (VMM)! VMM is part of the System Center suite used to configure, manage, and transform traditional datacenters. It helps to provide a unified management experience across on-premises, service provider, and the Azure cloud. VMM capabilities include:

- **Datacenter**: Configure and manage your datacenter components as a single fabric in VMM. Datacenter components include virtualization servers, networking components, and storage resources. VMM provisions and manages the resources needed to create and deploy virtual machines and services to private clouds.
- **Virtualization hosts**: VMM can add, provision, and manage Hyper-V and VMware virtualization hosts and clusters.
- **Networking**: Add networking resources to the VMM fabric, including network sites defined by IP subnets, virtual LANs (VLANs), logical switches, static IP address, and MAC pools. VMM provides network virtualization, including support for creating and managing virtual networks and network gateways. Network virtualization allows multiple tenants to have isolated networks and their own IP address ranges for increased privacy and security. Using gateways, VMs on virtual networks can connect to physical networks in the same site or in different locations.
- **Storage**: VMM can discover, classify, provision, allocate, and assign local and remote storage. VMM supports block storage (fiber channel, iSCSI, and Serial Attached SCSI (SAS) storage area networks (SANs)).
- **Library resources**: The VMM fabric retains a library of file-based and non-file-based resources that are used to create and deploy VMs and services on virtualization hosts. File-based resources include virtual hard disks, ISO images, and scripts. Non-file-based resources include templates and profiles that are used to standardize the creation of VMs. Library resources are accessed through library shares.

## Resources

- To read blog posts from the VMM engineering team, see [System Center Blog](https://techcommunity.microsoft.com/t5/system-center-blog/bg-p/SystemCenterBlog/label-name/System%20Center%20Virtual%20Machine%20Manager).

## Next steps

- Learn about [system requirements](system-requirements.md).
- Get started with [Arc-enabled SCVMM](/azure/azure-arc/system-center-virtual-machine-manager/overview#how-does-it-work).
