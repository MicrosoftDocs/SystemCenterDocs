---
ms.assetid: 28a3bb81-979c-4ebe-aa07-7ba7ecfb6efc
title: Convert a VMware VM to Hyper-V in the VMM fabric
description: This article describes how to convert VMware VMs in VMM fabric to Hyper-V.
author: jyothisuri
ms.author: jsuri
ms.date: 06/03/2025
ms.topic: how-to
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom:
  - engagement-fy24
  - sfi-image-nochange
---

# Convert a VMware VM to Hyper-V in the VMM fabric

This article describes how to convert VMware VMs in the System Center Virtual Machine Manager (VMM) fabric to Hyper-V.

::: moniker range=">=sc-vmm-2019 <=sc-vmm-2022"

You can convert the VMs using the *Convert Virtual Machine* wizard. You can use this wizard from the VMM console.

::: moniker-end

::: moniker range="sc-vmm-2019"

VMM 2019 UR3 supports the conversion of VMware VMs to Hyper-V and Azure Local 20H2. [Learn more about support to Azure Local 20H2](deploy-manage-azure-stack-hci.md).

::: moniker-end

::: moniker range="sc-vmm-2019"

>[!Important]
  >- See [system requirements](system-requirements.md) for supported versions of vSphere (ESXi).
  >- You can't convert VMware workstations.
  >- You can't convert VMs with virtual hard disks connected to an IDE bus.
  >- Anti-virus apps must be supported.
  >- Online conversions aren't supported. You need to power off the VMware VMs.
  >- VMware tools must be uninstalled from the guest operating system of the VM.
  >- We recommend upgrading to VMM 2022 UR2 to convert your VMware VMs to Hyper-V four times faster.

>[!NOTE]
> We recommend that no more than ten conversions be triggered parallelly from the same ESXi source to the same Hyper-V destination. If the source-destination pair is different, VMM can support up to 100 VM conversions in parallel, with the remaining conversions queued. However, we recommend staging the VM conversions in smaller batches for higher efficiency.

>[!NOTE]
> After conversion, all the VM disks except for the OS disk will be offline. This is because the `NewDiskPolicy` parameter is set to *offlineALL* on VMware VMs by default. To override this and to have the new disks brought online after conversion, you can make one of the following changes to your VMware VM disk policy before initiating the conversion:
  >- `Set-StorageSetting -NewDiskPolicy OfflineShared`: To have all the new shared bus disks offline and all the new local bus disks online
  >- `Set-StorageSetting -NewDiskPolicy OnlineAll`: To have all the new disks online, regardless of whether the disks are on a local or shared bus.
::: moniker-end

::: moniker range="sc-vmm-2022"
>[!Important]
  >- See [system requirements](system-requirements.md) for supported versions of vSphere (ESXi).
  >- You can't convert VMware workstations.
  >- You can't convert VMs with virtual hard disks connected to an IDE bus.
  >- Anti-virus apps must be supported.
  >- Online conversions aren't supported. You need to power off the VMware VMs.
  >- VMware tools must be uninstalled from the guest operating system of the VM.
  >- VMware VMs residing on vSAN-type storage can't be converted to Hyper-V with SCVMM.
  >- We recommend upgrading to VMM 2022 UR2 to convert your VMware VMs to Hyper-V four times faster.

>[!NOTE]
> We recommend that no more than ten conversions be triggered parallelly from the same ESXi source to the same Hyper-V destination. If the source-destination pair is different, VMM can support up to 100 VM conversions in parallel, with the remaining conversions queued. However, we recommend staging the VM conversions in smaller batches for higher efficiency.

>[!NOTE]
> After conversion, all the VM disks except for the OS disk will be offline. This is because the `NewDiskPolicy` parameter is set to *offlineALL* on VMware VMs by default. To override this and to have the new disks brought online after conversion, you can make one of the following changes to your VMware VM disk policy before initiating the conversion:
  >- `Set-StorageSetting -NewDiskPolicy OfflineShared`: To have all the new shared bus disks offline and all the new local bus disks online
  >- `Set-StorageSetting -NewDiskPolicy OnlineAll`: To have all the new disks online, regardless of whether the disks are on a local or shared bus.

::: moniker-end

::: moniker range="sc-vmm-2016"
There are currently a couple of methods for converting VMware VMs to Hyper-V:

- **Convert Virtual Machine Wizard**: You can use this wizard from the VMM console.

  >[!Important]
    >- See [system requirements](system-requirements.md) for supported versions of vSphere (ESXi).
    >- You can't convert VMware workstations.
    >- You can't convert VMs with virtual hard disks connected to an IDE bus.
    >- Anti-virus apps must be supported.
    >- Online conversions aren't supported. You need to power off the VMware VMs.
    >- VMware tools must be uninstalled from the guest operating system of the VM.

- [**Microsoft Virtual Machine Converter**](https://techcommunity.microsoft.com/t5/system-center-blog/microsoft-virtual-machine-converter-3-0-is-now-available-for/ba-p/349874): This standalone tool converts VMware VMs to Hyper-V hosts or Azure VMs. It also converts physical machines and disks to Hyper-V hosts.

  >[!Important]
  > This tool has reached end of support.

::: moniker-end

::: moniker range=">=sc-vmm-2016 <=sc-vmm-2022"

## Convert using the wizard

1. Select **VMs and Services** > **Home** > **Create** > **Create Virtual Machines** > **Convert Virtual Machine**.
2. In **Convert Virtual Machine** wizard > **Select Source**, select **Browse** and in **Select Virtual Machine Source**, select the VMware VMs you want to convert.
3. In **Specify Virtual Machine Identity**, modify the machine name and description as required.

::: moniker-end

::: moniker range="sc-vmm-2016"

4. In **Virtual Machine Configuration**, specify the number of processors and memory settings.

::: moniker-end

::: moniker range=">=sc-vmm-2019 <=sc-vmm-2022"

4. In **Virtual Machine Configuration**, specify the number of processors and memory settings. Choose **Generation 2** if the source VMware VM is configured with UEFI firmware or choose **Generation 1** if the source VMware VM is configured with BIOS firmware.

::: moniker-end

::: moniker range=">=sc-vmm-2016 <=sc-vmm-2022"

5. In **Select Host**, select a Hyper-V host/Azure Local machine (applicable from VMM 2019 UR3 and later) for placement. In **Select Path**, configure the storage location on the host for the VM files. The default VM paths are listed.
6. In **Select Networks**, select the logical network, virtual network, and the VLAN as applicable.
7. In **Add Properties**, configure the required settings. In **Summary**, review the settings, and select **Start the virtual machine after deploying it** if necessary.
8. Select **Create** to start the conversion.
   Verify the VM's conversion in **VMs and Services** > **Home** > **Show** > **VMs**.
::: moniker-end

::: moniker range="sc-vmm-2016"

## Convert EFI-based VM to Hyper-V Generation 2 VM
System Center VMM enables the migration of EFI-based VMware VMs to Hyper-V. VMware VMs that you migrate to Microsoft Hyper-V platform can now take advantage of Generation 2 features.

::: moniker-end

::: moniker range="sc-vmm-2022"

>[!Note]
>On converting VMware BIOS-based VMs with more than four disks, not all disks gets attached to the new Hyper-V VM after conversion due to the limitations with IDE standards. To attach the remaining disks, run this [PowerShell script](https://download.microsoft.com/download/aad31a6a-b2d9-42fe-bfeb-064af733107d/AttachDiskScript.ps1) after converting the VM.

::: moniker-end

::: moniker range=">=sc-vmm-2019 <=sc-vmm-2022"

> [!NOTE]
> - PowerShell commands allow you to provide the disk type for the target Hyper-V VM, which will enable the VMware thick provisioned disk to be migrated as Hyper-V dynamic disk or vice versa, based on the requirements.

## Convert using PowerShell cmdlets

Here are the sample cmdlets:

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

:::moniker range=">=sc-vmm-2016 <=sc-vmm-2022"

## Convert VMware VMs to Hyper-V faster

- As a prerequisite to start converting VMware VMs to Hyper-V four times faster, upgrade to SCVMM 2022 UR2 or later.
- As part of SCVMM 2022 UR2, a new registry named **V2VTransferChunkSizeBytes** is introduced at *HKLM:\SOFTWARE\Microsoft\Microsoft System Center Virtual Machine Manager Agent* in the Hyper-V hosts managed by SCVMM.
- This registry of type REG_DWORD, with a value of *2147483648*, which is 2 GB in bytes has to be set on every Hyper-V host managed by VMM by running [this script](https://download.microsoft.com/download/2/c/a/2caf6779-853a-4455-9c67-a0d2b1e2ccfe/Script%20To%20Add%20Registry%20with%20new%20Chunk%20Size%20On%20All%20Hosts.ps1) from the VMM Console.
- Alternatively, if you want to set this registry value in a single host and not on all the hosts, run [this script](https://download.microsoft.com/download/4/4/6/446e9dac-0356-44ce-a0c9-707a8d3e2bb0/Script%20To%20Add%20Registry%20with%20new%20Chunk%20Size%20On%20Single%20Host.ps1) from the VMM Console.
- After setting this registry value, if you remove any Hyper-V host(s) from SCVMM, stale entries for this registry might remain. If the same host(s) is re-added to SCVMM, the previous value of registry **V2VTransferChunkSizeBytes** will be honored.

:::moniker-end


:::moniker range="sc-vmm-2025"

VMM offers a simple wizard-based experience for V2V (Virtual to Virtual) conversion.

>[!Important]
>- Review the [system requirements](./system-requirements.md) for the supported vCenter/ESXi servers.
>- Review the [list of ports](./plan-ports-protocols.md) required for ESXi and Hyper-V hosts and vCenter server.
>- Review [this article](./manage-vmware-hosts.md) about managing vCenter servers, ESXi hosts and VMware VMs in SCVMM.
>- You can't convert VMware workstations.
>- You can't convert VMs with virtual hard disks connected to an IDE bus.
>- VMware tools must be uninstalled from the guest operating system of the VM.
>- VMware VMs residing on vSAN-type storage can't be converted to Hyper-V with SCVMM.
>- Online conversions aren't supported through SCVMM.
>- We recommend upgrading to VMM 2025 to convert your VMware VMs to Hyper-V four times faster and to have an enhanced conversion experience.

## Start by bringing your vCenter server and the source ESXi hosts under SCVMM management

1. Create [Run as account](./account-runas.md) for vCenter Server Administrator role in VMM. These administrator credentials are used to manage vCenter server and ESXi hosts.

    :::image type="content" source="media/vm-convert-vmware/create-run-as-account.png" alt-text="Screenshot of create run as account page." lightbox="media/vm-convert-vmware/create-run-as-account.png":::
 
2. In the VMM console, under **Fabric**, select **Servers > Add VMware vCenter Server**.

    :::image type="content" source="media/vm-convert-vmware/add-vmware-vcenter-server.png" alt-text="Screenshot of add VMware vCenter server option." lightbox="media/vm-convert-vmware/add-vmware-vcenter-server.png":::

3. In the **Add VMware vCenter Server** page, do the following:<br>
  a. **Computer name**: Specify the vCenter server name.<br>
  b. **Run As account**: Select the Run As account created for vSphere administrator.<br>

      :::image type="content" source="media/vm-convert-vmware/specify-vcenter-server.png" alt-text="Screenshot of specify vCenter server page." lightbox="media/vm-convert-vmware/specify-vcenter-server.png":::

4.	Select **Finish**.

5.	On the **Import Certificate** page, select **Import**.

    :::image type="content" source="media/vm-convert-vmware/import-certificate.png" alt-text="Screenshot of import certificate page." lightbox="media/vm-convert-vmware/import-certificate.png":::
 
6.	After the successful addition of the vCenter server, all the ESXi hosts under the vCenter are discovered in VMM.

7.	In the VMM console, under **Fabric**, select **Servers > Add VMware ESX Hosts and Clusters**.

    :::image type="content" source="media/vm-convert-vmware/add-vmware-esx-hosts-and-clusters.png" alt-text="Screenshot of add VMware ESX hosts and clusters page." lightbox="media/vm-convert-vmware/add-vmware-esx-hosts-and-clusters.png":::

8.	In the **Add Resource Wizard**,<br>
    a. Under **Credentials**, select the Run as account with administrator privileges on the ESXi host to be added and select **Next**.<br>

      :::image type="content" source="media/vm-convert-vmware/add-resource-wizard.png" alt-text="Screenshot of add resource wizard page." lightbox="media/vm-convert-vmware/add-resource-wizard.png":::

    b.	Under **Target Resources**, select all the ESXi clusters that need to be added to VMM and select **Next**.

      :::image type="content" source="media/vm-convert-vmware/select-esx-computers.png" alt-text="Screenshot of select ESXi computers page." lightbox="media/vm-convert-vmware/select-esx-computers.png":::

    c.	Under **Host Settings**, select the host group where you want to add the VMs and select **Next**.

      :::image type="content" source="media/vm-convert-vmware/add-virtual-machine-path.png" alt-text="Screenshot of add virtual machine path page." lightbox="media/vm-convert-vmware/add-virtual-machine-path.png":::

    d. Under **Summary**, review the settings and select **Finish**. Along with the hosts, associated VMs will also get added.
 
      :::image type="content" source="media/vm-convert-vmware/confirm-settings.png" alt-text="Screenshot of confirm settings page." lightbox="media/vm-convert-vmware/confirm-settings.png":::

9. Select **Fabric** > **Servers**> **All Hosts** and in the host group, check the status of each host or cluster. The **Host Status** should be either **OK** or **OK (limited)**.

10. If the status is limited, it means you've enabled the setting **Communicate with VMware ESX hosts in secure mode** but haven't yet imported a certificate from each vSphere host. To modify the security setting, right-click the vCenter server > **Properties** > **Security**.

11. To import the certificate, select each relevant host name > **Properties** > **Management** > **Retrieve** > **OK**. The host status must be **OK** after the import.

## Convert your VMware VMs to Hyper-V

Now that your VMware VMs are discovered and manageable by VMM, you can convert these VMs to Hyper-V by following these instructions:

1. Ensure the VMware VMs that are to be converted are in the **Stopped** state and that there are no snapshots associated with them.

2. Select **VMs and Services > Home > Convert Virtual Machine**.

3.	In **Convert Virtual Machine** wizard > **Select Source**, select **Browse**, and in **Select Virtual Machine Source**, select the VMware VM you want to convert.

4.	In **Specify Virtual Machine Identity**, modify the machine name and description as required.

5.	In **Virtual Machine Configuration**, specify the number of processors and memory settings. Choose **Generation 2** if the source VMware VM is configured with UEFI firmware or choose **Generation 1** if the source VMware VM is configured with BIOS firmware.

6.	In **Select Host**, select a Hyper-V host/Azure Local for placement. In **Select Path**, configure the storage location on the host for the VM files. The default VM path is listed.

7. In **Select Networks**, select the logical network, virtual network, and the VLAN as applicable.

8.	In **Add Properties**, configure the required settings. In **Summary**, review the settings, and select **Start the virtual machine after deploying it** if necessary.

9.	Select **Create** to start the conversion. Verify the VMs' conversion in **VMs and Services > Home > Show > VMs**.

>[!Note]
>On converting VMware BIOS-based VMs with more than four disks, not all disks gets attached to the new Hyper-V VM after conversion due to the limitations with IDE standards. To attach the remaining disks, run this [PowerShell script](https://download.microsoft.com/download/aad31a6a-b2d9-42fe-bfeb-064af733107d/AttachDiskScript.ps1) after converting the VM.


>[!Note]
>After conversion, all the VM disks except for the OS disk will be offline. This is because the `NewDiskPolicy` parameter is set to *offlineALL* on VMware VMs by default. To override this and to have the new disks brought online after conversion, you can make one of the following changes to your VMware VM disk policy before initiating the conversion:<br>
>- `Set-StorageSetting -NewDiskPolicy OfflineShared`: To have all the new shared bus disks offline and all the new local bus disks online.
>- `Set-StorageSetting -NewDiskPolicy OnlineAll`: To have all the new disks online, regardless of whether the disks are on a local or shared bus.

## Convert using PowerShell cmdlet

Here's the PowerShell cmdlet for V2V conversion via SCVMM with all the parameters:

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

>[!Note]
> We recommend that no more than ten conversions be triggered parallelly from the same ESXi source to the same Hyper-V destination. If the source-destination pair is different, VMM can support up to 100 VM conversions in parallel, with the remaining conversions queued. However, we recommend staging the VM conversions in smaller batches for higher efficiency.

>[!Note]
>Non-Microsoft migration options are provided by Microsoft partners. These options are available to you at an additional cost but can help reduce the VM downtime during migration. The following non-Microsoft migration options are available:<br>
>- [Commvault](https://documentation.commvault.com/11.20/converting_from_vmware_to_hyper_v.html)
>- [Zerto](https://www.zerto.com/blog/migrations-data-mobility/how-to-easily-migrate-from-vmware-to-hyper-v-with-zerto/)
>- [Veeam](https://www.veeam.com/blog/vmware-to-hyper-v-migration.html)
>- [Carbonite](https://www.carbonite.com/business/products/migration/)
>- [NAKIVO](https://www.nakivo.com/blog/how-to-convert-vmware-vm-to-hyper-v/)
:::moniker-end

## Next steps

[Manage the VM settings](vm-settings.md).
