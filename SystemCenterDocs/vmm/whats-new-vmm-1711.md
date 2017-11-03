---
ms.assetid: 0683ab30-6f03-4ffc-a50d-8d91d61768fe
title: What's new in System Center Virtual Machine Manager preview version 1711
description: This article describes the new features supported in preview VMM 1711.
author:  JYOTHIRMAISURI
ms.author: V-jysur
manager:  riyazp
ms.date:  11/08/2017
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
monikerRange: 'sc-vmm-1711'
---

# What's new in System Center VMM 1711 (Technical preview)

This article describes about the new features supported in System Center Virtual Machine Manager preview 1711 (VMM 1711).

## Compute

### Management of ARM-based and region-specific Azure subscriptions

Currently, the VMM Azure plugin supports only classic virtual machines (VMs) and public Azure regions.

VMM 1711 supports management of ARM-based VMs that are created by using the new Azure portal and region-specific Azure subscriptions (namely, Germany, China, US Government Azure regions).

Classic Azure VMs use certificate-based authentication and authorization, which are generated on the classic Azure portal.  The new Azure portal supports Azure Active Directory (AD) based authentication and authorization along with provision and managing ARM-based VMs. [Learn more](vms-manage-azure-ad-and-region-specific.md).

### Nested virtualization
VMM 1711 supports Nested Virtualization feature that allows you to run Hyper-V inside a Hyper-V virtual machine. In other words, with nested virtualization, a Hyper-V host itself can be virtualized. Nested virtualization can be enabled out-of-band by using PowerShell and Hyper-V host configuration.

You can leverage this functionality to reduce your infrastructure expense for development and test scenarios. This feature also allows you to use third party virtualization management products with Microsoft hypervisor.

You can enable or disable the nested virtualization feature using SCVMM 1711. You can configure the VM as a Host in VMM and perform host operations from VMM on this VM. For example, VMM dynamic optimization will consider a nested VM host for placement.  [Learn more](vm-nested-virtualization.md).


### Migration of VMware VM (EFI firmware based VM) to Hyper-V VM

The current VMM migration for VMware VMs to Hyper-V only supports migration of BIOS-based VMs.

VMM 1711 release enables migration of EFI based VMware VMs to Hyper-V. VMware VMs that you migrate to Microsoft Hyper-V platform can take advantage of the generation 2 features.

As part of this release, the **Convert Virtual machine** wizard enables the VM migration based on the firmware type (BIOS or EFI), selects and defaults the Hyper-V VM generation appropriately: [Learn more](vm-convert-vmware.md).

1.	BIOS-based VMs are migrated to Hyper-V VM generation 1.
2.	EFI-based VMs are migrated to Hyper-V VM generation 2 . [Learn more].


### Performance improvement in host refresher

The SCVMM 1711 host refresher has undergone certain updates for performance improvement.

With these updates, in scenarios where the organization is managing large number of hosts and VMs with checkpoints – you would be able to observe significant and noticeable improvements in the performance of the job.

This improvement in performance has been validated in our lab with VMM instances managing 20 hosts - each host managing 45-100 VMs.

### Configuration of  SLB VIPs through VMM service templates
SDN in Windows 2016 can use Software Load Balancing (SLB) to evenly distribute network traffic among workloads managed by service provider and tenants. VMM 2016 currently supports deployment of  SLB Virtual IPs (VIPs) using power shell.

With VMM 1711, VMM supports configuration of SLB VIPs while deploying multi-tier application by using the service templates. [Learn more](sdn-configure-slb-vip.md).

### Configuration of encrypted VM networks through VMM

VMM 1711 supports encryption of VM networks. Using the new encrypted networks feature, end-to-end encryption can be easily configured on VM networks by using the Network Controller (NC). This encryption prevents traffic between two VMs on the same network and same subnet, from being read and manipulated.

The control of encryption is at the subnet level and encryption can be enabled/disabled for each subnet of the VM network. [Learn more](sdn-encrypt-networks.md).

## Storage

### Improvement in VMM storage QoS
Storage Quality of Service (SQoS) provides a way to centrally monitor and manage storage performance for virtual machines using Hyper-V and the Scale-Out File Server (SOFS) roles. The feature automatically improves storage resource fairness between multiple VMs using the same cluster and allows policy-based performance goals.

SCVMM 1711 supports the following improvements in SQoS:

- Extension of SQoS support beyond S2D - You can now assign storage QoS policies to clusters. [Learn more](qos-storage-clusters.md).
- Support for VMM private - You can assign a storage QoS policy while creating a cloud. [Learn more](cloud-create.md).
- Availability of storage QoS policies as templates - You can get storage QoS policies as templates. [Learn more](library-vm-templates.md).


## Networking

### Configuration of guest clusters in SDN through VMM

VMM currently supports guest clustering.  However, with the advent of the network controller (NC), Windows Server 2016 and System Center 2016, the configuration of guest clusters has undergone some change.

With the introduction of the network controller, VMs, which are connected to the virtual network are only permitted to use the IP address that the network controller assigns for communication. The network controller does not support floating IP addresses which are essential for technologies such as Microsoft failover clustering to work.

VMM 1711 release supports the floating IP functionality through the Software Load Balancer (SLB) in the SDN.

VMM 1711 supports guest clustering through an Internal Load Balancer (ILB) VIP. The ILB uses probe ports which are created on the guest cluster VMs to identify the active node.  At any given time, the probe port of only the active node responds to the ILB and all the traffic directed to the VIP is routed to the active node. [Learn more](sdn-guest-clusters.md).

### Enhanced console session in VMM
Console connect in VMM provides an alternative way to remote desktop to connect to the VM. This is most useful when the VM does not have any network connectivity or want to change network configuration that could break the network connectivity. Currently, the current console connect in VMM supports only basic session where clipboard text can only be pasted through **Type Clipboard Text** menu option.

VMM 1711 supports enhanced session that enables Cut **(Ctrl + X)**, **Copy (Ctrl + C)** and **Paste (Ctrl + V)** operations on the ANSI text and files available on the clipboard, there by copy/paste commands for text and files are possible from and to the VM. [Learn more](enhanced-console-session.md).


## Security

### Linux shielded VM
Windows Server 2016 introduced the concept of a shielded VM for Windows OS based VMs. Shielded VMs provide protection against malicious administrator actions both when VM’s data is at rest or an untrusted software is running on Hyper-V hosts.

With Windows Server 1709, Hyper-V introduces support for provisioning Linux shielded VMs and the same has been extended to VMM 1711. [Learn more](guarded-deploy-linux-vm.md).

### Fallback HGS configuration in VMM
Being at the heart of providing attestation and key protection services to run shielded VMs on Hyper-V hosts, the host guardian service (HGS) should operate even in situations of disaster. SCVMM 1711 supports this feature.

Using VMM 1711, a guarded host can be configured with a primary and a secondary pair of HGS URLS (an attestation and key protection URI). This capability will enable scenarios such as guarded fabric deployments spanning two data centers for disaster recovery purposes, HGS running as shielded VMs etc.

The primary HGS URLs will always be used in favor of the secondary.  If the primary HGS fails to respond after the appropriate timeout and retry count, the operation will be re-attempted against the secondary.  Subsequent operations will always favor the primary; the secondary will only be used when the primary fails.
[Learn more](guarded-fallback-hgs.md).
