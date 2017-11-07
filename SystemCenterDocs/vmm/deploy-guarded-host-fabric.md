---
ms.assetid: a013a64d-946d-4847-97b0-7f3fcb4b3dbf
title: Scenario-Deploy guarded hosts and shielded virtual machines in VMM
description: Describes how to set up guarded hosts and provision shielded VMs in the VMM fabric
author:  rayne-wiselman
ms.author: raynew
manager:  carmonm
ms.date:  11/07/2017
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---

# Scenario - Deploy guarded hosts and shielded virtual machines in VMM

]

This article provides an overview of deploying Hyper-V guarded hosts and shielded virtual machines in a System Center - Virtual Machine Manager (VMM) compute fabric.

Guarded fabrics provide additional protections for VMs to prevent tampering and theft by malicious administrators and malware. As a cloud service provider or private cloud administrator, you can deploy a guarded fabric that typically consists of a server running the host guardian service (HGS), one or more guarded Hyper-V host servers, and one or more shielded VMs running on those hosts. [Learn more about guarded fabrics](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms-top-node).

## Why do I need to protect VMs?

Virtual machines contain sensitive data and configuration that the VM owner may not want a fabric administrator to see. However, since all the data for VMs are stored in files, the data can easily be copied off and inspected by malware or a malicious administrator. Shielded VMs in Windows Server 2016 help prevent such attacks by rigorously attesting to the health of a Hyper-V host before booting up a VM, ensuring the VM can only be started in datacenters authorized by the VM owner, and enabling the guest OS to encrypt its own data through the use of a new, virtual TPM. The VM owner can select from the following two types of protection when creating a security-sensitive VM:
- **Encryption Supported**:  Ideal for enterprise private cloud scenarios where encryption of data at rest and in-flight is necessary, but the fabric administrators are still trusted. The VM console and other management conveniences remain available to fabric administrators.
- **Shielded**: The most secure deployment option, shielding prevents fabric administrators from connecting to the VM console or modifying security aspects of the VM configuration. VM owners can only access the VM through remote management tools they choose to enable. This is recommended for tenants running sensitive workloads on public or shared infrastructure.

[Learn more](https://technet.microsoft.com/en-us/windows-server-docs/security/guarded-fabric-and-shielded-vms#what-are-the-types-of-virtual-machines-that-a-guarded-fabric-can-run ) about the differences between encryption supported and shielded VMs.

## Managing a guarded fabric with VMM

The core guarded fabric infrastructure (consisting of one or more guarded Hyper-V hosts, the Host Guardian Service, and the artifacts needed to create shielded VMs) is included with Windows Server 2016 and must be configured according to the [guarded fabric documentation](https://technet.microsoft.com/en-us/windows-server-docs/security/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms-top-node).
Once set up, you can optionally use System Center 2016 - Virtual Machine Manager to simplify management of the guarded fabric.

VMM can be used to:

- **Provision and manage guarded hosts in the VMM fabric**: You can add and manage guarded hosts to the VMM fabric. A guarded host is a Hyper-V server that:
    - Meets the [guarded host prerequisites](https://technet.microsoft.com/en-us/windows-server-docs/security/guarded-fabric-shielded-vm/guarded-fabric-deployment-prerequisites#prerequisites-for-hyper-v-hosts-that-will-become-guarded-hosts).
    - Is authorized by the Host Guardian Service for the fabric to run shielded VMs. The HGS admin determines the requirements for hosts to successfully attest and become "guarded".
    - Is marked as guarded in VMM by configuring it to use the same HGS URLs as those specified in the global VMM settings.
- **Configure a shielded virtual hard disk and optionally a VM template**: Signed template disks (VHDX) used to deploy new shielded VMs can be stored in the VMM library for easy deployment. You can then use this VHDX in a VM template.
- **Provision and manage shielded VMs**: VMM supports the full lifecycle of shielded VMs. This includes:
    - Creating new shielded VMs from a signed template disk (VHDX), and optionally using a VM template.
    - Converting existing VMs to shielded VMs.

## Next steps

- [Provision guarded hosts in the VMM fabric](guarded-deploy-host.md)
