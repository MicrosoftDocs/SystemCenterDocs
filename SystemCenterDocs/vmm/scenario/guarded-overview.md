---
title: Scenario-Deploy guarded hosts and shielded virtual machines in VMM
description: Describes how to set up guarded hosts and provision shielded VMs in the VMM fabric
author:  rayne-wiselman
ms.author: raynew
manager:  cfreeman
ms.date:  2016-10-12
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---

# Scenario: Deploy guarded hosts and shielded virtual machines in VMM

>Applies To: System Center 2016 - Virtual Machine Manager

This article provides an overview of deploying Hyper-V guarded hosts and shielded virtual machines in the System Center 2016 - Virtual Machine Manager (VMM) compute fabric.

Guarded fabric helps guarantee the security of Hyper-V virtual machines. As a cloud service provider, or private cloud administrator, you can deploy a guarded fabric that typically consists of a server running the host guardian service (HSG), one or more guarded Hyper-V host servers, and a set of shielded VMs running on those hosts. [Learn more](https://technet.microsoft.com/windows-server-docs/security/guarded-fabric-and-shielded-vms) about guarded fabric.

## Why do I need to protect VMs?

Virtual machines contain an operating system, applications, and dependencies in the form of file data. This file data needs protection from internal and external threats, and there are a couple of mechanisms to do this:
- **Encryption**:  You can deploy Virtual TPM and encryption to help with security for generation 2 VMs. Such protection is useful but relies upon the premise that fabric administrators are fully trusted.
- **Shielding**: You can deploy shielded VMs to provide protection against malicious administrator actions, and untrusted software running on Hyper-V hosts. Shielded VMs have the following characteristics:
    - The state and data of a shielded VM is protected against inspection, theft, and tampering from both malware and datacenter admins.
    - Encryption of at-rest and in-flight data. Virtual TPM enables disk encryption. Live migrate and VM state are also encrypted.
    - Host admins can’t access guest VM secret, or run arbitrary kernel-mode code.
    - There’s an attestation of VM health so that VM workloads can only run on healthy hosts.
    - After a VM is encrypted and shielding is enabled, it can’t be disabled by the administrator.
    - A shielded VM is available only via the network, and not via a VM console connection. The admin can’t change this setting.

[Learn more](https://technet.microsoft.com/en-us/windows-server-docs/security/guarded-fabric-and-shielded-vms#what-are-the-types-of-virtual-machines-that-a-guarded-fabric-can-run ) about comparing encryption and shielding capabilities.

## Guarded fabric deployment in VMM

To deploy guarded fabric, you need to make sure you have the deployment prerequisites in place, set up HSG, set up guarded hosts to work with HSG, and deploy shielded VMs.

VMM can be optionally deployed with guarded fabric to provide the following:

- **Provision and management of guarded hosts in the VMM fabric**: You can add and manage guarded hosts to the VMM fabric. A guarded host is a Hyper-V server that:
    - Meets the guarded host prerequisites.
    - Is registered with the HGS. If the HGS is used admin-trusted attestation, the Hyper-V host must belong to a specific security group. If the HGS uses TPM-trusted attestation, the TPM identifier for the host must be registered with HGS.
    - Is marked as guarded in VMM by configuring it to use the same HGS URLs as those specified in the global HGS settings.
- **Provision and management of shielded VMs**: There are a few options here:
    - You can create new VMs from a shielded VM template or signed virtual hard disk (VHDX)
    - You can enable shielding for existing VMs

## Next steps

[Provision guarded hosts in the VMM fabric](guarded-hosts.md)
