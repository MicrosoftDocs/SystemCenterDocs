---
ms.assetid: 12c2e82d-a325-4111-9ff8-147e949ce95e
title: Enable nested virtualization in System Center VMM
description: This article explains about how to enable and use nested virtualization in VMM
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.topic: how-to
ms.service: system-center
ms.subservice: virtual-machine-manager
monikerRange: '>sc-vmm-2016'
ms.custom: UpdateFrequency2, engagement-fy24
---

# Configure a nested VM as a host




Nested virtualization allows you to run Hyper-V inside a Hyper-V virtual machine. In other words, with nested virtualization, a Hyper-V host itself can be virtualized. Nested virtualization can be enabled out-of-band using PowerShell and Hyper-V host configuration.

You can use this functionality to reduce your infrastructure expense for development and test scenarios without the need for individual hardware.


::: moniker range=">=sc-vmm-2019"

With System Center Virtual Machine Manager (VMM), you can enable and disable the nested virtualization feature through VMM console. You can configure the nested Virtual Machine (VM) as a host in VMM and perform host operations from VMM on this VM. For example, VMM dynamic optimization will consider a nested VM host for placement.

::: moniker-end

Enable the nested virtualization on a VM and then configure it as a host.

>[!NOTE]
> Virtualization applications other than Hyper-V aren't supported in Hyper-V virtual machines and are likely to fail. This includes any software that requires hardware virtualization extensions.

## Before you start

::: moniker range="sc-vmm-2025"

Ensure the following prerequisites are met:

- A Hyper-V host running Windows Server 2019/2022/2025.
- A Hyper-V VM running Windows Server 2019/2022/2025.
- A Hyper-V VM with configuration version 8.0 or greater.
- An Intel processor with VT-x and EPT technology.

::: moniker-end
::: moniker range="sc-vmm-2022"

Ensure the following prerequisites are met:

- A Hyper-V host running Windows Server 2019, Windows Server 2022.
- A Hyper-V VM running Windows Server 2019, Windows Server 2022.
- A Hyper-V VM with configuration version 8.0 or greater.
- An Intel processor with VT-x and EPT technology.

::: moniker-end

::: moniker range="sc-vmm-2019"

Ensure the following prerequisites are met:

- A Hyper-V host running Windows Server 2016, Windows Server 2019.
- A Hyper-V VM running Windows Server 2016, Windows Server 2019.
- A Hyper-V VM with configuration version 8.0 or greater.
- An Intel processor with VT-x and EPT technology.

::: moniker-end


## Enable network virtualization

Administrators/delegated administrators can configure nested virtualization using VMM. Use the following procedures:

- [Enable nested virtualization](#enable-nested-virtualization-on-an-existing-virtual-machine)
- [Configure the VM as a host in VMM](#configure-the-nested-vm-as-a-host)

### Enable nested virtualization on an existing virtual machine


1.	Identify the VM that meets the above [prerequisites](#before-you-start).
2.	Ensure the VM is in **Stopped** state.

    ![Screenshot of the stopped VM.](media/nested-vm/nested-vm-stopped-state.png)

3. Right-click the VM to browse its **Properties**.

    ![Screenshot of the vm properties.](media/nested-vm/nested-vm-properties.png)
4. On **General**, select **Enable Nested Virtualization**.

    ![Screenshot of enable nested virtualization.](media/nested-vm/nested-virtualization-enable.png)

## Configure the nested VM as a host
1.	Enable the following inbound and outbound firewall rules on the nested VM that you want to configure as the host.

    **Inbound Firewall rules**

    - File and printer sharing
    - Windows remote management (HTTP-In)
    - Windows management instrumentation

    **Outbound Firewall rules**
    - File and printer sharing
    - Windows management instrumentation (WMI-Out)

2. Ensure the VM is in **Running** state. Start the VM if it isn't running.

    ![Screenshot of host vm running.](media/nested-vm/nested-vm-running-state.png)

3. Right-click the VM and select **Configure as a Host**. The **Add Resource** wizard appears.

    ![Screenshot of configure vm as a host.](media/nested-vm/nested-vm-configure-as-host.png)

    ![Screenshot of add resource wizard.](media/nested-vm/nested-vm-add-resource1.png)

4. Run through the wizard, select the appropriate options, and complete the wizard.

## Disable nested virtualization

1.	Select the host or VM for which nested virtualization is enabled.
2.	Ensure the VM is in **Stopped** state. Stop the VM if it's running.
3.	Right-click the VM to browse its **Properties**.
4.	On **General**, clear the **Enable Nested Virtualization** check box.

    >[!NOTE]
    > Check the note at the bottom of the wizard page before you disable nested virtualization.

::: moniker range="sc-vmm-2019"


## Nested virtualization in 2019 ur1

With VMM 2019 UR1, in addition to enabling nested virtualization on an existing VM, you can also enable nested virtualization while creating new VMs through VM templates, service templates, or through VM creation wizard on VMM console.

- [Enable nested virtualization through VM templates](#enable-nested-virtualization-through-vm-templates)

- [Enable nested virtualization through *Create Virtual Machines wizard*](#enable-nested-virtualization-through-create-virtual-machines-wizard)

- [Enable nested virtualization through service templates](#enable-nested-virtualization-through-service-template)

### Enable nested virtualization through VM templates
You can enable nested virtualization on VMs that are created through a VM template.

>[!NOTE]
> Ensure the VMs that will be created using these templates meet the above [prerequisites](#before-you-start).

To enable nested virtualization, on the **Create VM Template Wizard**, select **Select Source**, and select **Enable Nested Virtualization** on the right pane of the wizard.

![Screenshot of the enable nested virtualization through VM template.](media/nested-vm/enable-nested-virtualizaton-vm-template.png)

### Enable nested virtualization through create virtual machines wizard

You can enable nested virtualization on VMs that are created through Create Virtual Machine wizard.

>[!NOTE]
> Ensure the VMs that will be created using this wizard meet the above [prerequisites](#before-you-start).

To enable nested virtualization, on the **Create Virtual Machines wizard**, select  **Select Source**, and select **Enable Nested Virtualization** on the right pane of the wizard.

![Screenshot of enable nested virtualization through Create Virtual Machine wizard.](media/nested-vm/enable-nested-virtualization-vm-wizard.png)

### Enable nested virtualization through service template
You can enable nested virtualization on VMs that are created through service templates.

>[!NOTE]
> Ensure the VMs that will be created using this template meet the above [prerequisites](#before-you-start).

To enable nested virtualization,  from  **Single Tier Properties**, select  **General**, and select **Enable Nested Virtualization** on the right pane of the wizard.

![Screenshot of enable nested virtualization through Create VM Service template wizard.](media/nested-vm/enable-nested-virtualization-vm-service-template.png)

::: moniker-end

## Next steps
[Run Hyper-V in a nested VM](/virtualization/hyper-v-on-windows/user-guide/nested-virtualization).
