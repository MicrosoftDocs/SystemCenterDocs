---
ms.assetid: e76baa8d-7756-44e7-b887-e622e85d8006
title: Managing Nano server as a Hyper-V host or a VM in VMM
description: This article describes how to deploy and manage Nano server-based hosts & VMs in VMM
author:  rayne-wiselman
ms.author: raynew
manager:  carmonm
ms.date:  05/10/2017
ms.topic:  article
ms.prod:  system-center-2016
ms.technology:  virtual-machine-manager
---

# Deploy and manage Nano server-based Hyper-V hosts or VMs in VMM

>Applies To: System Center 2016 - Virtual Machine Manager

You can use System Center 2016 - Virtual Machine Manager (VMM) to manage hosts and virtual machines running Nano server.

Using VMM, you can add and manage existing hosts running Nano, configure bare metal machines as Nano Server-based hosts, deploy compute clusters, and storage clusters (disaggregated and hyper-converged). You can manage Nano-based VMs, including shielded VMs.


## Before you start

- For VM deployment, you need to create the Nano Server virtual hard disk outside VMM.
- You can't create a VM template from a Nano Server VM in VMM. You can create a VM template from scratch using a Nano Server virtual hard disk.
- There are some known issues when joining a Nano Server VM to a domain. If you try to join the VM to a domain with customization details in a VM template, the domain information is ignored by VMM. The VM is deployed, but doesn't join the domain. As a workaround, deploy the VM and then join it to a domain. [Learn more](https://technet.microsoft.com/windows-server-docs/compute/nano-server/getting-started-with-nano-server). Note that joining a physical machine to a domain during bare metal deployment works fine.

## Prepare a Nano server virtual hard disk

To get started with the deployment of a Nano Server-based host or virtual machines in VMM you need to create a Nano server VHD from the Windows Server VHD. The VHD should include the VMM packages:

- Add the VMM package, **Microsoft-NanoServer-SCVMM-Package**, to ensure that the VMM agent is part of the VHD.
- Add the VMM compute package, **Microsoft-NanoServer-SCVMM-Compute-Package**, to ensure that the VHD has the Hyper-V role, and that you can manage the physical server using VMM. If you install this package, don't use the **-Compute** option for the Hyper-V role).
- For the File Server role, use **Microsoft-NanoServer-Storage-Package**, along with **Microsoft-NanoServer-SCVMM-Package**.
- For a hyperconverged deployment, use **Microsoft-NanoServer-Storage-Package**, along with **Microsoft-NanoServer-SCVMM-Package** and **Microsoft-NanoServer-SCVMM-Compute-Package**.

### Create a virtual hard disk for a physical machine

1. Copy **NanoServerImageGenerator.psm1** and **Convert-WindowsImage.ps1** from the \NanoServer folder in the Windows Server ISO, to a folder on your hard drive.
2. Start Windows PowerShell as an administrator. Navigate to the folder in which you placed the scripts.
3. Import the **NanoServerImageGenerator** script by running:

    ```
    Import-Module NanoServerImageGenerator.psm1 -Verbose
    ```

4. Create a VHD that includes the VMM packages. To do this, run the following command which will prompt you for an administrator password for the new VHD:

    ```
    New-NanoServerImage -MediaPath <path to root of media> -BasePath .\Base -TargetPath .\NanoServerVM\NanoServerVM.vhdx -ComputerName <computername> -OEMDrivers -Package Microsoft-NanoServer-SCVMM-Package,Microsoft-NanoServer-SCVMM-Compute-Package
    ```

    For example:

    ```
    New-NanoServerImage -MediaPath F:\ -BasePath .\Base -TargetPath .\Nano1\NanoServer.vhd -ComputerName Nano-srv1 -OEMDrivers –Clustering –EnableRemoteManagementPort -Packages Microsoft-NanoServer-SCVMM-Package,Microsoft-NanoServer-SCVMM-Compute-Package
    ```
    
  - This example creates a VHD from an ISO mounted as F:
  - When creating the VHD, it uses a folder called Base in the same folder in which you ran **New-NanoServerImage**
  - It places the VHD in a folder called **Nano1**, in the folder from which the command runs.
  - The computer name in this example is **Nano-srv1**. It includes the OEM drivers installed for most common hardware, and has the clustering feature enabled.
  - The VHD has remote management of the Nano server enabled, even from the systems which are not in the same subnet.
  - If the server uses UEFI to boot, you need to change the script from **NanoServer.vhd** to **NanoServer.vhdx**.

5. Log in as an administrator on the physical server on which you want to run the Nano Server VHD.
6.  Copy the VHD that the script creates to the physical computer, and configure it to boot from the new VHD, as follows:

    - Mount the generated VHD.
    - Run **bcdboot d:\windows** (in this example, it's mounted under D:)
    - Unmount the VHD.

7.  Boot the physical computer into the Nano Server virtual hard disk.
8.  Log on to the Nano server Recovery Console using the administrator name and password you supplied when running the script, and obtain the IP address of the Nano server-based host. [Learn more](https://technet.microsoft.com/library/mt126167.aspx).
8.  Ensure that the Nano server is joined to the same domain as the VMM server. [Learn more](https://technet.microsoft.com/library/mt126167.aspx).
9. Ensure that the VMM service account, and the Run As account, are added to the administrators group on the Nano server.

### Install the VMM packages offline on an existing Nano Server

If you didn't add the VMM packages when you created the Nano Server VHD, you can install them later, as follows:

1. Copy the VHD/VHDX to a location on a Windows Server 2016 machine. For example: C:\MyNano.vhd.
2. Use PowerShell to install and import the NanoServerPackage provider of the PackageManagement (OneGet) PowerShell module:

    ```
    Install-PackageProvider NanoServerPackage
    Import-PackageProvider NanoServerPackage
    ```
2. After the provider is installed, you can search and install the VMM packages (VMM agent and Hyper-V), on the VHD using these cmdlets, where **C:\MyNano.vhd** is the location of the Nano Server based VHD.

    ```
    Find-NanoServerPackage
    Install-NanoServerPackage -Name Microsoft-NanoServer-SCVMM-Package -culture en-US -ToVhd "C:\MyNano.vhd"
    Install-NanoServerPackage -Name Microsoft-NanoServer-SCVMM-Compute-Package -culture en-US -ToVhd "C:\MyNano.vhd"
    ```

### Install the VMM packages on a running Nano server host

We recommend offline installation of the VMM packages (when creating the VHD). If you do need to install them online when the Nano server is running, do the following:

1.  Copy the **Packages** folder from the local installation media to the running Nano server. For example, to C:\packages.
2.  Use remote PowerShell to log onto the Nano server.
3. Add the VMM packages using the below commands:

    - To install Microsoft-NanoServer-SCVMM-Package
    ```
    dism /online /Add-package /PackagePath:C:\packages\en-US\Microsoft-NanoServer-SCVMM-Package_en-us.cab
    ```

    > [!NOTE]
    > Make sure that the en-us (Microsoft-NanoServer-SCVMM-Package_en-us.cab) and neutral (Microsoft-NanoServer-SCVMM-Package.cab) .cab files are in the same folder so that both are installed.

    - To install Microsoft-NanoServer-SCVMM-Compute-Package:

    ```
    dism /online /Add-package /PackagePath:C:\packages\en-US\Microsoft-NanoServer-SCVMM-Compute-Package_en-us.cab
    ```


4. Check that the VMM packages, and the associated language packs, are installed correctly by running the following command:

    ```
    dism /online /get-packages
    ```

6. You should see **Package Identity : Microsoft-NanoServer-SCVMM-Feature-Package~31bf3856ad364e35~amd64~~ 10.0.14300.1003** listed twice. Once for **Release Type : Language Pack**, and once for **Release Type : Feature Pack**. The same applies for the Microsoft-NanoServer-SCVMM-Compute-Package.
7. Restart the Nano Server host.


## Add the Nano server host to the VMM fabric  

After the Nano server host is ready, add it to the VMM fabric. [Learn more](hyper-v-existing.md).

## Create a Nano server VM

To create Nano server-based VMs, you need to add few VM-specific packages to the VHD. Create the VHD for a VM as follows:

1. Copy **NanoServerImageGenerator.psm1** and **Convert-WindowsImage.ps1** from the \NanoServer folder in VMM, to a folder on your hard drive.
2. Start Windows PowerShell as an administrator, and navigate to the script folder.
3. Import the **NanoServerImageGenerator** script with **Import-Module NanoServerImageGenerator.psm1 -Verbose**.
4.  Create a VHD that includes the SCVMM packages by running the following command. You'll be prompted for an administrator password for the new VHD.

    ```
    New-NanoServerImage -MediaPath <path to root of media> -BasePath .\Base -TargetPath .\NanoServerVM\NanoServerVM.vhdx -ComputerName <computername> -GuestDrivers -Package Microsoft-NanoServer-SCVMM-Package,Microsoft-NanoServer-SCVMM-Compute-Package
    ```
Example:

    ```
    New-NanoServerImage -MediaPath F:\ -BasePath .\Base -TargetPath .\Nano1\Nano.vhd -ComputerName Nano1 -GuestDrivers -Package     Microsoft-NanoServer-SCVMM-Package,Microsoft-NanoServer-SCVMM-Compute-Package
    ```
- This example creates a VHD from an ISO mounted as F.
- When creating the VHD it will use a folder called Base in the same directory in which you ran New-NanoServerImage
- It will place the VHD in a folder called Nano1 in the folder in which the command runs.
- The computer name will be Nano1 and will install virtual machine drivers running Hyper-V.

4. If you want a Generation 1 virtual machine, generate a VHD image using a .vhd extension for -TargetPath. For a Generation 2 virtual machine, generate a VHDX image with the .vhdx extension for -TargetPath.
5. In VMM, create a new virtual machine and use the virtual hard disk you created.

## Next steps

[Provision a VM](provision-vms.md)
