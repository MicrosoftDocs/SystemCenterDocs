---
title: How to Add a Text Box Control to a Form in the Authoring Tool
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c1fe66a-d9ca-4957-bb76-d5fd7fbcf083
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
# How to Add a Text Box Control to a Form in the Authoring Tool
A **Text Box** control is used in the [!INCLUDE[smatfull2012](../../../sm/manage/author/includes/smatfull2012_md.md)] for text display and editing. You can modify the properties of the control to customize characteristics such as the location, the size, the wrapping behavior, and the text of the **Text Box** control.  
  
 Use the following procedure to add a **Text Box** control to a form.  
  
### To add a Text Box control to a form  
  
1.  Ensure that the **Form Customization Toolbox** pane is open and that the form that you want to customize is open in the authoring pane.  
  
2.  Drag the **Text Box** icon from the **Form Customization Toolbox** window to the form. Click the **Text Box** control on the form.  
  
3.  Set a text string by doing either of the following:  
  
    -   In the **Details** pane, select the **Binding Path** property. Click the ellipsis \(**…**\) icon, and then in the **Binding Path** dialog box, select the class property that you want the **Text Box** control to bind to.  
  
    -   Select the **Text** property. Select the default **Text Box** string value and replace it. Note that the new string value that you entered now appears on the form.  
  
4.  Select the **Accepts the ENTER key** property, and set its value to **True**. In the deployed form, this value lets users enter multiple lines of text.  
  
5.  Click any other property, such as **Horizontal Scroll Bar Visibility** and **Maximum Lines**, in the **Details** pane to customize other properties of the **Text Box** control.  
  
6.  Click **File**, and then click **Save All** to save the custom form to a management pack.  
  
## See Also  
 [Forms: Customizing and Authoring](../Topic/Forms:%20Customizing%20and%20Authoring.md)