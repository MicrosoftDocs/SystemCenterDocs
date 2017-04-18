---
title: Customize and author forms
description: Provides guidelines about how to customize and author forms with the Service Manager Authoring Tool and it describes how to accomplish common authoring tasks.
manager: carmonm
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9140312b-4d0b-4f22-a466-85887485e066
---

# Customize and author forms with the Service Manager Authoring Tool

>Applies To: System Center 2016 - Service Manager


This article provides guidelines about how to customize and author forms with the Service Manager Authoring Tool and it describes how to accomplish common authoring tasks.

Use the following guidelines when you are authoring forms in the Service Manager Authoring Tool. For more information about how Windows Presentation Foundation \(WPF\) forms work and WPF customization guidelines, see [Windows Presentation Foundation](http://go.microsoft.com/fwlink/p/?LinkID=194437) on MSDN.  

-   When you are customizing existing default forms by adding new controls, first create a new **Tab** control, and then add the new controls to the new **Tab** control.  
-   Store all customizations of a particular form in a single management pack.  
-   Group related controls in a **Panel** control so that you can better handle them as a group.  
-   You can drop controls only in containers, such as the **Panel** container control.  
-   Set one or more of the following control properties to **Auto** to allow for dynamic adjustment of placement: **Height**, **Width**, **Minimum Height**, **Minimum Width**, **Left**, **Top**, **Right**, and **Bottom**. Depending on the resulting behavior, adjust these settings.  

## Browse a form

Use one of the following procedures to browse a form in the Service Manager Authoring Tool. In both procedures, note that the properties in the **Details** pane are updated according to the class property that is bound to the selected control. And, note that the **Binding Path** entry in the **Details** pane indicates the respective property that the field in the form represents.  

### To browse a form from the Form Browser  

1.  If the **Form Browser** pane is not visible, click **View**, and then click the **Form Browser** tab.  
2.  In the **Form Browser** pane, select the management pack that contains the form that you want to view.  
3.  In the list of forms, right\-click the form that you want to view, and then click **View**. The form opens in the authoring pane.  
4.  Ensure that the **Details** pane is visible. If not, click **View** on the menu bar, and then click **Details Window**. The properties of the form appear in the **Details** pane.  
5.  Select a control on the form.  

### To browse a form from Management Pack Explorer  

1.  In the Authoring Tool, click **File**, and then click **Open**.  
2.  In the **Open a Management Pack** dialog box, select the management pack that contains the form that you want to view. For example, select **Management Packs** as the file type, and then select the **ServiceManager.ChangeManagement.Library.mp** management pack in the D:\\Program Files \(x86\)\\Microsoft System Center\\Service Manager 2016 Authoring\\Library folder.  
3.  In the **Management Pack Explorer**, select the opened management pack, and then expand **Forms**. Right\-click the form that you want to view, and then click **View form**. The form opens in the authoring pane.  
4.  Ensure that the **Details** pane is visible. If not, click **View** on the menu bar, and then click **Details Window**. The properties of the form appear in the **Details** pane.  
5.  Select a control on the form.  

## Customize a form

You can use the Service Manager Authoring Tool to customize some properties of a form. For example, you can change the layout of the form's fields, and you can add an icon to the form.  

To customize a form, you open the management pack file that contains the original form definition. After you complete the customizations, you save the changes to a management pack file. If the original form is defined in an unsealed management pack, you save your customizations to that management pack. If the original form is defined in a sealed management pack, you must save your customizations to an unsealed management pack that is already open in the Authoring Tool or to an unsealed management pack that you create.  

To use the custom form in Service Manager, import the management pack that contains the custom form into the Service Manager console. Then, when you run a task that requires that form, the custom form is displayed instead of the default form.  

Use the following procedure to customize an existing form.  

> [!IMPORTANT]  
>  You cannot perform two customizations to the same form at the same time. Additionally, the Authoring Tool option **Undo all customizations** does not fully delete information from the management pack. If you want to remove all artifacts, delete the customized form, which removes it and any associated type projection from the management pack.  

### To customize an existing form  

1.  In the Authoring Tool, click **File**, and then click **Open**.  
2.  In the **Open File** dialog box, select the management pack that contains the form that you want to customize, and then click **Open**. For example, select the Change Management Library management pack. The path might be *Authoring Tool installation drive*\\Program Files \(x86\)\\Microsoft System Center\\Service Manager 2016 Authoring\\Library\\ServiceManager.ChangeManagement.Library.mp.  
3.  Locate the form that you want to customize using the **Form Browser** or the **Management Pack Explorer**, as follows:  
     Using the **Form Browser**:  
    1.  In the **Form Browser**, select **All Management Packs** or select the management pack that contains the form that you want to customize, such as the **Service Manager Change Management Library** management pack.  
    2.  Right\-click the form that you want to customize, such as the form that ends with **ChangeRequestForm**, and then click **View**.  
    3.  In the authoring pane, click **Customize**.  
     Using the **Management Pack Explorer**:  
        1.  In the **Management Pack Explorer** pane, select the management pack that contains the form that you want to customize, such as the **Service Manager Change Management Library** management pack.  
        2.  Expand **Forms**, and then right\-click the form that you want to customize, such as the form that ends with **ChangeRequestForm**.  
        3.  Select **Customize**.  
4.  In the **Target Management Pack** dialog box, select an unsealed management pack in which to save this customization, and then click **OK**.  
    In the **Management Pack Explorer** pane, a new form item appears in the **Forms** list of the management pack that you specified as the targeted management pack. The name of the new form ends with the string **\(Customized\)**.  
5.  In the authoring pane, you can rearrange the location of controls on the form to change the appearance and behavior of the form. Also, you can add controls to the form by doing the following:  
    -   Drag controls from the **Form Customization Toolbox** pane.  
    -   Drag specific properties from the **Class Browser** pane. This will automatically create and bind the control according to the property that you dragged.  

## Create a new form

If you defined a new custom class to extend Service Manager, you might have to create a custom form to interact with that class. You can use the Service Manager Authoring Tool to create a form using either of the following methods:  

-   Start from a base class.  
-   Load a custom Windows Presentation Foundation \(WPF\) form that was initially developed by the Microsoft Visual&nbsp;Studio development system, and continue to customize that form in the Authoring Tool.  

The Authoring Tool includes form controls, such as the **Check Box**, **Date Picker**, **Tab Control**, and **Tab Item**, that you can add to the form. You can access these controls from the **Form Customizations Toolbox**. Typically, you bind the form controls to specific properties of the form's base class. Therefore, using either method you must first select a base class for the form to be associated with. For more information about the controls that you can add to a form, see previous topics in this section, such as [How to Add a Check Box Control to a Form in the Authoring Tool](add-check-box-control.md), and [How to Add a Tab Control and Tab Item Controls to a Form in the Authoring Tool](../sm/manage/author-how-to-add-a-tab-control-and-tab-item-controls-to-a-form-in-the-authoring-tool.md).  

The following sections describe how to create a new form in the Authoring Tool.  

### Create a new form from a base class  

Use the following procedure to create a simple form from a base class.  

> [!NOTE]  
>  When you create a form from a base class, the Authoring Tool does not support advanced capabilities. For example, there is no support for code\-behind, complex rules, such as field interdependency or calculated values.  

#### To create a new form from a base class  

1.  In the **Management Pack Explorer**, expand the management pack in which you want to store the new form. Right\-click **Forms**, and then click **Create**.  
2.  In the **Base class** dialog box, select the base class for the form. You can narrow your search by selecting a specific management pack, or you can leave the default **All Management Packs**. Click **OK**.  
3.  If you selected a sealed management pack in step 1, the **Target Management Pack** dialog box appears. Select an unsealed management pack in which to store the form, and then click **OK**.  
4.  In the **Create form** dialog box, in the **Internal name** box, type a name for the form, and then click **Create**.  
     An initial blank form is displayed in the authoring pane. The initial form consists of a header section at the top and a body section underneath; both sections are blank.  
5.  Customize the form by dragging controls from the **Form Customizations Toolbox** pane to the new form.  
6.  Save the management pack that contains the form that you created.  

### Create a new form that is based on a custom WPF form  
Sometimes a simple form is not sufficient, and you must use advanced features, such as custom logic, in the form. In this case, you can develop a custom WPF form by using a tool other than the Authoring Tool, using instead Visual Studio. Then, instead of authoring a form from base class, you load that WPF form's assembly file into the Authoring Tool and use that as a starting point for further customizations to the form. The form customizations that you make in the Authoring Tool are stored in a management pack file.  

Later, to use the customized form in Service Manager, after you complete all customizations, you must bundle the original form assembly file with the management pack that contains the customizations that you made in the Authoring Tool. For more information about bundling a management pack and creating a .mpb file, see [How to Bundle Management Packs and Resource Files](bundle-mps.md).  

Use the following procedure to load a custom WPF form assembly file into the Service Manager and customize that form.  

#### To create a new form that is based on a custom WPF form  

1.  In the **Management Pack Explorer**, expand the management pack in which you want to store customizations to the form. Right\-click **Forms**, and then click **Add Custom**.  
2.  In the **Base class** dialog box, select the base class for the form. You can narrow your search by selecting a specific management pack, or keep the default **All Management Packs**. Click **OK**.  
3.  If you selected a sealed management pack in step 1, the **Target Management Pack** dialog box appears. Select an unsealed management pack in which to store the form, and click **OK**.  
4.  In the **Add custom form** dialog box, type a name in the **Internal name** box. In the **Assembly** box, select the assembly file that contains the custom form that you want to load, and in the **Type** box, select the name of the form from the assembly file that you want to load. Click **Create**. The form that you selected is now displayed in the authoring pane.  
5.  Customize the form by dragging controls from the **Form Customizations Toolbox** pane to the form on the authoring pane.  
6.  Save the management pack that contains the customizations of the form.  
7.  Bundle the form's original assembly file, the management pack that contains the form customizations that you made in the Authoring Tool, and any other resource files that you need, to create an .mpb file.  

## Add a check box control to a form

A **Check Box** control in the Service Manager Authoring Tool presents an option on the form, and lets the user choose that option. You can modify the properties of the **Check Box** control to customize characteristics such as the label that is displayed on the check box.  

Use the following procedure to add a **Check Box** control to a form.  

### To add a Check Box control to a form  

1.  Ensure that the **Form Customization Toolbox** pane is open and that the form that you want to customize is open in the authoring pane.  
2.  Drag the **Check Box** icon from the **Form Customization Toolbox** pane to the form. Click the **Check Box** control on the form.  
3.  In the **Details** pane, select the **Content** property and set its value to text that will be displayed on the check box.  
4.  In the **Details** pane, select the **Binding Path** property, and then click the ellipsis \(**...**\) icon. In the **Binding Path** dialog box, expand the classes, and then select a **Boolean** property for the control to bind to. Note that the **Content** property is automatically set to the display name of the property that the control is bound to.  
5.  Click any other property, such as **Font Family**, in the **Details** pane to customize the properties of the **Check Box** control.  
6.  Click **File**, and then click **Save All** to save the custom form to a management pack.  

## Add a date picker control to a form

A **Date Picker** control in the Service Manager Authoring Tool is used for displaying dates on a form. You can modify the properties of the **Date Picker** control to customize characteristics such as the format of the date that is displayed.  

Use the following procedure to add a **Date Picker** control to a form.  

### To add a Date Picker control to a form  

1.  Ensure that the **Form Customization Toolbox** pane is open and that the form that you want to customize is open in the authoring pane.  
2.  Drag the **Date Picker** icon from the **Form Customization Toolbox** pane to the form. Click the **Date Picker** control on the form.  
3.  In the **Details** pane, select the **Binding Path** property. Click the ellipsis \(**...**\) icon, and then in the **Binding Path** dialog box, select the class property that you want the **Date Picker** control to bind to.  
4.  Click any property, such as **Date Format**, in the **Details** pane to customize the properties of the **Date Picker** control.  
5.  Click **File**, and then click **Save All** to save the custom form to a management pack.  

## Add an image control to a form

An **Image** control in the Service Manager Authoring Tool is used for displaying an image. You can modify the properties of the **Image** control to customize characteristics such as the location, size, and image that is displayed.  

Use the following procedure to add an **Image** control to a form.  

### To add an Image control to a form  

1.  Ensure that the **Form Customization Toolbox** pane is open and that the form that you want to customize is open in the authoring pane.  
2.  Drag the **Image** icon from the **Form Customization Toolbox** pane to the form.  
3.  In the **Insert Image** dialog box, specify the path of the image file for the image. Note that the image you chose appears on the form.  
4.  Click any property in the **Details** pane to customize other properties of the **Image** control.  
5.  Click **File**, and then click **Save All** to save the custom form to a management pack.  

## Add a label control to a form

A **Label** control is used in the Service Manager Authoring Tool for displaying a label on a form. You can modify the properties of the **Label** control to customize characteristics such as the text string that the label displays.  

Use the following procedure to add a **Label** control to a form.  

### To add a Label control to a form  

1.  Ensure that the **Form Customization Toolbox** pane is open and that the form that you want to customize is open in the authoring pane.  
2.  Drag the **Label** icon from the **Form Customization Toolbox** pane to the form. Click the **Label** control on the form.  
3.  In the **Details** pane, select the **Binding Path** property. Click the ellipsis \(**...**\) icon, and then in the **Binding Path** dialog box, select the class property that you want the **Label** control to bind to.  
     Alternatively, if you want the **Label** control to display a static string, select the **Content** property and type a string to replace the default Label\_1 string. It will be displayed on the form.  
4.  Click any other property in the **Details** pane to customize properties of the **Label** control.  
5.  Click **File**, and then click **Save All** to save the custom form to a management pack.  

## Add a list picker control to a form

The **List Picker** control in the Service Manager Authoring Tool is a custom control that is used for selecting an item from a prepopulated list of items. You can modify properties of the **List Picker** control to customize the characteristics of the control.  

One of the characteristics of the control that you have to set is the list of items that will populate the **List Picker** control that you are creating. You can either choose an existing list, such as the **Activity Priority** list, or you can create a new list while you are creating the control.  

To add list items to a newly created list, you must use the Service Manager console. You cannot use the Authoring Tool to add list items to a newly created list. For more information about using the Service Manager console to add list items, see [How to Add a List Item](http://go.microsoft.com/fwlink/p/?LinkId=231881).  

Use the following procedure to add a **List Picker** control to a form.  

### To add a List Picker control to a form  

1.  Ensure that the **Form Customization Toolbox** pane is open and that the form that you want to customize is open in the authoring pane.  
2.  Drag the **List Picker** icon from the **Form Customization Toolbox** pane to the form. Click the **List Picker** control on the form.  
3.  In the **Details** pane, select the **List type** property, and then click the ellipsis \(**...**\) icon. In the **Select a list** dialog box, select the list of items that will populate the **List Picker** control that you are creating. Select a list from the **Available lists** list.  
     Click **OK**.  
4.  Click any other property, such as **Width** or **Height**, in the **Details** pane to customize other properties of the **List Picker** control.  
5.  Click **File**, and then click **Save All** to save the custom form to a management pack.  

## Add a panel control to a form

The **Panel** control in the Service Manager Authoring Tool is a **Layout** control that helps you manage a group of related controls. Typically, you drag and position several controls that have a related purpose on the form on a panel control. Then, if you need to move the controls that are on the panel, instead of moving each control individually, you can simply move the **Panel** control.  

Use the following procedure to add a **Panel** control to a form.  

### To add a panel control to a form  

1.  Ensure that the **Form Customization Toolbox** pane is open and that the form that you want to customize is open in the authoring pane.  
2.  Drag the **Panel** icon from the **Form Customization Toolbox** pane to the form. You can now add other controls on the **Panel** control.  

## Add a single instance picker control to a form

A **Single Instance Picker** control in the Service Manager Authoring Tool is a custom control. It is used for presenting a list of instances of a certain class, and it lets the user select an instance from that list. This control resembles the **User Picker** control, but instead of being based on the **User** class, it is based on any class that you specify, including custom classes. You can modify properties of the **Single Instance Picker** control to customize characteristics such as the class whose instances will populate the list.  

Use the following procedure to add a **Single Instance Picker** control to a form.  

### To add a Single Instance Picker control to a form  

1.  Ensure that the **Form Customization Toolbox** pane is open and that the form that you want to customize is open in the authoring pane.  
2.  Drag the **Single Instance Picker** icon from the **Form Customization Toolbox** pane to the form. Click the **Single Instance Picker** control on the form.  
3.  In the **Details** pane, select the **Binding Path** property, and then click the ellipsis \(**...**\) icon. In the **Binding Path** dialog box, select the related class whose instances will populate the control's instances list on the form.  
4.  Click any other property, such as **Width** or **Height**, in the **Details** pane to customize other properties of the **Single Instance Picker** control.  
5.  Click **File**, and then click **Save All** to save the custom form to a management pack.  

## Add a tab control and tab item controls to a form

A **Tab Control** control, combined with **Tab Item** controls, is used for arranging visual content in tabular form in the Service Manager Authoring Tool. You can modify the properties of these controls to customize characteristics such as the appearance and layout. Typically, the **Tab Control** control is accompanied by several **Tab Item** controls that enable selection of individual items inside the **Tab Control**.  

Use the following procedures to add a **Tab Control** control and a **Tab Item** control to a form.  

### To add a Tab Control control to a form  

1.  Ensure that the **Form Customization Toolbox** pane is open and that the form that you want to customize is open in the authoring pane.  
2.  Drag the **Tab Control** icon from the **Form Customization Toolbox** pane to the form. Click the **Tab Control** control on the form.  
3.  Click any property in the **Details** pane to customize the properties of the **Tab Control** control.  
4.  Click **File**, and then click **Save All** to save the custom form to a management pack.  

### To add a Tab Item control to a form  

1.  Add a **Tab Control** control as described in the previous procedure, and then select it on the form.  
2.  Drag the **Tab Item** icon from the **Form Customization Toolbox** pane, and drop it on the **Tab Control** control that it should be associated with.  
3.  Right\-click the **Tab Item** control, and then click **Edit Content**. Enter the text that you want to appear as the label on the **Tab Item**. Click any property in the **Details** pane to customize other properties of the **Tab Item** control.  
4.  Click **File**, and then click **Save All** to save the custom form to a management pack.  

## Add a text box control to a form

A **Text Box** control is used in the Service Manager Authoring Tool for text display and editing. You can modify the properties of the control to customize characteristics such as the location, the size, the wrapping behavior, and the text of the **Text Box** control.  

Use the following procedure to add a **Text Box** control to a form.  

### To add a Text Box control to a form  

1.  Ensure that the **Form Customization Toolbox** pane is open and that the form that you want to customize is open in the authoring pane.  
2.  Drag the **Text Box** icon from the **Form Customization Toolbox** window to the form. Click the **Text Box** control on the form.  
3.  Set a text string by doing either of the following:  
    -   In the **Details** pane, select the **Binding Path** property. Click the ellipsis \(**...**\) icon, and then in the **Binding Path** dialog box, select the class property that you want the **Text Box** control to bind to.  
    -   Select the **Text** property. Select the default **Text Box** string value and replace it. Note that the new string value that you entered now appears on the form.  
4.  Select the **Accepts the ENTER key** property, and set its value to **True**. In the deployed form, this value lets users enter multiple lines of text.  
5.  Click any other property, such as **Horizontal Scroll Bar Visibility** and **Maximum Lines**, in the **Details** pane to customize other properties of the **Text Box** control.  
6.  Click **File**, and then click **Save All** to save the custom form to a management pack.  

## Add a user picker control to a form

The **User Picker** control is a Service Manager custom control that is used for choosing a user from a drop\-down list of users. You can modify the properties of the **User Picker** control in the Service Manager Authoring Tool to customize characteristics such as the layout and the list of users to bind to.  

Use the following procedure to add a **User Picker** control to a form.  

### To add a User Picker control to a form  

1.  Ensure that the **Form Customization Toolbox** pane is open and that the form that you want to customize is open in the authoring pane.  
2.  Drag the **User Picker** icon from the **Form Customization Toolbox** pane to the form. Click the **User Picker** control on the form.  
3.  In the **Details** pane, select the **Binding Path** property, and then click the ellipsis \(**...**\) icon. In the **Binding Path** dialog box, select the related user class that represents the user instances that you want this control to bind to. On the deployed form, the user can use this control to view and pick one of the user instances of the specified related user class.  
4.  Click any property in the **Details** pane to customize the properties of the **User Picker** control.  
5.  Click **File**, and then click **Save All** to save the custom form to a management pack.  
