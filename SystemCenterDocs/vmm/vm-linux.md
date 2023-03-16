---
ms.assetid: de18e064-a779-47e0-93b6-710dd80e1420
title: Create and deploy Linux virtual machines in the VMM fabric
description: This article describes how to create and deploy Linux VMs in the VMM fabric
author: jyothisuri
ms.author: jsuri
manager: mkluck
ms.date: 05/06/2022
ms.topic: article
ms.prod: system-center
ms.technology: virtual-machine-manager
ms.custom: UpdateFrequency2
---


# Create and deploy Linux virtual machines in the VMM fabric

::: moniker range=">= sc-vmm-1801 <= sc-vmm-1807"

[!INCLUDE [eos-notes-virtual-machine-manager.md](../includes/eos-notes-virtual-machine-manager.md)]

::: moniker-end


This article describes how to create and deploy Linux VMs in the System Center - Virtual Machine Manager (VMM) fabric.

## Before you start

VMM supports virtual machines that contain Linux as the guest operating system. Ensure that:

- Linux Integration Services (LIS) must be installed on the virtual machine.
- The VMM guest agent for Linux must be installed on the virtual machine. It's required for service template integration, and it allows you to modify properties on the Linux computer, such as the host name.

    > [!NOTE]
    > SCVMMLinuxGuestAgent (XPlat) cfghostdomain garbles the hosts file if hostname is already set to localhost. We recommend you not to set the hostname as localhost when deploying Linux VMs through VMM.

- VMM doesn't verify that the VM meets these requirements. However, if it doesn't, VM deployment will fail.


## Create the VM

Create a VM running Linux using any of the available methods in the VMM fabric. [Learn more](provision-vms.md).

## Install LIS on the VM

By default, LIS is included with some distributions of Linux. If LIS isn't included in the distribution of Linux that you're using for the virtual machine, then install it manually. [Learn more](/windows-server/virtualization/hyper-v/Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows).

## Install the VMM guest agent

1. Open an elevated command prompt on the VMM server.

::: moniker range="sc-vmm-2016"
2. Go to the **c:\Program Files\Microsoft System Center 2016\Virtual Machine Manager\agents\Linux** folder.
::: moniker-end

::: moniker range=">sc-vmm-2016"
2. Go to the **c:\Program Files\Microsoft System Center\Virtual Machine Manager\agents\Linux** folder.
::: moniker-end

3. Copy all the agent installation files from that folder to a new folder on the VM.
4. Open the new folder on the VM, and run the following command: **chmod +x install**.
5. Run either of these commands, depending on the operating system.

     ```powershell
    ./install scvmmguestagent.1.0.0.544.x64.tar
    ```

     ```powershell
    ./install scvmmguestagent.1.0.0.544.x86.tar
    ```
When the agent installs on the VM, the following files and folders will be created on the VHD:

- A default installation folder (/opt/microsoft/scvmmguestagent), and an installation log file (scvmm-install.log)
- A default log files folder - /var/opt/microsoft/scvmmagent/log
- A specialization log file (scvmm.log). This file is created when the virtual machine is deployed and specialized.
- A configuration file (scvmm.conf). This file contains the location of the log file and is used to control logging during deployment and specialization.

## Next steps

Learn more about how to [Configure virtual machine settings in the VMM compute fabric](vm-settings.md).
