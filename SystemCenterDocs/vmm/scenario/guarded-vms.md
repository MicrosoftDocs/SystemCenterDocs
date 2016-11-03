---
ms.assetid: 56e1b31e-1d0c-4844-9625-bcd051dd189e
title: Provision shielded virtual machines in VMM
description: Describes how to add and provision shielded VMs in the VMM fabric. Shielding VMs helps keep them secure.
author: rayne-wiselman
ms.author: raynew
manager: cfreeman
ms.date: 11/01/2016
ms.topic: article
ms.prod: system-center-2016
ms.technology: virtual-machine-manager
---

# Provision shielded virtual machines in the VMM fabric

>Applies To: System Center 2016 - Virtual Machine Manager

This article describes how to deploy shielded virtual machines in the System Center 2016 - Virtual Machine Manager (VMM) compute fabric.

You can deploy shielded VMs in VMM in a couple of ways:

- Convert an existing VM into a shielded VM
- Create a new shielded VM using a signed virtual machine hard disk (VHDX), and optionally a VM template.

## Before you start

[Watch](https://channel9.msdn.com/Blogs/hybrid-it-management/Demo-Creating-a-Shielded-VM-using-System-Center-2016-Virtual-Machine-Manager-VMM) a video that provides a quick, two-minute overview of provisioning shielded VMs in VMM. Then, make sure you've done the following:

1. **Prepare an HGS server**: You should have an HGS server deployed. [Learn more](https://technet.microsoft.com/windows-server-docs/security/guarded-fabric-shielded-vm/guarded-fabric-setting-up-the-host-guardian-service-hgs).
2. **Set up VMM**: You need to configure global HGS settings in VMM, and set up at least one guarded host. If guarded hosts belong to a cloud, the cloud should be enabled to support shielded VMs. [Learn more](guarded-hosts.md).
3. **Prepare a shielded VHDX and VM template**: You deploy shielded VMs from a shielded virtual hard disk (VHDX), optionally using a VM template. [Learn more](guarded-template.md) about preparing these.
4. **Prepare shielding data files**: To use the signed template disks in the VMM library, tenants must prepare one or more shielding data files. This file contains all the secrets that a tenant needs to deploy a VM, including the unattend file used to specialize the VM, certificates, administrator account passwords. The file also specifies which guarded fabric a tenant trusts to host their VM and information about the signed template disks. The file is encrypted and can only be read by a host in a guarded fabric trusted by the tenant. [Learn more](https://technet.microsoft.com/windows-server-docs/security/guarded-fabric-shielded-vm/guarded-fabric-tenant-creates-shielding-data).
5. **Set up host group**: For easy management, we recommend that guarded hosts be placed in a dedicated VMM host group.
6. **Verify existing VM requirements**: If you want to convert an existing VM to shielded, note the following:
    - The VM must be generation 2 and have the Microsoft Windows Secure Boot template enabled
    - The operating system on the disk must be one of:
    -   Windows Server 2016, Windows Server 2012 R2, Windows Server 2012
    -   Windows 10, Windows 8.1, Windows 8
    - The OS disk for the VM must use GUID Partition Table. This is required for generation 2 VMs to support UEFI.
7. **Set up helper VHD**: The hosting service provider will need to create a VM that acts as a helper VHD for converting existing machines. [Learn more](guarded-template.md#configure-the-shielding-helper-vhd).

## Adding shielding data files to VMM

Before you can convert an existing VM to a shielded VM or provision a new shielded VM from a template, the VM owner must generate a shielding data file and add it to VMM.

If you do not already have a shielding data file imported, complete the following steps:

1. [Create a shielding data file](https://technet.microsoft.com/en-us/windows-server-docs/security/guarded-fabric-shielded-vm/guarded-fabric-tenant-creates-shielding-data) if you don't already have one. Make sure the shielding data file authorizes the hosting fabric VMM manages to run your shielded VMs.
> [!NOTE] Be sure to import the correct type of shielding data file for the operation you are trying to perform. Different shielding data files are required for provisioning new shielded VMs and converting existing VMs.
2. In the VMM console, click **Library** > **Import Shielding Data** > **Browse** and select your shielding data file.
3. Specify a friendly name for the shielding data file in **Name** and optionally add a description. It is recommended that you indicate whether the shielding data file is intended for use with existing or new VMs in its name to make it easier to find again.
4. Click **Import** to save the shielding data in VMM.

To manage your imported shielding data files, go to **Library** > **VM Shielding Data** (under "Profiles").

## Provision a new shielded VM

1.	Make sure you have all the prerequisites in place before you start.
2.	In **VMs and Services**, click **Create Virtual Machine** to open the Create Virtual Machine Wizard.
3.	In **Select Source**, click **Use an existing virtual machine, VM template, or virtual hard disk** > **Browse**.
4.	Select a shielded VM template or signed template disk. Both are identified by the shield icon ![Shield Icon in VMM](../media/guarded-shield.png).
5.	In **Select Shielding Data File**, click **Browse** and select a shielding data file. Only shielding data files that can be used to create a new shielded VM will be shown. Click **OK** > **Next** to continue.
6.	Follow [these instructions](../manage/manage-vm-template.md) to complete the wizard, and to deploy the VM on a host/cloud.

When you complete the wizard, VMM creates a new shielded VM from the disk or template:

1.	The template disk (VHDX) file is copied from the VMM library
2.	VM provisioning decrypts the data in the shielding data file, completes any substitution strings in the unattend.xml file, and copies additional files from the shielding data file to the operating system drive (for example, the RDP certificate).
3.	The VM restarts, is customized, and re-encrypted with BitLocker. The BitLocker full volume encryption key is stored in the virtual TPM of the new VM.
4.	VM customization is complete when the shutdown command in the unattend.xml file runs, the VM remains switched off.  If customization gets stuck, check the unattend.xml file by running it on an unshielded VM, or using an encryption-supported shielding data file that allows console access.
5.	After VMM detects that specialization has finished, it will update its status to indicate the VM is created and, if selected, start up the VM.

## Shield an existing VM

You can enable shielding for a VM currently running on a host in the VMM fabric that isn't guarded.

1.	Ensure you have all the prerequisites in place before you start.
2.	Take the VM offline.
3.	We recommend that you enable BitLocker on all disks attached to the VM before moving it to the guarded host.
4.	Select the VM > **Properties** > **Shield**, and select a shielding data file.
5.	Shut down the VM, export from non-guarded host, and import it to a guarded host. Only a guarded host can access the VM data.

## Next steps

- [Manage virtual machine settings](../manage/manage-vm-settings.md)
