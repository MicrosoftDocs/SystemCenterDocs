---
ms.assetid: 24a4c010-ed26-4176-8d27-99180010945a
title: Import gallery items in SPF
description: Provides information about importing gallery items into SPF
author: rayne-wiselman
ms.author: raynew
manager: cfreeman
ms.date: 10/16/2016
ms.topic: article
ms.prod: system-center-threshold
ms.technology: service-provider-foundation
---

# Import gallery items in SPF

>Apples To: System Center 2016

 Gallery items are virtual machine roles that serve as standard and reusable artifacts. These items can be used by hosting service providers, to provide offerings to their tenants. In Windows Azure Pack, you can add a gallery item to a tenant subscription plan. Virtual machine roles represent a scalable tier of virtual machines that can be provisioned by a tenant using a single process. Examples of workloads that can be created by virtual machine roles could include a single virtual machine, an Active Directory Domain Controller, a SQL Server cluster, or Internet Information Services \(IIS\) web farm.  [Learn more](http://social.technet.microsoft.com/wiki/contents/articles/20194.downloading-and-installing-windows-azure-pack-gallery-resource.aspx) about gallery resources.

In System Center 2026- Service Provider Foundation (SPF), you can import gallery items into System Center 2016 - Virtual Machine Manager (VMM) from downloaded resource packages. The gallery items are tracked in the SPFDB database. Gallery items will then be immediately available for viewing in the management portal, by Windows Azure Pack administrators.

SPF provides the following cmdlets for the gallery:  

-   Get\-SCSPFVMRoleGalleryItem  

-   Get\-SCSPFVMRoleGalleryItemIcon  

-   Get\-SCSPFVMRoleGalleryItemPackage  

-   Import\-SCSpfVMRoleGalleryItem  

-   Remove\-SCSPFVMRoleGalleryItem  

-   Set\-SCSPFVMRoleGalleryItem  


## Obtain a gallery resource

You can use the SPF Admin web service or cmdlets to get a gallery package, item, or the icon for an item. Portal developers can create UI elements and functionality, to offer tenants a compelling experience in selecting gallery items.  

The following example shows how to use PowerShell to import a gallery item from a package and use its contents, and then remove it.  

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
