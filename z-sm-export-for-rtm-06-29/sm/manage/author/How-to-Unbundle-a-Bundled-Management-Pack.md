---
title: How to Unbundle a Bundled Management Pack
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 89e11c59-3f08-4f0a-8efe-b55375c2bb6c
translation.priority.mt: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# How to Unbundle a Bundled Management Pack
A bundled management pack \(.mpb\) file in [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] includes several management pack \(.mp\) files. In addition, it might include references to resources, such as an image or a form assembly. To customize a .mpb file, you must access and customize the individual files in the bundle.  
  
 In this version of the [!INCLUDE[smatfull2012](../../../sm/manage/author/includes/smatfull2012_md.md)], you cannot directly open an .mpb file to access its individual files. Instead, you must manually unbundle the .mpb file and store all the .mp, .xml, and other resource files in a single folder that is accessible to the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)]. Then, you can open and customize the individual files in the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)] in the same manner that you customize other management packs. After you complete the customizations, you have to rebundle the files and generate a new .mpb management pack file.  
  
 You can extract most of the resource files from an .mpb file by using a Windows PowerShell script. The following procedures provide Windows PowerShell sample scripts that extract files from an .mpb file. [!INCLUDE[crabout](../../../sm/deploy/deploy-guide/includes/crabout_md.md)] how to use the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] SDK to create other scripts, see [Service Manager SDK](http://go.microsoft.com/fwlink/p/?LinkID=198541).  
  
 You cannot extract sealed management packs from an .mpb file. Package owners must provide each file separately for a sealed management pack.  
  
### To extract individual unsealed management packs from an .mpb file  
  
1.  Start a [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] Windows PowerShell session. [!INCLUDE[crdefault](../../../sm/manage/author/includes/crdefault_md.md)][Configuring and Using the System Center 2012 \- Service Manager Cmdlets for Windows PowerShell](http://go.microsoft.com/fwlink/p/?LinkId=233745).  
  
2.  In the Windows PowerShell console, type the following commands:  
  
    ```  
    mkdir <mpdir>  
    ```  
  
    ```  
    Get-SCSMManagementPack -bundlefile .\<filename>.mpb | Export-SCSMManagementPack -path <mpdir>  
    ```  
  
    -   In the command, replace the *\<mpdir\>* placeholder with the folder in which the extracted management pack files will be stored.  
  
    -   Replace the *\<filename\>* placeholder with the name of the .mpb file.  
  
 You can now navigate to the *\<mpdir\>* folder in the current working folder to view and access the management pack files that you extracted.  
  
### To extract resource files from an .mpb file  
  
1.  In a Windows PowerShell window, type the following commands:  
  
    ```  
    $SM2012DirKey = Get-ItemProperty "hklm:\SOFTWARE\Microsoft\System Center\2012\Common\Setup"  
    $SM2012Dir = $SM2012DirKey.InstallDirectory   
    [reflection.assembly]::loadfrom($SM2012Dir + "\SDK Binaries\Microsoft.EnterpriseManagement.Packaging.dll")  
    [reflection.assembly]::LoadWithPartialName("Microsoft.EnterpriseManagement.Core") | out-null  
    $emg = new-object Microsoft.EnterpriseManagement.EnterpriseManagementGroup localhost  
    $mpbReader = [Microsoft.EnterpriseManagement.Packaging.ManagementPackBundleFactory]::CreateBundleReader()  
    $mpb = $mpbReader.Read("$PWD\Administration.mpb", $emg)  
    ```  
  
 From the $mpb object, you can now access the $mpb.ManagementPacks; these are the management packs in the .mpb bundle. And, you can access the $mpb.GetStreams\(ManagementPack\),which associates the resources with a management pack in that bundle. These resources will be in the form of binary streams that you can write to files.  
  
## See Also  
 [Management Packs: Working with Management Packs](../Topic/Management%20Packs:%20Working%20with%20Management%20Packs.md)