---
title: How to Back Up Unsealed Management Packs
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ddd02198-d3ec-4408-a41a-dfc31d6741d5
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
# How to Back Up Unsealed Management Packs
You can use the Windows PowerShell command\-line interface to identify and copy your unsealed management packs to a folder on your hard disk drive. After you copy them, save these management packs so that—as part of your disaster recovery plan for [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)]—you can later import these management packs.  
  
### To back up unsealed management packs  
  
1.  On the computer that hosts the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server, create a folder on the hard disk drive where you will store the backup copy of the management packs. For example, create the folder C:\\mpbackup.  
  
2.  On the Windows desktop, click **Start**, point to **Programs**, point to **Windows PowerShell 1.0**, right\-click **Windows PowerShell**, and then click **Run as administrator**.  
  
3.  In the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], click **Administration**.  
  
4.  In the **Tasks** pane, click **Start PowerShell Session**  
  
5.  At the Windows PowerShell command prompt, type the following command:  
  
    ```  
    Get-SCSMManagementPack | where {$_.Sealed -eq $false}|Export-SCSMManagementPack -Path c:\mpbackup  
    ```  
  
6.  Save the unsealed management packs on a separate physical computer.