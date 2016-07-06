---
title: How to Create a Class Using Inheritance in the Authoring Tool
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0999f6ac-8589-42ae-9ea6-289ff4f43002
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
# How to Create a Class Using Inheritance in the Authoring Tool
In the [!INCLUDE[smatfull2012](../../../sm/manage/author/includes/smatfull2012_md.md)], you can create a class that inherits properties and relationships from an existing base class. You can then modify or add properties and relationships to the new class.  
  
 As the first step of defining class inheritance, choose the base class from which to inherit properties and relationships. In the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)], you can choose the base class by using one of the following methods:  
  
-   Use a shortcut to inherit properties and relationships from the base configuration item class.  
  
-   Use a shortcut to inherit properties and relationships from the base work item class.  
  
-   First select the base class, and then start defining the inheritance.  
  
-   Start defining inheritance without a specific base class selection.  
  
 The following procedures describe all the methods for defining class inheritance in the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)].  
  
### To start with the configuration item class or the work item class as a base class  
  
1.  If the **Management Pack Explorer** is not visible in the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)], click **View**, and then click **Management Pack Explorer**.  
  
2.  In the **Management Pack Explorer**, select and then expand any management pack.  
  
3.  Right\-click **Classes**, and then click **Create Configuration Item Class** or **Create Work Item Class**.  
  
4.  If you are creating a class from a sealed management pack, in the **Target Management Pack** dialog box, select an unsealed management pack to store the class customization, and then click **OK**.  
  
    > [!NOTE]  
    >  If you are creating a class from an unsealed management pack, this class customization is saved in that selected management pack.  
  
5.  In the **Create Class** dialog box, specify the internal name for the new class, and then click **Create**.  
  
     In the authoring pane, you can now view the list of properties of the new class. If you are creating a configuration item class, all properties of the configuration item class are listed. If you are creating a work item class, all properties of the work item class are displayed.  
  
6.  Click **Create property** or **Create relationship** to define new properties and new relationships for the class.  
  
### To start with a selected base class  
  
1.  If the **Management Pack Explorer** is not visible in the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)], click **View**, and then click **Management Pack Explorer**.  
  
2.  In the **Management Pack Explorer**, locate and then right\-click the base class from which the new class will inherit properties and relationships. Select **Inherit from this class**.  
  
3.  In the **Inherit New Class** dialog box, enter an internal name for the class.  
  
     In the authoring pane, the **Class properties and relationship** list displays the properties of the base class.  
  
4.  You can now click **Create property** or **Create relationship** to add properties or a relationship to the new class.  
  
### To start without a selected base class  
  
1.  If the **Management Pack Explorer** is not visible in the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)], click **View**, and then click **Management Pack Explorer**.  
  
2.  In the **Management Pack Explorer**, select and then expand any management pack.  
  
3.  Right\-click **Classes**, and then click **Create other class**.  
  
4.  In the **Base class** dialog box, select the base class to inherit properties and relationships from.  
  
     Optionally, if you know in which management pack the base class that you want to use is defined, you can filter on the respective management pack, and then select the base class for this customization.  
  
     Click **OK**.  
  
5.  If the base class that you selected to inherit properties and relationships from is in a sealed management pack, in the **Target Management Pack** dialog box, select an unsealed management pack to store the class customization, and then click **OK**.  
  
     If the base class that you selected to inherit properties and relationships from is in an unsealed management pack, this class customization will be saved in that selected management pack.  
  
6.  In the **Create class** dialog box, specify the internal name for this class, and then click **Create**.  
  
     In the authoring pane, you can now view the list of properties of the new class. This list includes all the properties of the base class that you selected.  
  
## See Also  
 [Classes: Customizing and Authoring](../Topic/Classes:%20Customizing%20and%20Authoring.md)