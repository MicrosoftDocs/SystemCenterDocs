---
title: Install an operating system on a VM in the System Center VMM fabric
description: This article describes how to install an operating system on a VM in the VMM fabric
author: jyothisuri
ms.author: jsuri
ms.date: 08/30/2024
ms.topic: install-set-up-deploy
ms.service: system-center
ms.subservice: virtual-machine-manager
ms.custom: intro-installation, UpdateFrequency2, engagement-fy24
---


# Install an operating system on a VM in the VMM fabric



This article describes how to install an operating system on a VM in the System Center Virtual Machine Manager (VMM) fabric.

After you've deployed a VM in the VMM fabric, you can install an operating system on it. Review the [supported operating systems](./system-requirements.md#vms-in-the-vmm-fabric).

You can install an operating system from a DVD, from an ISO image file in the VMM library, or from a network installation.

- For the system CD or ISO image, when you [set up the VM](vm-blank-disk.md), you need a virtual drive to attach to the physical drive or image file.
- To use an ISO image, it must be added to the VMM library.
- For a network installation, you configure a virtual network adapter.

## Prepare to install from a system DVD

1. In **Virtual Machines**, right-click the VM > **Properties**.
2. In **Hardware Configuration**, select **DVD** on the **New** toolbar to add a virtual DVD drive to the IDE bus.
3. Select **Physical CD/DVD drive** and select the drive on the host.

## Prepare to install from an ISO in the VMM library

1. Copy the image file to a share in the Virtual Machine Manager library. The file will be available when the library refreshes. [Learn more](library-files.md) about adding file-based resources to the library.
2. In the VM properties > **Hardware Configuration**, select **DVD** on the **New** toolbar to add a virtual DVD drive to the IDE bus.
3. Select **Known image file**, and select the file from the library resources in the list.


## Enable shared ISOs

By default, when you create a VM, an ISO attached as a virtual DVD drive is copied into the VM folder. VMM does this so that you can easily migrate VMs from host to host. If you want to share the image from the VMM library, instead of copying it, you can do that as follows:

1. Specify an Active Directory domain account as the VMM service account on the VMM server.
2. Grant the VMM service account read access on the VMM library share that stores the ISO image files. Grant the Hyper-V host machine account read access for the shared ISO location.
3. Configure constrained delegation for each Hyper-V host. This ensures that each host presents delegated credentials for CIFS/SMB to the VMM server on which the library stores the ISO. To do this, in Active Directory, locate the host machine account and open the account properties. In the **Delegation** tab, select **Select this computer for delegation to specified services only** > **Use any authentication protocol** > **Add**. Add the VMM library server that contains the ISO you want to share. In **Add Services**, add **cifs**.
4. Now configure a virtual machine to share an ISO image.<br>
     a. In the VM properties > **Hardware Configuration**, in **Capture** mode > select **Existing image file** and browse to select the ISO image file in the library.<br>
     b. Select **Share image file instead of copying it**.


> [!NOTE]
> You must attach the shared ISO image file to the VM after you've created it. You cannot attach the file when you create the VM.

## Prepare to install from the network

If the network adapter on the host computer supports network service boots, you can configure a virtual network adapter on the VM to enable this.

1. In **Virtual Machines**, right-click the VM > **Properties**.
2. In **Hardware Configuration**, configure a network connection.
3. On the **New** toolbar, select **Network Adapter** to add a virtual network adapter to the IDE bus.
4. In **Connect to**, select the external virtual network to use for the network service boot. The list contains all virtual networks that are configured on the host.
5. Under **Ethernet (MAC) address**, specify a dynamic or static IP address for the VM.
6. With the VM configured to provide access to the installation medium of choice, you can connect to the virtual machine to install the operating system. By default, VMM uses port 5900 to connect to VMRC. No configuration is required unless a firewall is blocking the port.

## Install the operating system on the virtual machine

1. Right-click the VM > **Connect to virtual machine**. Select **Yes** to start the VM.
2. On the **Remote Control** menu, select **Special Keys** and then select **Send Ctrl+Alt+Delete**.
3. Install the operating system on the VM. The boot disk partition must be the Windows partition.
4. After completing the installation, end your session with the VM and stop the VM in VMM.


## Next steps

[Manage the VM settings](./vm-settings.md).
