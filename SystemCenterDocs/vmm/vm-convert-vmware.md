---
ms.assetid: 28a3bb81-979c-4ebe-aa07-7ba7ecfb6efc
title: Convert a VMware VM to Hyper-V in the VMM fabric
description: This article describes how to convert VMware VMs in VMM fabric to Hyper-V
author:  rayne-wiselman
ms.author: raynew
manager:  carmonm
ms.date:  10/16/2016
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---


# Convert a VMware VM to Hyper-V in the VMM fabric

>Applies To: System Center 2016 - Virtual Machine Manager


This article describes how to convert VMware VMs in the System Center 2016 - Virtual Machine Manager (VMM) fabric to Hyper-V.


There are currently a couple of methods for converting VMWare VMs to Hyper-V:

- **Convert Virtual Machine Wizard**: In the VMM console you can use this wizard. This method has a number of limitations:
- Supported for vSphere 4.1 onwards.
	- You can't convert VMware workstations
	- You can't convert VMs with virtual hard disks connected to an IDE bus
	- Online conversions aren't supported. You need to power off the VMware VMs.
	- Anti-virus apps must be supported.
	- VMware tools must be uninstalled from the guest operating system of the VM.
- [Microsoft Virtual Machine Converter](https://technet.microsoft.com/library/dn873998.aspx): This standalone tool converts VMware VMs to Hyper-V hosts or Azure VMs. It also converts physical machines and disks to Hyper-V hosts. IMPORTANT: This tool is in the process of retirement. It won't be available after June 3, 2017. [Learn more](https://blogs.technet.microsoft.com/scvmm/2016/06/04/important-update-regarding-microsoft-virtual-machine-converter-mvmc/)
- Azure Site Recovery currently doesn't have to ability for a direct VMware to Hyper-V conversion. [Read more](https://feedback.azure.com/forums/256299-site-recovery/suggestions/10050060-asr-to-support-vmware-to-hyper-v-protection-migrat) about up-voting this solution.


## Convert using the wizard

1. Click **VMs and Services** > **Home** > **Create** > **Create Virtual Machines** > **Convert Virtual Machine**.
2. In **Convert Virtual Machine Wizard** > **Select Source** click **Browse** and inS**Select Virtual Machine Source** select the VMware VMs you want to convert.
3. In **Specify Virtual Machine Identity** modify the machine name and description as required.
4. In **Virtual Machine Configuration** specify the number of processor and memory settings.
5. In **Select Host** select a Hyper-V host for placement. In **Select Path** configure the storage location on the host for the VM files. The default VM paths are listed.
6. In **Select Networks** select the logical network, virtual network, and the VLAN as applicable. The list matches whatever is configured on the physical adapters of the host.
7. In **Add Properties** configure settings. In **Summary** review the settings and select **Start the virtual machine after deploying it** if required. Then click **Create** to start the conversion. Verify the VM was converted in **VMs and Services** > **Home** > **Show** > **VMs**.

## Next steps

[Manage the VM settings](vm-settings.md)
