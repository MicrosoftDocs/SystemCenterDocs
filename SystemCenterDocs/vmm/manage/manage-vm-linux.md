---
title: Create and deploy Linux virtual machines in the VMM fabric
description: This article describes how to create and deploy Linux VMs in the VMM fabric
author:  rayne-wiselman
manager:  cfreemanwa
ms.date:  2016-09-13
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---


# Create and deploy Linux virtual machines in the VMM fabric

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager


This article describes how to create and deploy Linux VMs in the System Center 2016 - Virtual Machine Manager (VMM) fabric.

## Before you start

VMM supports virtual machines that contain Linux as the guest operating system. Note that:

- Linux Integration Services (LIS) must be installed on the virtual machine.
- The VMM guest agent for Linux must be installed on the virtual machine. It is required for service template integration, and it allows you to modify properties on the Linux computer such as the host name.
- VMM doesn't verify that the VM meets these requirements. However, if it doesn't, VM deployment will fail.


## Create the VM

Create a VM running Linux using any of the available methods in the VMM fabric. [Learn more](manage-vm-overview.md)

## Install LIS on the VM

By default, LIS is included with some distributions of Linux. If LIS is not included in the distribution of Linux that you are using for the virtual machine, then install it manually. [Learn more](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows).

## Install the VMM guest agent

1. Open an elevated command prompt on the VMM server.
2. Go to the **c:\Program Files\Microsoft System Center 2012\Virtual Machine Manager\agents\Linux** folder.
3. Copy all the agent installation files from that folder to a new folder on the VM.
4. Open the new folder on the VM, and run the following command: **chmod +x install**.
5. Run either of these commands, depending on the operating system.

    ```
    ./install scvmmguestagent.1.0.0.544.x64.tar
    ./install scvmmguestagent.1.0.0.544.x86.tar
    ```

When the agent installs on the VM the following files nad folders will be created on the VHD:

- A default installation folder (/opt/microsoft/scvmmguestagent), and an installation log file (scvmm-install.log)
- A default log files folder - /var/opt/microsoft/scvmmagent/log
- A specialization log file (scvmm.log). This file is created when the virtual machine is deployed and specialized.
- A configuration file (scvmm.conf). This file contains the location of the log file and is used to control logging during deployment and specialization.

## Next steps

[Manage VM settings](manage-vm-settings.md)
