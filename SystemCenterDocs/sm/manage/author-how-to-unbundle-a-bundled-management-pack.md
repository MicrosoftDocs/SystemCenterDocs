---
title: How to Unbundle a Bundled Management Pack
manager: cfreeman
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 2016-10-12
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 89e11c59-3f08-4f0a-8efe-b55375c2bb6c
---

# How to Unbundle a Bundled Management Pack

>Applies To: System Center 2016 - Service Manager

A bundled management pack \(.mpb\) file in System Center - Service Manager includes several management pack \(.mp\) files. In addition, it might include references to resources, such as an image or a form assembly. To customize a .mpb file, you must access and customize the individual files in the bundle.  

 In this version of the Service Manager Authoring Tool, you cannot directly open an .mpb file to access its individual files. Instead, you must manually unbundle the .mpb file and store all the .mp, .xml, and other resource files in a single folder that is accessible to the Authoring Tool. Then, you can open and customize the individual files in the Authoring Tool in the same manner that you customize other management packs. After you complete the customizations, you have to rebundle the files and generate a new .mpb management pack file.  

 You can extract most of the resource files from an .mpb file by using a Windows&nbsp;PowerShell script. The following procedures provide Windows&nbsp;PowerShell sample scripts that extract files from an .mpb file. For more information about how to use the Service Manager SDK to create other scripts, see [Service Manager SDK](http://go.microsoft.com/fwlink/p/?LinkID=198541).  

 You cannot extract sealed management packs from an .mpb file. Package owners must provide each file separately for a sealed management pack.  

### To extract individual unsealed management packs from an .mpb file  

1.  Start a Service Manager Windows&nbsp;PowerShell session.  

2.  In the Windows&nbsp;PowerShell console, type the following commands:  

    ```  
    mkdir <mpdir>  
    ```  

    ```  
    Get-SCSMManagementPack -bundlefile .\<filename>.mpb | Export-SCSMManagementPack -path <mpdir>  
    ```  

    -   In the command, replace the *mpdir* placeholder with the folder in which the extracted management pack files will be stored.  

    -   Replace the *filename* placeholder with the name of the .mpb file.  

 You can now navigate to the *mpdir* folder in the current working folder to view and access the management pack files that you extracted.  

### To extract resource files from an .mpb file  

1.  In a Windows&nbsp;PowerShell window, type the following commands:  

    ```  
    $SM2016DirKey = Get-ItemProperty "hklm:\SOFTWARE\Microsoft\System Center\2016\Common\Setup"  
    $SM2016Dir = $SM2016DirKey.InstallDirectory   
    [reflection.assembly]::loadfrom($SM2016Dir + "\SDK Binaries\Microsoft.EnterpriseManagement.Packaging.dll")  
    [reflection.assembly]::LoadWithPartialName("Microsoft.EnterpriseManagement.Core") | out-null  
    $emg = new-object Microsoft.EnterpriseManagement.EnterpriseManagementGroup localhost  
    $mpbReader = [Microsoft.EnterpriseManagement.Packaging.ManagementPackBundleFactory]::CreateBundleReader()  
    $mpb = $mpbReader.Read("$PWD\Administration.mpb", $emg)  
    ```  

 From the $mpb object, you can now access the $mpb.ManagementPacks; these are the management packs in the .mpb bundle. And, you can access the $mpb.GetStreams\(ManagementPack\),which associates the resources with a management pack in that bundle. These resources will be in the form of binary streams that you can write to files.  
