---
title: Working with Management Packs in the Service Manager Console
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6bf81515-8883-471e-b1df-62c30ad9ae9e
translation.priority.ht: 
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
# Working with Management Packs in the Service Manager Console
When you make customizations in the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)] in [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)], you save them in a management pack file. Sometimes, you have to first create a new management pack file. Later, to implement the customizations of the management pack, you import it into the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)].  
  
 When you create a management pack in the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], you provide the display name for the management pack. [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] generates a random ID that is used as the internal name for the management pack and that becomes the management pack’s file name. If you need to further customize objects in that management pack by directly modifying its XML code, it might be difficult to locate the management pack file that you want to edit. In that case, we recommend that you modify the management pack internal file name to be a meaningful name, and use it as follows:  
  
-   Edit the management pack XML file itself; change the internal management pack name to the new name.  
  
-   Rename the management pack file on the hard drive to the new name.  
  
 [!INCLUDE[crabout](../../../sm/deploy/deploy-guide/includes/crabout_md.md)] using management packs in the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], see the [Administrator's Guide for System Center 2012 \- Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209669).  
  
## See Also  
 [Management Packs: Working with Management Packs](../Topic/Management%20Packs:%20Working%20with%20Management%20Packs.md)