---
title: How to Bundle Management Packs and Resource Files
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c9cb6eaf-d744-4f91-b1d4-3294812953df
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
# How to Bundle Management Packs and Resource Files
A custom management pack might include references to resources, such as an image or a form assembly. To import such a management pack into [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)], you must first bundle the management pack file and its associated resources into a single .mpb management pack file.  
  
 In [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)], to bundle a management pack file with its resources, use the Windows PowerShell cmdlet **New\-SCSMManagementPackBundle**. [!INCLUDE[crabout](../../../sm/deploy/deploy-guide/includes/crabout_md.md)] this cmdlet, see [New\-SCSMManagementPackBundle](http://go.microsoft.com/fwlink/p/?LinkID=225397).  
  
 When you bundle a management pack, any form .dll in the bundle is stored in the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database, along with any other resources, such as images. The form is then automatically deployed to any [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)] computer that needs to render that form. When the form is loaded for the first time in the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], it is retrieved from the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database and cached on the local computer. In subsequent uses, the form is retrieved from the local cache.  
  
 To customize management packs that are bundled in an .mpb file, you must first unbundle the .mpb file and then individually customize each management pack and resource file. [!INCLUDE[crabout](../../../sm/deploy/deploy-guide/includes/crabout_md.md)] how to unbundle an .mpb management pack file, see [How to Unbundle a Bundled Management Pack](../../../sm/manage/author/How-to-Unbundle-a-Bundled-Management-Pack.md).  
  
## See Also  
 [Management Packs: Working with Management Packs](../Topic/Management%20Packs:%20Working%20with%20Management%20Packs.md)