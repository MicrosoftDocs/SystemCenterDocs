---
ms.assetid: b329876f-68f3-4087-beb3-076c1ad84f49
title: include file
description: include file to describe the new features in virtual machine manager 2016
author: Jeronika-MS
ms.author: v-gajeronika
ms.date:  04/24/2020
ms.topic:  include
ms.service:  system-center
ms.subservice:  virtual-machine-manager
ms.update-cycle: 1095-days
---


## What's new in VMM 2016

See the following sections for detailed information about the new features supported in VMM 2016.


## Compute

### Full lifecycle management of Nano Server-based hosts and VMs
You can provision and manage Nano Server-based hosts and virtual machines in the VMM fabric. [Learn more](../vmm/hyper-v-nano.md).

### Rolling upgrade of a Windows Server 2012 R2 host clusters

You can now upgrade Hyper-V and scale-out file server (SOFS) clusters in the VMM fabric from Windows Server 2012 R2 to Windows Server 2016, with no downtime for the host workloads. VMM orchestrates the entire workflow. It drains the node, removes it from the cluster, reinstalls the operating system, and adds it back into the cluster. Learn more about performing rolling upgrades for [Hyper-V clusters](../vmm/hyper-v-rolling-upgrade.md) and [SOFS clusters](../vmm/sofs-rolling-upgrade.md).

### Creating Hyper-V & SOFS clusters

There's a streamlined workflow for creating Hyper-V and SOFS clusters:

* **Bare metal deployment of Hyper-V host clusters**: Deploying a Hyper-V host cluster from bare-metal machines is now a single step. [Learn more](../vmm/hyper-v-bare-metal.md)

* **Adding a bare-metal node to an existing Hyper-V host cluster or an SOFS Cluster**: You can now directly add a bare-metal computer to an existing [Hyper-V](../vmm/hyper-v-bare-metal.md) or [SOFS](../vmm/sofs-bare-metal.md) cluster.

### New operations for running VMs

You can now increase/decrease static memory and add/remove virtual network adapter for virtual machines that are running. [Learn more](../vmm/vm-settings.md).

### Production checkpoints

You can now create production checkpoints for VMs. These checkpoints are based on Volume Shadow Copy Service (VSS) and are application-consistent (compared to standard checkpoints based on saved state technology that aren't). [Learn more](../vmm/vm-settings.md).

### Server App-V

The Server App-V application in service templates is no longer available in VMM 2016. You can't create new templates or deploy new services with the Server App-V app. If you upgrade from VMM 2012 R2 and have a service with the Server App-V application, the existing deployment will continue to work. However, after the upgrade, you can't scale out the tier with Server App-V application. You can scale out other tiers.


>[!NOTE]
> The following feature is available from 2016 UR9.

### Enhanced console session in VMM

The console connect capability in VMM provides an alternative way to connect to the VM via remote desktop. This method is most useful when the VM doesn't have any network connectivity or when you want to change to a network configuration that could break the network connectivity. Currently, the console connect capability in VMM supports only a basic session where clipboard text can be pasted only by using the **Type Clipboard Text** menu option.

VMM supports an enhanced console session that enables **Cut (Ctrl + X)**, **Copy (Ctrl + C)**, and **Paste (Ctrl + V)** operations on the ANSI text and files available on the clipboard. As a result, **Copy** and **Paste** commands for text and files are possible from and to the VM. For more information, see [Enable enhanced console session in VMM](../vmm/enhanced-console-session.md).


## Storage

### Deploy and manage storage clusters with Storage Spaces Direct (S2D)

[Storage Spaces Direct in Windows Server 2016](/windows-server/storage/storage-spaces/storage-spaces-direct-overview) enables you to build highly available storage systems on Windows Server. You can use VMM to create a Scale-Out File Server running Windows Server 2016, and configure it with Storage Spaces Direct. After it's configured, you can create storage pools and file shares on it. [Learn more](../vmm/s2d.md).


### Storage Replica

In VMM 2016, you can use Windows Storage Replica to protect data in a volume by synchronously replicating it between primary and secondary (recovery) volumes. You can deploy the primary and secondary volumes to a single cluster to two different clusters or to two standalone servers. You use PowerShell to set up Storage Replica and run failover. [Learn more](../vmm/storage-replica.md)

### Storage Quality of Service (QoS)

You can configure QoS for storage to ensure that disks, VMs, apps, and tenants don't drop below a certain resource quality when hosts and storage are handling heavy loads. You can configure QoS for storage in the VMM fabric.


## Networking

### Software Defined Networking (SDN)

In VMM 2016, you can deploy the entire SDN stack using VMM service templates.

* You can deploy and manage a multi-node Network Controller in a subnet. After you deploy and onboard the Network Controller, you can specify that fabric components should be managed with SDN to provide connectivity to tenant VMs and to define policies.
* You can deploy and configure a software load balancer to distribute traffic within networks managed by Network Controller. The software load balancer can be used for inbound and outbound NAT.
* You can deploy and configure a Windows Server Gateway pool with M+N redundancy. After you deploy the gateway, you connect a tenant network to a hosting provider network, or to your own remote data center network using S2S GRE, S2S IPSec, or L3.

### Network traffic isolation and filtering

You can limit and segregate network traffic by specifying port ACLs on VM networks, virtual subnets, network interfaces, or on an entire VMM stamp using Network Controller and PowerShell. [Learn more](../vmm/hyper-v-acls.md).

### Virtual network adapter naming

When you deploy a virtual machine, you might want to run a post-deployment script on the guest operating system to configure virtual network adapters. Previously, this was difficult because there wasn't an easy way to distinguish different virtual network adapters during deployment. Now, for generation 2 virtual machines deployed on Hyper-V hosts running Windows Server 2016, you can name the virtual network adapter in a virtual machine template. This is similar to using consistent device naming (CDN) for a physical network adapter.

### Self-service SDN management using Windows Azure Pack (WAP)

You can provide self-service capabilities for fabric managed by Network Controller. These include creating and managing VM networks, configuring S2S IPSec connections, and configuring NAT options for tenant and infrastructure VMs in your data center.  

### Logical switch deployment across hosts

- The interface for creating a logical switch has been streamlined to make it easier to select settings.
- You can directly use Hyper-V to configure a standard virtual switch on a managed host, and then use VMM to convert the standard virtual switch to a VMM logical switch, which you later apply on additional hosts.
- When applying a logical switch to a particular host, if the entire operation doesn't succeed, the operation is reverted and host settings are left unchanged. Improved logging makes it easier to diagnose failures.

## Security

### Guarded host deployment

You can provision and manage guarded hosts and shielded VMs in the VMM fabric, to help provide protection against malicious host administrators and malware.

-   You can manage guarded hosts in the VMM compute fabric. You configure guarded hosts to communicate with HGS servers, and you can specify code integrity policies that restrict software that can run in kernel mode on the host.
- You can convert existing VMs to shielded VMs, and deploy new shielded VMs.