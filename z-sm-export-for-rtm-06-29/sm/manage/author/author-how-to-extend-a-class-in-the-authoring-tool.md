---
title: How to Extend a Class in the Authoring Tool
ms.custom: na
ms.prod: system-center-2012-r2
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 506e0398-6fca-4f97-8f01-87f0dfb3e17f
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
# How to Extend a Class in the Authoring Tool
You can extend a class in the [!INCLUDE[smatfull2012](../../../sm/manage/author/includes/smatfull2012_md.md)] by adding properties and relationships to the definition of the class. Extending a class affects all existing instances of that class: all instances of that class will be updated to include the new properties and relationships.  
  
### To extend a class  
  
1.  If the **Management Pack Explorer** pane is not visible in the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)], click **View**, and then click **Management Pack Explorer**.  
  
2.  In the **Management Pack Explorer** pane, locate and right\-click the class that you want to extend, and then click **Extend class**.  
  
3.  In the **Target Management Pack** dialog box, select an unsealed management pack to store the class extension, and then click **OK**.  
  
4.  The **Class properties and relationship** list on the **Extension of \<class\>** tab in the authoring pane displays the properties and the relationships of the class. Create new properties and relationships as follows:  
  
    1.  Click **Create property**; in the **Create property** dialog box, type a name in **Internal name** for the new property; and then click **Create**.  
  
    2.  Click **Create relationship**; in the **Create relationship** dialog box, type a name in **Internal name** for the new relationship; and then click **Create**.  
  
    > [!NOTE]  
    >  When you are extending a class, do not define a property with an ID that is already in use in that class.  
  
5.  Locate and select the new property or relationship in the **Class properties and relationship** list, and modify its properties in the **Details** pane as needed.  
  
## See Also  
 [Classes: Customizing and Authoring](../Topic/Classes:%20Customizing%20and%20Authoring.md)