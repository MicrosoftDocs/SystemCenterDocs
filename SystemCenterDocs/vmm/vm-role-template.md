---
ms.assetid:  e2581377-1e74-49c1-b02f-1fd245ccd478
title:  Create VM templates using VMM 2016 and Windows Azure Pack
description: This article describes how to create VM role templates that can be used by tenants
author:  rayne-wiselman
ms.author: raynew
manager:  carmonm
ms.date:  05/07/2016
ms.topic:  article
ms.prod:  system-center-threshold
ms.technology:  virtual-machine-manager
---

# Create VM templates using VMM and Windows Azure Pack

>Applies To: System Center 2016 - Virtual Machine Manager

As a hosting provider, you can use System Center 2016 - Virtual Machine Manager (VMM) in combination with Windows Azure Pack to increase the features that you offer to tenants. To help tenants create virtual machines with specific operating systems and applications already installed, you can create VM role templates. Tenants can use these templates to create VMs on-premises, and in service-provider hosting environments.

## Before you begin

- Learn about [Windows Azure Pack](https://technet.microsoft.com/library/dn296435.aspx)
- Learn about how VMM manages resources in the [VMM library](manage-library-server.md)

## Download Azure Pack Gallery resources

Azure Pack Gallery Resources provide tenant offerings using standard and reusable components. The VM role gallery enables you to deploy VMs. Usually you need two packages to deploy a VM role:

    - A resource definition package (\*\.resdefpkg) to deploy the VM. This template describes information asked to self-portal tenants about VM size, name etc. These parameters are used by VMM to deploy the role.
    - A resource extension package (\*\.resextpkg) to install apps on a VM.

Each resource contains a Readme file that explains how to prepare your environment.

1. Download the [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx). You use this to download the gallery resources.
2. Start the installer, click the **Options** link at the bottom, and type the link http://www.microsoft.com/web/webpi/partners/servicemodels.xml into **Custom Feeds**. Click **Add Feed** > **OK**. A **Service Models** tab should appear.
3. In the **Service Models** tab, select **Gallery Resources**.
4. Select the resource you want, and click **Add** > **Install**.
5. Accept the license terms if appropriate, and then click **Continue**. A window will be opened for the folder on the local computer where the resource is downloaded.
6. The Readme file that accompanies the resource will specify whether additional software is needed. Follow the instructions as needed.

## Import resource extensions to the library

For gallery resources that use Resource Extensions, you need to import the extensions into the VMM library, using PowerShell. This example shows you how to install a Resource Extension Pack (MyVMRole.resextpkg), with a library shared named MSSCVMMLibrary,

1. At the command line, run the following:

``` $libraryShare = Get-SCLibraryShare | Where-Object {$_.Name -eq 'MSSCVMMLibrary'}
$resextpkg = $Env:SystemDrive + "\GalleryResources\My-VMRole-Pkg\MyVMRole.resextpkg"
Import-CloudResourceExtension –ResourceExtensionPath $resextpkg -SharePath $libraryShare -AllowUnencryptedTransfer
```
2. Verify that the import completed with the following cmdlet:

``` Get-CloudResourceExtension
```

## Create and prepare a virtual hard disk

To create a template, you need a virtual hard disk file that contains an operating system that's been prepared for deployment, using Sysprep.

### Specify the operating system

1. When you create the hard disk, specify the required operating system in the Operating System property. For data disks this value must be set to None.
2. Set the property using the VMM console, or PowerShell. The following example shows how to set the virtual hard disk MyVirtualHardDisk to run Windows Server 2012 Datacenter. Your cmdlet with replace the disk name with one of the values in the Readme file.

``` $myVHD = Get-SCVirtualHardDisk | where {$_.Name –eq 'MyVirtualHardDisk.vhd'}
$WS2012Datacenter = Get-SCOperatingSystem | where { $_.name –eq '64-bit edition of Windows Server 2012 Datacenter' }
Set-scvirtualharddisk –virtualharddisk $myVHD –OperatingSystem $WS2012Datacenter
```

### Specify the name and release

1. The Familyname and Release properties of the virtual hard disk must be set in order for the Windows Azure Pack portal to display the virtual hard disk as an available disk for this Gallery Resource. These values are shown in the portal drop-down list.

    - The Familyname property values should indicate the contents of the virtual hard disk, including the Windows Server release and edition. The Readme file of the Gallery Resource should include appropriate Familyname values.
    - Release property values must conform to the Windows Azure versioning scheme of n.n.n.n. Examples include 1.0.0.0 and 1.0.0.1.
2. Set the property using the VMM console, or PowerShell. The following example shows how to set the virtual hard disk MyVirtualHardDisk to a Familyname "Windows Server 2012 Datacenter", and the Release property to "1.0.0.0". Your cmdlet with replace values with one of the values in the Readme file.

``` $myVHD = Get-SCVirtualHardDisk | where {$_.Name –eq 'MyVirtualHardDisk.vhd'}
$familyName = "Windows Server 2012 DataCenter"
$release = "1.0.0.0"
Set-scvirtualharddisk –virtualharddisk $myVHD –FamilyName $familyName –Release $release
```

### Specify tags

Virtual Machine Role gallery items specify tags that must be included on an operating system disk for it to be available as an option when a user provisions the virtual machine. The Readme file of the gallery resource should include the tags that it requires.

1. When you create the hard disk, specify the required tags using PowerShell.
2. The following example shows how to set the tag "WindowsServer2012R1" for the virtual hard disk MyVirtualHardDisk. Your cmdlet use the values in the Readme file.

``` $myVHD = Get-SCVirtualHardDisk | where {$_.Name –eq 'MyVirtualHardDisk.vhd'}
$tags = $myVHD.Tag
if ( $tags -cnotcontains "WindowsServer2012R1" ) { $tags += @("WindowsServer2012R1") }
Set-scvirtualharddisk –virtualharddisk $myVHD –Tag $tags
```
## Add the virtual disk to the library

After you create the virtual hard disk, you must add it to the VMM library with the values you specified. [Learn more](library-files) about adding file-based resources to the library.

## Import the Resource Definition packages

After the Resource Extension and virtual hard disk are in the VMM lbirary, you can import the Resource Definition package, and publish the gallery item using the Service Administrator Portal in Windows Azure Pack. After these steps, the gallery item will be available to the tenant.

- The Gallery Resource will include one or more Resource Definition Package files.
- If it includes more than one, then the ReadMe file will specify the different configuration that each one will provide.

1. Open the Service Admin Portal.
2. Navigate to the **VM Clouds** workspace.
3. Click the **Gallery** tab > **Import**.
4. Select and import the Resource Definition Package file for the gallery item. This will be the file with the extension resdefpkg.

The gallery item should now be listed on the Gallery tab.

## Publish the item and add to a plan

1. On the **Gallery** tab, select the version of the gallery item that you just imported.
2. Click the arrow next to the gallery item name. Verify the details of the gallery item. Navigate back, and click **Make Public**.
3. Select the **Plans** workspace, and select the plan to which you want to add the gallery item.
4. Select the **Virtual Machine Clouds** service. Scroll to the **Gallery** section, and click **Add Gallery Items**.
5 Select the gallery items that you imported, and then click **Save**

The Virtual Machine Role is now available to the tenant as part of the selected plan.


## Next steps

Learn about [provisioning VMs](manage-vm-overview.md).
