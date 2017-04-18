---
ms.assetid: b329876f-68f3-4087-beb3-076c1ad84f49
title: What's new in VMM in System Center 2016
description: This article describes what's new in System Center VMM 2016
author:  rayne-wiselman
ms.author: raynew
manager:  cfreeman
ms.date:  12/12/2016
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---


# What's new in VMM in System Center 2016

>Applies To: System Center 2016 - Virtual Machine Manager

This article describes what's new in System Center 2016 - Virtual Machine Manager (VMM).


## Compute

### Full lifecycle management of Nano Server-based hosts and VMs
You can provision and manage Nano Server-based hosts and virtual machines in the VMM fabric. [Learn more](hyper-v-nano.md).

### Rolling upgrade of a Windows Server 2012 R2 host clusters

You can now upgrade Hyper-V and scale-out file server (SOFS) clusters in the VMM fabric from Windows Server 2012 R2 to Windows Server 2016, with no downtime for the host workloads. VMM orchestrates the entire workflow. It drains the node, removes it from the cluster, reinstalls the operating system, and adds it back into the cluster. Learn more about performing rolling upgrades for [Hyper-V clusters](hyper-v-rolling-upgrade.md), and [SOFS clusters](manage/manage-sofs-rolling-upgrade.md).

### Creating Hyper-V & SOFS clusters

There's a streamlined workflow for creating Hyper-V and SOFS clusters:

* **Bare metal deployment of Hyper-V host clusters**: Deploying a Hyper-V host cluster from bare metal machines is now a single step. [Learn more](hyper-v-bare-metal.md)

* **Adding a bare-metal node to an existing Hyper-V host cluster or an SOFS Cluster**: You can now directly add a bare-metal computer to an existing [Hyper-V](hyper-v-bare-metal.md) or [SOFS](manage/manage-sofs-bare-metal.md) cluster.

### New operations for running VMs

You can now increase/decrease static memory and add/remove virtual network adapter for virtual machines that are running. [Learn more](manage/manage-vm-settings.md).

### Production checkpoints

You can now create production checkpoints for VMs. These checkpoints are based on Volume Shadow Copy Service (VSS) and are application-consistent (compared to standard checkpoints based on saved state technology that aren't. [Learn more](manage/manage-vm-settings.md).

### Server App-V

The Server App-V application in service templates is no longer available in VMM 2016. You can't create new templates or deploy new services with the Server App-V app. If you upgrade from VMM 2012 R2 and have a service with the Server App-V application, the existing deployment will continue to work. However, after the upgrade you can't scale out the tier with Server App-V application. You can scale out other tiers.

## Storage

### Deploy and manage storage clusters with Storage Spaces Direct (S2D)

[Storage Spaces Direct in Windows Server 2016](https://technet.microsoft.com/library/mt126109.aspx) enables you to build highly available storage systems on Windows Server. You can use VMM to create a Scale-Out File Server running Windows Server 2016, and configure it with Storage Spaces Direct. After it's configure you can create storage pools and file shares on it. [Learn more](manage/manage-storage-spaces-direct-vmm.md).


### Storage Replica

In VMM 2016 you can use Windows Storage Replica to protect data in a volume by synchronously replicating it between primary and secondary (recovery) volumes. You can deploy the primary and secondary volumes to a single cluster, to two different clusters, or to two standalone servers. You use PowerShell to set up Storage Replica and run failover. [Learn more](manage/manage-storage-replica.md)

### Storage Quality of Service (QoS)

You can configure QoS for storage to ensure that disks, VMs, apps, and tenants don't drop below a certain resource quality when hosts and storage are handling heavy loads. You can configure QoS for storage in the VMM fabric.


## Networking

### Software Defined Networking (SDN)

In VMM 2016 you can deploy the entire SDN stack using VMM service templates.

* You can deploy and manage a multi-node Network Controller in a subnet. After you deploy and onboard the Network Controller, you can specify that fabric components should be managed with SDN, to provide connectivity to tenant VMs and to define policies.
* You can deploy and configure a software load balancer, to distribute traffic within networks managed by Network Controller. The software load balancer can be used for inbound and outbound NAT.
* You can deploy and configure a Windows Server Gateway pool with M+N redundancy. After you deploy the gateway, you connect a tenant network to a hosting provider network, or to your own remote data center network using S2S GRE, S2S IPSec, or L3.

### Network traffic isolation and filtering

You can limit and segregate network traffic by specifying port ACLs on VM networks, virtual subnets, network interfaces, or on an entire VMM stamp using Network Controller and PowerShell. [Learn more](hyper-v-acls.md).

### Virtual network adapter naming

When you deploy a virtual machine, you might want to run a post-deployment script on the guest operating system to configure virtual network adapters.  Previously, this was difficult because there wasn't an easy way to distinguish different virtual network adapters during deployment. Now, for generation 2 virtual machines deployed on Hyper-V hosts running Windows Server 2016, you can name the virtual network adapter in a virtual machine template. This is similar to using consistent device naming (CDN) for a physical network adapter.

### Self-service SDN management using Windows Azure Pack (WAP)

You can provide self-service capabilities for fabric managed by Network Controller. These include creating and managing VM networks, configuring S2S IPSec connections, and configuring NAT options for tenant and infrastructure VMs in your data center.  

### Logical switch deployment across hosts

- The interface for creating a logical switch has been streamlined to make it easier to select settings.
- You can directly use Hyper-v to configure a standard virtual switch on a managed host, and then use VMM to convert the standard virtual switch to a VMM logical switch, which you later apply on additional hosts.
- When apply a logical switch to a particular host, if the entire operation doesn't succeed, the operation is reverted and host settings are left unchanged. Improved logging makes it easier to diagnose failures.

## Security

### Guarded host deployment

You can provision and manage guarded hosts and shielded VMs in the VMM fabric, to help provide protection against malicious host administrators and malware.

-   You can manage guarded hosts in the VMM compute fabric. You configure guarded hosts to communicate with HGS servers, and you can specify code integrity policies that restrict software that can run in kernel mode on the host.
- You can convert existing VMs to shielded VMs, and deploy new shielded VMs.
