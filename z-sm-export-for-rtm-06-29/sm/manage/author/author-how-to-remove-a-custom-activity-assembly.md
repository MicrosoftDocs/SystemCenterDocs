---
title: How to Remove a Custom Activity Assembly
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e24dfa62-62ca-4a65-b7c0-f2eda6b281fb
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
# How to Remove a Custom Activity Assembly
To remove a custom activity assembly, you must have administrative permissions on the computer running the [!INCLUDE[smatfull2012](../../../sm/manage/author/includes/smatfull2012_md.md)] and on the computer running the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)]. After the custom activity assembly has been removed, the activities compiled into that assembly are no longer available in personalized activity groups.  
  
### To remove a custom activity assembly  
  
1.  On the computer running the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)], browse to the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)] Workflow Activity Library folder, for example, D:\\Program Files \(x86\)\\Microsoft System Center\\Service Manager 2012 Authoring\\Workflow Activity Library. Remove the custom activity assembly from this folder.  
  
2.  On the computer running the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], browse to the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] installation folder. Remove the custom activity assembly from this folder.  
  
3.  After you have removed the custom activity assembly, notify the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)] users that the custom activities are no longer available.  
  
## See Also  
 [Modifying the Default Toolbox](../../../sm/manage/author/Modifying-the-Default-Toolbox.md)