---
ms.assetid: 28a3bb81-979c-4ebe-aa07-7ba7ecfb6efc
title: Convert a VMware VM to Hyper-V in the VMM fabric
description: This article describes how to convert VMware VMs in VMM fabric to Hyper-V
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 09/24/2024
ms.topic: article
ms.service: system-center
ms.subservice: virtual-machine-manager
---


# Convert a VMware VM to Hyper-V in the VMM fabric

This article describes how to convert VMware VMs in the System Center Virtual Machine Manager (VMM) fabric to Hyper-V.

VMM offers a simple wizard-based experience for V2V (Virtual to Virtual) conversion. You can use the [sample PowerShell script](vm-convert-vmware.md#convert-using-powershell-cmdlet) provided in this article to migrate workloads at scale from VMware infrastructure to Hyper-V infrastructure.

>[!Important]
>- Review the [system requirements](./system-requirements.md) for the supported vCenter/ESXi servers.
>- Review the [list of ports](./plan-ports-protocols.md) required for ESXi and Hyper-V hosts and vCenter server.
>- Review [this article](./manage-vmware-hosts.md) about managing vCenter servers, ESXi hosts and VMware VMs in SCVMM.
>- You can't convert VMware workstations.
>- You can't convert VMs with virtual hard disks connected to an IDE bus.
>- VMware tools must be uninstalled from the guest operating system of the VM.
>- *Add a point on the unsupported case with VMware VMs with vSAN storage*
>- Online conversions aren't supported through SCVMM.
>- We recommend upgrading to VMM 2025 to convert your VMware VMs to Hyper-V four times faster.

## Start by bringing your vCenter server and the source ESXi hosts under SCVMM management

1.	Create **Run as account** for vCenter Server Administrator role in VMM. These administrator credentials are used to manage vCenter server and ESXi hosts.

    :::image type="content" source="media/vm-convert-vmware/create-run-as-account.png" alt-text="Screenshot of create run as account page." lightbox="media/vm-convert-vmware/create-run-as-account.png":::
 
2.	In the VMM console, under **Fabric**, select **Servers > Add VMware vCenter Server**.

    :::image type="content" source="media/vm-convert-vmware/add-vmware-vcenter-server.png" alt-text="Screenshot of add vmware vcenter server option." lightbox="media/vm-convert-vmware/add-vmware-vcenter-server.png":::

3.	In the **Add VMware vCenter Server** page, do the following:<br>
  a. **Computer name**: Specify the vCenter server name.<br>
  b. **Run As account**: Select the Run As account created for vSphere administrator.<br>

      :::image type="content" source="media/vm-convert-vmware/specify-vcenter-server.png" alt-text="Screenshot of specify vcenter server page." lightbox="media/vm-convert-vmware/specify-vcenter-server.png":::

4.	Select **Finish**.

5.	In the **Import Certificate** page, select **Import**.

    :::image type="content" source="media/vm-convert-vmware/import-certificate.png" alt-text="Screenshot of import certificate page." lightbox="media/vm-convert-vmware/import-certificate.png":::
 
6.	After the successful addition of the vCenter server, all the ESXi hosts under the vCenter are discovered in VMM.

7.	In the VMM console, under **Fabric**, select **Servers > Add VMware ESX Hosts and Clusters**.

    :::image type="content" source="media/vm-convert-vmware/add-vmware-esx-hosts-and-clusters.png" alt-text="Screenshot of add vmware ESX hosts and clusters page." lightbox="media/vm-convert-vmware/add-vmware-esx-hosts-and-clusters.png":::

8.	In the **Add Resource Wizard**,<br>
    a. Under **Credentials**, select the Run as account that is used for the port and select **Next**.<br>

    :::image type="content" source="media/vm-convert-vmware/add-resource-wizard.png" alt-text="Screenshot of add resource wizard page." lightbox="media/vm-convert-vmware/add-resource-wizard.png":::

    b.	Under **Target Resources**, select all the ESX clusters that need to be added to VMM and select **Next**.

    :::image type="content" source="media/vm-convert-vmware/select-esx-computers.png" alt-text="Screenshot of select ESX computers page." lightbox="media/vm-convert-vmware/select-esx-computers.png":::

    c.	Under **Host Settings**, select the location where you want to add the VMs and select **Next**.

      :::image type="content" source="media/vm-convert-vmware/add-virtual-machine-path.png" alt-text="Screenshot of add virtual machine path page." lightbox="media/vm-convert-vmware/add-virtual-machine-path.png":::

    d.	Under **Summary**, review the settings and select **Finish**. Along with the hosts, associated VMs will also get added.
 
    :::image type="content" source="media/vm-convert-vmware/confirm-settings.png" alt-text="Screenshot of confirm settings page." lightbox="media/vm-convert-vmware/confirm-settings.png":::

## Convert your VMware VMs to Hyper-V

Now that your VMware VMs are discovered and manageable by VMM, you can convert these VMs to Hyper-V by following these instructions:

>[!Note]
> As part of converting your VMware to Hyper-V, you can modernize your BIOS-based VMware VMs to Generation 2 Hyper-V VMs by following [these instructions](vm-convert-vmware.md#convert-a-vmware-vm-to-hyper-v-in-the-vmm-fabric) as a pre-step before starting the conversion.

1.	Select **VMs and Services > Home > Create > Create Virtual Machines > Convert Virtual Machine**.

    *Add Image*

2.	In **Convert Virtual Machine** wizard > **Select Source**, select **Browse** and in **Select Virtual Machine Source**, select the VMware VM you want to convert.

    *Add Image*

3.	In **Specify Virtual Machine Identity**, modify the machine name and description as required.

    *Add Image*

4.	In **Virtual Machine Configuration**, specify the number of processors and memory settings. You can migrate BIOS-based VMware VMs to Generation 1 Hyper-V VMs and UEFI-based VMware VMs to Generation 2 Hyper-V VMs.

    *Add Image*

5.	In **Select Host**, select a Hyper-V host/Azure Stack HCI for placement. In **Select Path**, configure the storage location on the host for the VM files. The default VM path is listed.

    *Add Image*

6.	In **Select Networks**, select the logical network, virtual network, and the VLAN as applicable.

    *Add Image*

    >[!Note]
    >The PowerShell script-based approach provides guidance to retain the IP of the VM after conversion. You can also read about it in Cameron Peppers’ blogpost here.

7.	In **Add Properties**, configure the required settings. In **Summary**, review the settings, and select **Start the virtual machine after deploying it** if necessary.

    *Add Image*

8.	Select **Create** to start the conversion. Verify the VM's conversion in **VMs and Services > Home > Show > VMs**.

    *Add Image*

    >[!Note]
    >After conversion, all VM disks except for the OS disk will be offline. This is because the NewDiskPolicy parameter is set to offlineALL on VMware VMs by default. To override this and to have the new disks brought online after conversion, you can make one of the following changes to your VMware VM disk policy before initiating the conversion:<br>
    >- `Set-StorageSetting -NewDiskPolicy OfflineShared`: To have all the new shared bus disks offline and all the new local bus disks online
    >- `Set-StorageSetting -NewDiskPolicy OnlineAll`: To have all the new disks online, regardless of whether the disks are on a local or shared bus.

## Convert using PowerShell cmdlet

Here is the PowerShell cmdlet for V2V conversion via SCVMM with all the parameters:

```powershell

New-SCV2V -VMHost <Host> -VMXPath <string> [-EnableVMNetworkOptimization <bool>] [-EnableMACAddressSpoofing <bool>] [-VMMServer <ServerConnection>] [-LibraryServer <LibraryServer>] [-JobGroup <guid>] [-Trigger] [-VhdType {UnknownType | DynamicallyExpanding | FixedSize}] [-VhdFormat {VHD | VHDX}] [-Description <string>] [-Name <string>] [-Owner <string>] [-UserRole <UserRole>] [-Path <string>] [-StartVM] [-CPUCount <byte>] [-CPURelativeWeight <int>] [-CPUType <ProcessorType>] [-MemoryMB <int>] [-Generation <int>] [-DelayStartSeconds <int>] [-StartAction {NeverAutoTurnOnVM | AlwaysAutoTurnOnVM | TurnOnVMIfRunningWhenVSStopped}] [-StopAction {SaveVM | TurnOffVM | ShutdownGuestOS}] [-LogicalNetwork <LogicalNetwork>] [-VMNetwork <VMNetwork>] [-NoConnection] [-MACAddress <string>] [-MACAddressType <string>] [-SourceNetworkConnectionID <string>] [-VirtualNetwork <VirtualNetwork>] [-VirtualNetworkAdapter <VirtualNetworkAdapter>] [-VLanEnabled <bool>] [-VLanID <uint16>] [-OverridePatchPath <string>] [-SkipInstallVirtualizationGuestServices] [-NetworkLocation <string>] [-NetworkTag <string>] [-RunAsynchronously] [-PROTipID <guid>] [-JobVariable <string>] [<CommonParameters>]

```

## Convert your VMware VMs to Hyper-V at-scale using PowerShell scripts

>[!Note]
> We recommend that no more than ten conversions be triggered parallelly from the same ESXi source to the same Hyper-V destination. If the source-destination pair is different, VMM can support up to 100 VM conversions in parallel, with the remaining conversions queued. However, we recommend staging the VM conversions in smaller batches for higher efficiency.

PowerShell script-based conversion allows you to automate your conversion process and perform at-scale conversions. PowerShell commands also allow you to provide the disk type for the target Hyper-V VM, which will enable the VMware thick provisioned disk to be migrated as Hyper-V dynamic disk, based on the requirements. Here is a sample PowerShell script to convert five VMs - VM1, VM2, VM3, VM4, VM5:

*Sample script with appropriate values*

>[!Note]
>Third-party migration options are provided by Microsoft partners. These options are available to you at an additional cost but may help in reducing the VM downtime during migration. The following third-party migration options are available:<br>
>- [Commvault](https://documentation.commvault.com/11.20/converting_from_vmware_to_hyper_v.html)
>- [Zerto](https://www.zerto.com/blog/migrations-data-mobility/how-to-easily-migrate-from-vmware-to-hyper-v-with-zerto/)
>- [Veeam](https://www.veeam.com/blog/vmware-to-hyper-v-migration.html)
>- [Carbonite](https://www.carbonite.com/business/products/migration/)

## Next steps

[Manage the VM settings](vm-settings.md).
