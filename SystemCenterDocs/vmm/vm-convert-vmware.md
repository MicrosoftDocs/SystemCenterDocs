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
- Support for vSphere (ESXi) 4.1, 5.0, 5.1, 5.5, 6.0
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

::: moniker range="sc-vmm-1711"

## Convert  EFI based VM to Hyper-V generation 2 VM (Technical preview content - under construction)
The System Center Preview Virtual Machine Manager 1711 (SCVMM 1711) release enables migration of EFI based VMware VMs to Hyper-V. VMware VMs that you migrate to Microsoft Hyper-V platform can now take the advantage of generation 2 features.

As part of this release, the **Convert Virtual Machine** wizard enables the VM's migration based on the firmware type (BIOS or EFI), selects and defaults the Hyper-V VM generation appropriately.

- BIOS-based VMs are migrated to Hyper-V VM generation 1.
- EFI-based VMs are migrated to Hyper-V VM generation 2.

### Before you start
Ensure the following prerequisites are met:
1.	VMware VMs with firmware type as EFI
2.	VMware ESXi Hosts added in System Center VMM

### Conversion procedure
1. To convert, follow the [above procedure](#convert-using-the-wizard), select **Generation 2** in step 4.

    ![vm conversion to gen 2](media\vm-conversion\vm-conversion-select-gen2.png)

2. Once the VM is converted, you can see the Generation 2 VM as follows:

    ![vm conversion to gen 2](media\vm-conversion\vm-conversion-gen2-created.png)

> ![NOTE]
>
- Disk conversion (from “vmdk” to “VHDX/VHD”) is enhanced to be ~50% faster than earlier.
- PowerShell commands allow the user to provide the disk type for the target Hyper-V VM, which will enable the VMware thick provisioned disk to be migrated as Hyper-V dynamic disk or vice versa, based upon the requirements.   

## PowerShell commands
```powershell

New-SCV2V -VMHost <Host> -VMXPath <string> [-EnableVMNetworkOptimization <bool>] [-EnableMACAddressSpoofing
<bool>] [-VMMServer <ServerConnection>] [-LibraryServer <LibraryServer>] [-JobGroup <guid>] [-Trigger] [-VhdType
{UnknownType | DynamicallyExpanding | FixedSize}] [-VhdFormat {VHD | VHDX}] [-Description <string>] [-Name
<string>] [-Owner <string>] [-UserRole <UserRole>] [-Path <string>] [-StartVM] [-CPUCount <byte>]
[-CPURelativeWeight <int>] [-CPUType <ProcessorType>] [-MemoryMB <int>] [-Generation <int>] [-DelayStartSeconds
<int>] [-StartAction {NeverAutoTurnOnVM | AlwaysAutoTurnOnVM | TurnOnVMIfRunningWhenVSStopped}] [-StopAction
{SaveVM | TurnOffVM | ShutdownGuestOS}] [-LogicalNetwork <LogicalNetwork>] [-VMNetwork <VMNetwork>]
[-NoConnection] [-MACAddress <string>] [-MACAddressType <string>] [-SourceNetworkConnectionID <string>]
[-VirtualNetwork <VirtualNetwork>] [-VirtualNetworkAdapter <VirtualNetworkAdapter>] [-VLanEnabled <bool>] [-VLanID
<uint16>] [-OverridePatchPath <string>] [-SkipInstallVirtualizationGuestServices] [-NetworkLocation <string>]
[-NetworkTag <string>] [-RunAsynchronously] [-PROTipID <guid>] [-JobVariable <string>]  [<CommonParameters>]
```

::: moniker-end

## Next steps

[Manage the VM settings](vm-settings.md)
