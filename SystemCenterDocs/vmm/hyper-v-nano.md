---
ms.assetid: e76baa8d-7756-44e7-b887-e622e85d8006
title: Managing Nano server as a Hyper-V host or a VM in VMM
description: This article describes how to deploy and manage Nano server-based hosts & VMs in VMM
author:  rayne-wiselman
ms.author: raynew
manager:  cfreeman
ms.date:  10/16/2016
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---

# Deploy & Manage Nano server-based Hyper-V hosts or VMs in VMM

>Applies To: System Center 2016 - Virtual Machine Manager

You can use System Center 2016 - Virtual Machine Manager (VMM) to manage hosts and virtual machines running Nano server.

- **Bare metal deployment of Nano Server-based hosts and clusters (both compute and storage)**

You can now configure bare metal machines as Nano Server-based hosts, compute clusters, and storage clusters (both dis-aggregated and hyper-converged) using VMM. This process is very similar to bare metal deployment of Full Servers except for the fact that the VHD(x) used for the operating system deployment needs to be a Nano Server-based VHD(x). Details regarding how to create a Nano Server VHD(x) can be found below in this article. For more details regarding bare-metal deployment of Nano Server-based hosts & clusters see [Provision a Hyper-V host or cluster from bare metal computers](hyper-v-bare-metal.md).

- **Management of Nano Server-based hosts and clusters (both compute and storage)**

Along with bare metal deployment, you can also add and manage existing Nano Server-based standalone hosts, compute clusters, and storage clusters (both dis-aggregated and hyper-converged) using VMM. For more details, see [Add Windows servers as Hyper-V hosts or clusters in the VMM compute fabric](hyper-v-existing.md).


## Before you start

VMM supports full lifecycle management of Nano Server-based VMs, including shielded VMs. However, note the following:

- Creation of the Nano Server VHD(X) needs to be done outside of VMM, details on how to create the VHD(X) can be found below in the 'Prepare a Nano server virtual hard disk' section of this article.
- You can't create a VM template from a Nano Server VM in VMM. As a workaround, create a VM template from scratch using a Nano Server virtual hard disk.
- There are some known issues when joining a Nano Server-based virtual machine (VM) to a domain. If you try to join the VM to a domain by specifying customization details in a VM template, the domain information is ignored by VMM. The VM is deployed, but doesn't join the domain. As a workaround, deploy the VM and then join it to a domain. [Learn more](https://technet.microsoft.com/windows-server-docs/compute/nano-server/getting-started-with-nano-server). Note that domain joining of a physical machine during bare metal deployment works fine.

## Prepare a Nano server virtual hard disk

To get started with the deployment of a Nano Server-based host or virtual machines in VMM you need to create a Nano server VHD from the Windows Server VHD. The VHD should include the VMM packages:

- Adding the VMM package, **Microsoft-NanoServer-SCVMM-Package** ensures that the VMM agent is part of the VHD.
- Adding the VMM compute package, **Microsoft-NanoServer-SCVMM-Compute-Package** ensures that the VHD has the Hyper-V role and you can manage the physical server using VMM. (If you install this package, do not use the -Compute option for the Hyper-V role)
- For the File Server role, use **Microsoft-NanoServer-Storage-Package** along with **Microsoft-NanoServer-SCVMM-Package**.
- For hyper-converged mode, use **Microsoft-NanoServer-Storage-Package** along with **Microsoft-NanoServer-SCVMM-Package** & **Microsoft-NanoServer-SCVMM-Compute-Package**.

### Create a virtual hard disk for a physical machine

1. Copy NanoServerImageGenerator.psm1 and Convert-WindowsImage.ps1 from the \NanoServer folder in the Windows Server ISO to a folder on your hard drive.
2. Start Windows PowerShell as an administrator, change directory to the folder where you've placed these scripts and then import the NanoServerImageGenerator script by running: **Import-Module NanoServerImageGenerator.psm1 -Verbose**.
3. Create a VHD that includes the VMM packages by running the following command which will prompt you for an administrator password for the new VHD: **New-NanoServerImage -MediaPath <path to root of media> -BasePath .\Base -TargetPath .\NanoServerVM\NanoServerVM.vhdx -ComputerName <computername> -OEMDrivers -Package Microsoft-NanoServer-SCVMM-Package,Microsoft-NanoServer-SCVMM-Compute-Package**
4. For example: **New-NanoServerImage -MediaPath F:\ -BasePath .\Base -TargetPath .\Nano1\NanoServer.vhd -ComputerName Nano-srv1 -OEMDrivers –Clustering –EnableRemoteManagementPort -Packages Microsoft-NanoServer-SCVMM-Package,Microsoft-NanoServer-SCVMM-Compute-Package**.

    - This example creates a VHD from an ISO mounted as F:.
    - When creating the VHD it uses a folder called Base in the same directory where you ran New-NanoServerImage; it places the VHD in a folder called Nano1 in the folder from where the command is run.
    - The computer name in this example is Nano-srv1 and includes the OEM drivers installed for most common hardware. It also has the clustering feature enabled. The VHD has remote management of the Nano server enabled, even from the systems which are not in the same subnet.
    - If the server uses UEFI to boot, you need to change the script from NanoServer.vhd to NanoServer.vhdx

5. Log in as an administrator on the physical server where you want to run the Nano Server VHD.
6.  Copy the VHD that this script creates to the physical computer and configure it to boot from this new VHD. Do this as follows:

    - Mount the generated VHD.
    - Run **bcdboot d:\windows** (in this example, it's mounted under D:)
    - Unmount the VHD.

7.  Boot the physical computer into the Nano Server VHD.
8.  Log on to the Nano server Recovery Console using the administrator and password you supplied while running the script and obtain the IP address of the Nano server-based host. [Learn more](https://technet.microsoft.com/library/mt126167.aspx).
8.  Ensure that the Nano server is joined to the same domain as the VMM server. [Learn more](https://technet.microsoft.com/library/mt126167.aspx).
9. Ensure that the VMM service account and the Run As account are added to the administrators group on the Nano server.

### Install the VMM packages offline on an existing Nano Server VHD(X)

If you forgot to add the SCVMM packages while creating the Nano Server VHD, you can install them later on the VHD by doing the following:

1. On a Windows Server 2016 machine, copy the VHD to a location (for example, C:\MyNano.vhd)
2. Use PowerShell to install and import the NanoServerPackage provider of PackageManagement (OneGet) PowerShell module:
    - **Install-PackageProvider NanoServerPackage**
    - **Import-PackageProvider NanoServerPackage**
2. Once the provider is installed, you can search and install the SCVMM packages (SCVMM Agent & Hyper-V) on the VHD using the below cmdlets:
    - **Find-NanoServerPackage**
    - **Install-NanoServerPackage -Name Microsoft-NanoServer-SCVMM-Package -culture en-US -ToVhd "C:\MyNano.vhd"**
    - **Install-NanoServerPackage -Name Microsoft-NanoServer-SCVMM-Compute-Package -culture en-US -ToVhd "C:\MyNano.vhd"**

    Note: C:\MyNano.vhd is the location of the Nano Server based VHD.

### Install the VMM packages on a running Nano server host

We recommend offline installation of the VMM packages (when creating the VHD) but if you do need to install them online when the Nano server is running, do the following:

1.  Copy the **Packages** folder from the installation media locally to the running Nano server (for example, to C:\packages).
2.  Use remote Powershell to login to the Nano server. Add the VMM packages using the below commands.
3. To install Microsoft-NanoServer-SCVMM-Package

    - **dism /online /Add-package /PackagePath:C:\packages\en-US\Microsoft-NanoServer-SCVMM-Package_en-us.cab**

    Note: Ensure that the en-us (Microsoft-NanoServer-SCVMM-Package_en-us.cab) and neutral (Microsoft-NanoServer-SCVMM-Package.cab) .cab files are in the same directory to make sure in installs both.

4. To install Microsoft-NanoServer-SCVMM-Compute-Package:

    - **dism /online /Add-package /PackagePath:C:\packages\en-US\Microsoft-NanoServer-SCVMM-Compute-Package_en-us.cab**

    Note: Ensure that the en-us (Microsoft-NanoServer-SCVMM-Compute-Package_en-us.cab) and neutral (Microsoft-NanoServer-SCVMM-Compute-Package.cab) .cab files are in the same directory to make sure in installs both.

5. Check that the VMM packages and the associated language packs are installed correctly by running the following command: **dism /online /get-packages**.
6. You should see "Package Identity : Microsoft-NanoServer-SCVMM-Feature-Package~31bf3856ad364e35~amd64~~ 10.0.14300.1003" listed twice, once for Release Type : Language Pack and once for Release Type : Feature Pack. Same applies for the Microsoft-NanoServer-SCVMM-Compute-Package.
7. Restart the Nano server-based host.



## Add the Nano server host to the VMM fabric  

After the Nano server host is ready, add it to VMM in the same way that you [add a regular Windows server](hyper-v-existing.md).

## Create a Nano server VM

If you're going to create Nano server-based VMs, you need to add few VM-specific packages to the VHD. Create the VHD for a VM as follows:

1.  Copy NanoServerImageGenerator.psm1 and Convert-WindowsImage.ps1 from the \NanoServer folder in VMM to a folder on your hard drive.
2.  Start Windows PowerShell as an administrator, and navigate to the folder where you've placed these scripts. Import the NanoServerImageGenerator script with **Import-Module NanoServerImageGenerator.psm1 -Verbose**.
3.  Create a VHD that includes the SCVMM packages by running the following command. You'll be prompted for an administrator password for the new VHD: **New-NanoServerImage -MediaPath <path to root of media> -BasePath .\Base -TargetPath .\NanoServerVM\NanoServerVM.vhdx -ComputerName <computername> -GuestDrivers -Package Microsoft-NanoServer-SCVMM-Package,Microsoft-NanoServer-SCVMM-Compute-Package**
4. For example: **New-NanoServerImage -MediaPath F:\ -BasePath .\Base -TargetPath .\Nano1\Nano.vhd -ComputerName Nano1 -GuestDrivers -Package Microsoft-NanoServer-SCVMM-Package,Microsoft-NanoServer-SCVMM-Compute-Package**. This example creates a VHD from an ISO mounted as F:. When creating the VHD it will use a folder called Base in the same directory where you ran New-NanoServerImage; it will place the VHD in a folder called Nano1 in the folder from where the command is run. The computer name will be Nano1 and will virtual machine drivers installed running Hyper-V. If you want a Generation 1 virtual machine, generate a VHD image by specifying a .vhd extension for -TargetPath. For a Generation 2 virtual machine, generate a VHDX image by specifying a .vhdx extension for -TargetPath.

Then in VMM, create a new virtual machine and use the VHD created in Step 3.
