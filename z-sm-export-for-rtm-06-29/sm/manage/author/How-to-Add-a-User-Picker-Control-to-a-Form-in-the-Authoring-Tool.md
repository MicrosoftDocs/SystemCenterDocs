---
title: How to Add a User Picker Control to a Form in the Authoring Tool
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b6f8143f-04b5-4bc4-b6ab-4b44a82f0216
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
# How to Add a User Picker Control to a Form in the Authoring Tool
The **User Picker** control is a [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] custom control that is used for choosing a user from a drop\-down list of users. You can modify the properties of the **User Picker** control in the [!INCLUDE[smatfull2012](../../../sm/manage/author/includes/smatfull2012_md.md)] to customize characteristics such as the layout and the list of users to bind to.  
  
 Use the following procedure to add a **User Picker** control to a form.  
  
### To add a User Picker control to a form  
  
1.  Ensure that the **Form Customization Toolbox** pane is open and that the form that you want to customize is open in the authoring pane.  
  
2.  Drag the **User Picker** icon from the **Form Customization Toolbox** pane to the form. Click the **User Picker** control on the form.  
  
3.  In the **Details** pane, select the **Binding Path** property, and then click the ellipsis \(**…**\) icon. In the **Binding Path** dialog box, select the related user class that represents the user instances that you want this control to bind to. On the deployed form, the user can use this control to view and pick one of the user instances of the specified related user class.  
  
4.  Click any property in the **Details** pane to customize the properties of the **User Picker** control.  
  
5.  Click **File**, and then click **Save All** to save the custom form to a management pack.  
  
## See Also  
 [Forms: Customizing and Authoring](../Topic/Forms:%20Customizing%20and%20Authoring.md)