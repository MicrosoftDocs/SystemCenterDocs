---
title: Importing Gallery Items in Service Provider Foundation
description: This topic describes how to add items to the gallery you offer to tenants through your portal if you are pulling items from a VM Cloud in Virtual Machine Manager.  
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: service-provider-foundation
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4acda26b-e58f-4b48-9cce-4286743bf72c
author: bwren
manager: cfreeman
ms.author: raynew
ms.date: 10/12/2016
---

# Importing Gallery Items in Service Provider Foundation
>Apples To: System Center 2016

This topic pertains to using the **VM Clouds** gallery in Windows Azure Pack for Windows Server. Gallery items are virtual machine roles that serve as standard and reusable artifacts that hosting service providers can use to provide offerings to their tenants. In Windows Azure Pack, you can add a gallery item to a plan that is subscribed to by tenants. Virtual machine roles represent a scalable tier of virtual machines that can be provisioned by a tenant using a single process. Examples of workloads that can be created by virtual machine roles could include a single virtual machine, an Active Directory Domain Controller, a SQL Server cluster, or Internet Information Services \(IIS\) web farm.  

For information about obtaining gallery resources, see the [Downloading and Installing Windows Azure Pack Gallery Resource](http://social.technet.microsoft.com/wiki/contents/articles/20194.downloading-and-installing-windows-azure-pack-gallery-resource.aspx).  

Service Provider Foundation allows you to import gallery items into System Center 2016 Virtual Machine Manager from downloaded resource packages. In addition, the gallery items are tracked in the SPFDB database. By doing so, the gallery items will be immediately available for viewing in management portal for administrators in Windows Azure Pack.  

You can also use Service Provider Foundation Admin web service or cmdlets to get a gallery package, item, or the icon for an item. This allows portal developers to create UI elements and functionality that offer tenants a compelling experience in selecting gallery items.  

The following example shows how to use Windows PowerShell to import a gallery item from a package and use its contents, and then remove it.  

```powershell  
PS C:\> # The first command gets the path to the resource package and stores it in the $Path variable.   
PS C:\> # The second command gets a System.IO.FileStream object of the package.   
PS C:\> # The third command imports the package.  
PS C:\> $Path = "c:\packages\create.resdefpkg"  
PS C:\> $FStream = New-Object IO.FileStream $Path, Open  
PS C:\> Import-SCSPFVMRoleGalleryItem -Package $FStream  
PS C:\>  
PS C:\> # Get an item from the gallery by specifying its name and store it in the $galItem variable.  
PS C:\> $galItem = Get-ScSpfVmRoleGalleryItem -Name 570569955cbfb62b374358b34467020750f65c  
PS C:\>   
PS C:\> # Get the icon object by specifying the required parameters with the variable.   
PS C:\> # The IconFileName parameter is explicitly specified in case the variable has a null value for the icon file name.  
PS C:\> $galItemIcon = Get-SCSPFVMRoleGalleryItemIcon -Name $galItem.Name -Publisher $galItem.Publisher -Version $galItem.Version -IconFilename "contoso.ico"  
PS C:\>  
PS C:\> # Get the package of the gallery and stores it in the $galPkg variable. This cmdlets returns an System.IO.MemoryStream object.  
PS C:\> $galPkg = Get-SCSPFVMRoleGalleryItemPackage -Name 570569955cbfb62b374358b34467020750f65c -Publisher Microsoft -Version 1.0.0.0  
PS C:\>   
PS C:\> # One use of the memory stream of the package is to save it to a file on your computer.  
PS C:\> $fs = New-Object IO.Filestream "c:\@tmp\gal.bin", Create  
PS C:\> $binwriter = New-Object IO.BinaryWriter $fs  
PS C:\> $binwriter.Write($galPkg.ContentStream.ToArray())  
PS C:\> $fs.Close()  
PS C:\> $binwriter.Close()  
PS C:\>  
PS C:\> # Import the package that was just saved, using the PackageFilePath parameter.  
PS C:\> Import-ScSpfVmRoleGalleryItem -PackageFilePath "C:\@tmp\gal.bin"  

```  

Service Provider Foundation provides the following cmdlets for the gallery:  

-   Get\-SCSPFVMRoleGalleryItem  

-   Get\-SCSPFVMRoleGalleryItemIcon  

-   Get\-SCSPFVMRoleGalleryItemPackage  

-   Import\-SCSpfVMRoleGalleryItem  

-   Remove\-SCSPFVMRoleGalleryItem  

-   Set\-SCSPFVMRoleGalleryItem  

## See Also  
[Portals in Service Provider Foundation](../Get-Started/Portals-in-Service-Provider-Foundation.md)  
[Get Started with Virtual Machine Roles: Walkthrough Guide](http://technet.microsoft.com/library/dn296459.aspx)  
[System Center 2016 Virtual Machine Role Authoring Guide \- Resource Definition Package](http://social.technet.microsoft.com/wiki/contents/articles/18273.system-center-2016-virtual-machine-role-authoring-guide-resource-definition-package.aspx)  
[Using gallery items in Virtual Machine Clouds](http://technet.microsoft.com/en-us/library/dn457794.aspx)  
