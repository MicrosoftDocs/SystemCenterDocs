---
title: Forms: Key Concepts
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 79a37387-ed4a-48ea-b006-d73b6867f7db
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
# Forms: Key Concepts
Before customizing forms, you should be familiar with the following form concepts.  
  
## How Forms Are Used  
 When the management pack that contains the form definitions is imported into [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)], the form definitions are stored in the database. Later, when the user initiates a [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)] task that requires the display of an object, [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] must find a form to display the requested object. [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] accesses the database and searches for a form that has been defined for that object. If no form is defined for the object, [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] searches for a form that is defined for the object’s parent object. [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] continues to search the entire object’s inheritance hierarchy until it finds a defined form.  
  
## Generic Forms  
 If [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] cannot find any form for the object or for any of its parent objects, [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] dynamically builds a default *generic form* for that object. The generic form is a system\-generated form that is sufficient for simple form use. The generic form represents a quick and easy way to create a form for objects without any form definitions.  
  
 By default, the generic form displays all the properties of the form in a simple layout that you cannot change. The generic form displays the properties of all the parent objects in the inheritance hierarchy of the form, and you cannot change that behavior. Customizations to the generic form are limited. For example, you can specify the properties that you want the generic form to display; however, the generic form cannot be used as a basis for customization. If you later define a custom form for that object, your custom form overwrites the object’s generic form.  
  
 For information about hiding properties in a generic form and other ways that you can customize a generic form, see the blog post [Overview of the Forms Infrastructure and the Generic Form](http://go.microsoft.com/fwlink/p/?LinkID=208536).  
  
## Combination Classes in Forms  
 Sometimes, you need a form to display information that is derived from more than one class. To do this, you create a *combination class* and then bind a field on the form to the combination class. [!INCLUDE[crabout](../../../sm/deploy/deploy-guide/includes/crabout_md.md)] combination classes, see [Changes to the System Center Common Schema](../../../sm/manage/author/Changes-to-the-System-Center-Common-Schema.md).  
  
## Functional Aspects of a Form  
 A form has the following functional aspects:  
  
1.  Initialization  
  
2.  Size and location  
  
3.  Refresh  
  
4.  Submit changes  
  
 These aspects are described in the following sections.  
  
### Initialization  
 During initialization, a form’s Extensible Application Markup Language \(XAML\) is parsed and all controls on the form are instantiated and loaded. The form’s **Loaded** event indicates when the form and all contained elements have been loaded. Data\-loading operations are asynchronous. Therefore, the target instance may not be available when the **Loaded** event is raised. Instead, the **DataContextChanged** event must be used for notification when the target instance is set for the form. The **PropertyChanged** event for the **DataContext** property can be used in place of the **DataContextChanged** event.  
  
 We recommend that you use the **Loaded** event for control\-related custom initialization and then use the **DataContextChanged** or **PropertyChanged** events on the **DataContext** property for target instance\-related custom initialization.  
  
### Size and Location  
 When a form is displayed in a pop\-up window, its initial size is determined based on the form’s **Width**, **Height**, **MinWidth**, and **MinHeight** properties. If these properties are not set for the form, the form’s initial size is calculated based on its content.  
  
 We recommend that you set these properties as follows:  
  
-   Set the **Width** and **Height** properties of the form to explicitly specify the ideal size. Consider setting these properties to the **Auto** value. This sets the width and height of the form based on the size of the content.  
  
-   Set the **MinWidth** and **MinHeight** properties of the form to specify the smallest window acceptable for the form. If a user resizes the window to a smaller size than specified, scrollbars appear for scrolling to the hidden form content.  
  
 When the form is hosted inside the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] forms host, the last\-used size and location is preserved for subsequent display of that form by the same user within the same run session.  
  
### Refresh  
 The target instance of a form can change as a result of executing a **Refresh** command on the form. The handler for this command fetches new data from the database. When the data arrives, the form’s **DataContext** property value is set to the new target instance and the **DataContextChanged** event is raised.  
  
 To differentiate between the **DataContextChanged** event that was raised when the form was first loaded and the event that was raised to handle a **Refresh** command, check the **OldValue** property of the event arguments that are passed in with the event. This property is null if the form has just been initialized.  
  
### Submit Changes  
 The form host pop\-up window in [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] provides buttons for submitting changes that are made in the form and for closing the pop\-up window.  
  
 When a user clicks the **Apply** button for a form, the form’s target instance is submitted for storage. This operation is synchronous; therefore, the user cannot edit the form until the submission operation is complete. If failure occurs during the form submission, an error message appears. The form remains open for further changes. We recommend that users apply their changes frequently to avoid collisions if another instance of the form is being edited at the same time.  
  
 If the user clicks the **OK** button, the behavior is similar to **Apply**, except that, if the form submission operation is successful, the form and its host window are closed.  
  
 If the user clicks the **Cancel** button, a dialog box appears that asks the user to confirm the operation. The user can click **Yes** and lose changes, or click **No** and return to the form.  
  
## See Also  
 [Forms: Customizing and Authoring](../Topic/Forms:%20Customizing%20and%20Authoring.md)