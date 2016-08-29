---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  rayne-wiselman
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  How to add a Nano Server as a Hyper V host in VMM
ms.technology:  virtual-machine-manager
ms.assetid:  424a7893-2c1f-40e9-990a-4d34e0d0eeb8
---

# How to add a Nano Server as a Hyper-V host in VMM

>Applies To: System Center 2016 Technical Preview - Virtual Machine Manager

You can use Virtual Machine Manager to easily manage Nano Server-based hosts & virtual machines. 

## Preparing a Nano Server VHD for VMM from the Windows Server Technical Preview ISO

To get started with the deployment of a Nano Server-based host or virtual machines in VMM you need to create a Nano Server VHD from the Windows Server ISO.

### **How to create a Nano Server VHD for a Physical Machine** 

1. Copy NanoServerImageGenerator.psm1 and Convert-WindowsImage.ps1 from the \NanoServer folder in the Windows Server Technical Preview ISO to a folder on your hard drive.
2. Start Windows PowerShell as an administrator, change directory to the folder where you've placed these scripts and then import the NanoServerImageGenerator script with the below command:
```
Import-Module NanoServerImageGenerator.psm1 -Verbose
```
3. Create a VHD that includes the SCVMM packages by running the following command which will prompt you for an administrator password for the new VHD:


```
New-NanoServerImage -MediaPath <path to root of media> -BasePath .\Base -TargetPath .\NanoServerVM\NanoServerVM.vhdx -ComputerName <computername> -OEMDrivers -Packages Microsoft-NanoServer-SCVMM-Package,Microsoft-NanoServer-SCVMM-Compute-Package
```
**Example PowerShell script:**


```
New-NanoServerImage -MediaPath F:\ -BasePath .\Base -TargetPath .\Nano1\NanoServer.vhd -ComputerName Nano-srv1 -OEMDrivers "Clustering "EnableRemoteManagementPort -Packages Microsoft-NanoServer-SCVMM-Package,Microsoft-NanoServer-SCVMM-Compute-Package"
```
The example above creates a VHD from an ISO mounted as F:. When creating the VHD it uses a folder called Base in the same directory where you ran New-NanoServerImage; it places the VHD in a folder called Nano1 in the folder from where the command is run. The computer name in this example is Nano-srv1 and includes the OEM drivers installed for most common hardware. It also has the clustering feature enabled. The VHD has remote management of the Nano server enabled, even from the systems which are not in the same subnet. If the server uses UEFI to boot, you need to change the script from NanoServer.vhd to NanoServer.vhdx

**Note:** 
* Adding the SCVMM package, **Microsoft-NanoServer-SCVMM-Package** will ensure that the VMM agent is part of the VHD.
* Adding the SCVMM Compute package, **Microsoft-NanoServer-SCVMM-Compute-Package**, will ensure that the VHD has the Hyper-V role and you can manage the physical server using VMM. (If you install this package, do not use the -Compute option for the Hyper-V role)
* For the File Server Role, use Microsoft-NanoServer-Storage-Package along with Microsoft-NanoServer-SCVMM-Package.
* For hyper-converged mode, use the Microsoft-NanoServer-Storage-Package along with Microsoft-NanoServer-SCVMM-Package & Microsoft-NanoServer-SCVMM-Compute-Package.

4.  Log in as an administrator on the physical server where you want to run the Nano Server VHD.
5.  Copy the VHD that this script creates to the physical computer and configure it to boot from this new VHD. To do that, follow these steps:
o   Mount the generated VHD. 
o   Run **bcdboot d:\windows** (in this example, it's mounted under D:)
o   Unmount the VHD.
6.  Boot the physical computer into the Nano Server VHD.
7.  Log on to the Recovery Console (see the "Nano Server Recovery Console" section in [this article](https://technet.microsoft.com/library/mt126167.aspx)), using the administrator and password you supplied while running the script in Step 3 and obtain the IP address of the Nano Server-based host.
8.  Ensure that the Nano Server is joined to the same domain as the VMM Server (For joining a Nano Server-based host to a domain, see the section on "Joining Domains" in [this article](https://technet.microsoft.com/library/mt126167.aspx))
9. Ensure that the VMM Service account and the Run-as-account to be used are added to the administrators group on Nano server   
10. Once you have the Nano Server-based host ready, adding it to Virtual Machine Manager is exactly similar to adding a regular Windows server host. For more details, see [Adding Windows Servers as Hyper-V hosts in VMM](Adding-Windows-servers-as-Hyper-V-hosts-or-host-clusters-in-VMM.md).

### **How to create a Nano Server VHD for a Virtual Machine**
If you are planning to create Nano Server-based virtual machines, you need to add few virtual machine specific packages to the VHD. Follow the steps mentioned below to create a VHD for a virtual machine:
1.  Copy NanoServerImageGenerator.psm1 and Convert-WindowsImage.ps1 from the \NanoServer folder in the Windows Server Technical Preview ISO to a folder on your hard drive.
2.  Start Windows PowerShell as an administrator, change directory to the folder where you've placed these scripts and then import the NanoServerImageGenerator script with Import-Module NanoServerImageGenerator.psm1 -Verbose
3.  Create a VHD that includes the SCVMM packages by running the following command which will prompt you for an administrator password for the new VHD:


```
New-NanoServerImage -MediaPath <path to root of media> -BasePath .\Base -TargetPath .\NanoServerVM\NanoServerVM.vhdx -ComputerName <computername> -GuestDrivers -Packages Microsoft-NanoServer-SCVMM-Package,Microsoft-NanoServer-SCVMM-Compute-Package
```
**Example PowerShell script**

```
New-NanoServerImage -MediaPath F:\ -BasePath .\Base -TargetPath .\Nano1\Nano.vhd -ComputerName Nano1 -GuestDrivers -Packages Microsoft-NanoServer-SCVMM-Package,Microsoft-NanoServer-SCVMM-Compute-Package"
```

This example creates a VHD from an ISO mounted as F:. When creating the VHD it will use a folder called Base in the same directory where you ran New-NanoServerImage; it will place the VHD in a folder called Nano1 in the folder from where the command is run. The computer name will be Nano1 and will virtual machine drivers installed running Hyper-V. If you want a Generation 1 virtual machine, generate a VHD image by specifying a .vhd extension for -TargetPath. For a Generation 2 virtual machine, generate a VHDX image by specifying a .vhdx extension for -TargetPath. 

**Note:**

* Adding the SCVMM package, Microsoft-NanoServer-SCVMM-Package will ensure that the VMM agent is part of the VHD.
* Adding the SCVMM Compute package, Microsoft-NanoServer-SCVMM-Compute-Package, will ensure that the VHD has the Hyper-V role and you can manage the physical server using VMM. (If you install this package, do not use the -Compute option for the Hyper-V role)
* For the File Server Role, use Microsoft-NanoServer-Storage-Package along with Microsoft-NanoServer-SCVMM-Package.
* For hyper-converged mode, use the Microsoft-NanoServer-Storage-Package along with Microsoft-NanoServer-SCVMM-Package & Microsoft-NanoServer-SCVMM-Compute-Package.

4.  In Virtual Machine Manager, create a new virtual machine and use the VHD created in Step 3.

## Installing SCVMM Packages on a running Nano Server-based host

Though offline installation of the SCVMM packages (while creating the VHD) is recommended, you might need to install it online (with the Nano Server running). To do this, follow these steps:

1.  Copy the Packages folder from the installation media locally to the running Nano Server (for example, to C:\packages).
2.  Use remote Powershell to login to the Nano Server-based host. Add the SCVMM packages using the below commands:

For installing Microsoft-NanoServer-SCVMM-Package:


```
dism /online /Add-package /PackagePath:C:\packages\en-US\Microsoft-NanoServer-SCVMM-Package_en-us.cab 
dism /online /Add-package /PackagePath:C:\packages\Microsoft-NanoServer-SCVMM-Package.cab
```
For installing Microsoft-NanoServer-SCVMM-Compute-Package:


```
dism /online /Add-package /PackagePath:C:\packages\en-US\Microsoft-NanoServer-SCVMM-Compute-Package_en-us.cab
dism /online /Add-package /PackagePath:C:\packages\Microsoft-NanoServer-SCVMM-Compute-Package.cab
```
**Note:** C:\packages is the directory you copied the content of Packages to.

3.  Confirm that the SCVMM packages and the associated language packs are installed correctly by running the following command:


```
dism /online /get-packages
```
You should see "Package Identity : Microsoft-NanoServer-SCVMM-Feature-Package~31bf3856ad364e35~amd64~~ 10.0.14300.1003" listed twice, once for Release Type : Language Pack and once for Release Type : Feature Pack. Same applies for the Microsoft-NanoServer-SCVMM-Compute-Package. 

4.  Restart the Nano Server-based host.
  


