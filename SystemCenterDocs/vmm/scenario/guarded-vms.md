---
title: Provision shielded virtual machines in VMM
description: Describes how to add and provision shielded VMs in the VMM fabric. Shielding VMs helps keep them secure.
author: rayne-wiselman
ms.author: raynew
manager: cfreeman
ms.date: 10-12-2016
ms.topic: article
ms.prod: system-center-2016
ms.technology: virtual-machine-manager
---

# Scenario: Provision shielded virtual machines in the VMM fabric

>Applies To: System Center 2016 - Virtual Machine Manager

This article describes how to deploy shielded virtual machines in the System Center 2016 - Virtual Machine Manager (VMM) compute fabric.

Guarded fabric helps guarantee the security of Hyper-V virtual machines. As a cloud service provider, or private cloud administrator, you can deploy a guarded fabric that typically consists of a server running the host guardian service (HGS), one or more guarded Hyper-V host servers, and a set of shielded VMs running on those hosts. [Learn more](https://technet.microsoft.com/windows-server-docs/security/guarded-fabric-and-shielded-vms) about guarded fabric.

You can deploy shielded VMs in VMM in a couple of ways:

- Turn an existing VM into a shielded VM
- Create a new shielded VM using a signed virtual machine hard disk (VHDX), or a VM template.

> Note that converting existing VMs into shielded VMs isn't supported right now.

## Before you start


You set up shielded VMs in the VMM fabric as follows:

1. **Prepare an HGS server**: You should have an HGS server deployed. [Learn more](https://technet.microsoft.com/windows-server-docs/security/guarded-fabric-shielded-vm/guarded-fabric-setting-up-the-host-guardian-service-hgs).
2. **Set up VMM**: You’ll need to configure global HGS settings in VMM, and set up at least one guarded host. If guarded hosts belong to a cloud, the cloud should be enabled to support shielded VMs. [Learn more](guarded-hosts.md).
3. **Prepare shielded data files**: To use the signed template disks in the VMM library, tenants must prepare one or more shielding data files. This file contains all the secrets that a tenant needs to deploy a VM, including the unattend file used to specialize the VM, certificates, administrator account passwords. The file also specifies which guarded fabric a tenant trusts to host their VM, and information about the signed template disks. The file is encrypted and can only be read by a host in a guarded fabric trusted by the tenant. [Learn more](https://technet.microsoft.com/windows-server-docs/security/guarded-fabric-shielded-vm/guarded-fabric-tenant-creates-shielding-data).
4. **Set up host group**: For easy management, we recommend that shielded VMs should be placed in a dedicated VMM host group.
5. **Verify existing VM requirements**: If you want to convert an existing VM to shielded, note the following:
    - The VM must be generation 2.
    - The VHDX operating system for the VM should support generation 2 VMs and the Microsoft secure boot template.
    -   Windows Server 2016, Windows Server 2012 R2, Windows Server 2012
    -   Windows 10, Windows 8.1, Windows 8
    - The OS disk for the VM must use GUID Partition Table. This is required for generation 2 VMs to support UEFI.
6. **Set up helper VHD**: The hosting service provider will need to create a VM that acts as a helper VHD for converting existing machines. [Learn more](https://technet.microsoft.com/windows-server-docs/security/guarded-fabric-shielded-vm/guarded-fabric-vm-shielding-helper-vhd).

## Enable shielding for existing VM

You can enable shielding for a VM currently running on a host in the VMM fabric that isn’t guarded.
1.	Ensure you have all the prerequisites in place before you start.
2.	Take the VM offline.
3.	We recommend that you enable BitLocker on all disks attached to the VM before moving it to the guarded host.
4.	Select the VM > **Properties** > **Shield**, and select a shielding data file.
5.	Shut down the VM, export from non-guarded host, and import it to a guarded host. Only a guarded host can access the VM data.

## Provision a new shielded VM

1.	Make sure you have all the prerequisites in place before you start.
2.	In **VMs and Services**, click **Create Virtual Machine** to open the Create Virtual Machine Wizard.
3.	In **Select Source**, click **Use an existing virtual machine, VM template, or virtual hard disk** > **Browse**.
4.	You can either select the template disk, or the shielded VM template.
5.	In **Select Shielding Data File**, click **Browse** > **Import Shielding Data** > **Browse**. Select a shielding data file you create. Click **Import** > **OK** > **Next**.
6.	Follow [these instructions](../manage/manage-vm-template.md) to complete the wizard, and to deploy the VM on a host/cloud.

When you complete the wizard, VMM creates a new shielded VM from the disk or template:

1.	The template disk (VHDX) file is copied from the VMM library
2.	VM provisioning decrypts the data in the shielding data file, completes any substitution strings in the unattend.xml file, and copies additional files from the shielding data file to the operating system drive (for example the RDP certificate).
3.	The VM restarts, is customized, and re-encrypted with BitLocker. The BitLocker full volume encryption key is stored in the virtual TPM of the new VM.  You can track the VM status in Jobs.
4.	VM customization is complete when the shutdown command in the unattend.xml file runs, the VM remains switched off.  If customization gets stuck, check the unattend.xml file by running it on an unshielded VM, or on a VM that supports encryption.
5.	After VMM detects that specialization has finished, it start the VM and sends status that the VM was created successfully.

## Next steps

- [Manage virtual machine settings](../manage/manage-vm-settings.md)
