---
title: Guidelines and Best Practices for Authoring Forms in the Authoring Tool
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9140312b-4d0b-4f22-a466-85887485e066
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
# Guidelines and Best Practices for Authoring Forms in the Authoring Tool
Use the following guidelines when you are authoring forms in the [!INCLUDE[smatfull2012](../../../sm/manage/author/includes/smatfull2012_md.md)]. [!INCLUDE[crabout](../../../sm/deploy/deploy-guide/includes/crabout_md.md)] how Windows Presentation Foundation \(WPF\) forms work and WPF customization guidelines, see [Windows Presentation Foundation](http://go.microsoft.com/fwlink/p/?LinkID=194437) on MSDN.  
  
-   When you are customizing existing default forms by adding new controls, first create a new **Tab** control, and then add the new controls to the new **Tab** control.  
  
-   Store all customizations of a particular form in a single management pack.  
  
-   Group related controls in a **Panel** control so that you can better handle them as a group.  
  
-   You can drop controls only in containers, such as the **Panel** container control.  
  
-   Set one or more of the following control properties to **Auto** to allow for dynamic adjustment of placement: **Height**, **Width**, **Minimum Height**, **Minimum Width**, **Left**, **Top**, **Right**, and **Bottom**. Depending on the resulting behavior, adjust these settings.  
  
## See Also  
 [Forms: Customizing and Authoring](../Topic/Forms:%20Customizing%20and%20Authoring.md)