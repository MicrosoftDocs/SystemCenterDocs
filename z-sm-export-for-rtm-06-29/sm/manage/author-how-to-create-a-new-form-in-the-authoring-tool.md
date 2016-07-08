---
title: How to Create a New Form in the Authoring Tool
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5a021f84-ad51-4a29-9ed8-200a79000110


















---
# How to Create a New Form in the Authoring Tool
If you defined a new custom class to extend System Center 2012 - Service Manager, you might have to create a custom form to interact with that class. You can use the System Center 2016 - Service Manager Authoring Tool to create a form using either of the following methods:  
  
-   Start from a base class.  
  
-   Load a custom Windows Presentation Foundation \(WPF\) form that was initially developed by the Microsoft Visual Studio development system, and continue to customize that form in the Authoring Tool.  
  
 The Authoring Tool includes form controls, such as the **Check Box**, **Date Picker**, **Tab Control**, and **Tab Item**, that you can add to the form. You can access these controls from the **Form Customizations Toolbox**. Typically, you bind the form controls to specific properties of the form’s base class. Therefore, using either method you must first select a base class for the form to be associated with. For more information about the controls that you can add to a form, see previous topics in this section, such as [How to Add a Check Box Control to a Form in the Authoring Tool](../../../sm/manage/author/How-to-Add-a-Check-Box-Control-to-a-Form-in-the-Authoring-Tool.md), and [How to Add a Tab Control and Tab Item Controls to a Form in the Authoring Tool](../../../sm/manage/author/How-to-Add-a-Tab-Control-and-Tab-Item-Controls-to-a-Form-in-the-Authoring-Tool.md).  
  
 The following sections describe how to create a new form in the Authoring Tool.  
  
## Creating a New Form from a Base Class  
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
  
## Creating a New Form That Is Based on a Custom WPF Form  
 Sometimes a simple form is not sufficient, and you must use advanced features, such as custom logic, in the form. In this case, you can develop a custom WPF form by using a tool other than the Authoring Tool, using instead Visual Studio. Then, instead of authoring a form from base class, you load that WPF form’s assembly file into the Authoring Tool and use that as a starting point for further customizations to the form. The form customizations that you make in the Authoring Tool are stored in a management pack file.  
  
 Later, to use the customized form in Service Manager, after you complete all customizations, you must bundle the original form assembly file with the management pack that contains the customizations that you made in the Authoring Tool. For more information about bundling a management pack and creating a .mpb file, see [How to Bundle Management Packs and Resource Files](../../../sm/manage/author/How-to-Bundle-Management-Packs-and-Resource-Files.md).  
  
 Use the following procedure to load a custom WPF form assembly file into the Service Manager and customize that form.  
  
#### To create a new form that is based on a custom WPF form  
  
1.  In the **Management Pack Explorer**, expand the management pack in which you want to store customizations to the form. Right\-click **Forms**, and then click **Add Custom**.  
  
2.  In the **Base class** dialog box, select the base class for the form. You can narrow your search by selecting a specific management pack, or keep the default **All Management Packs**. Click **OK**.  
  
3.  If you selected a sealed management pack in step 1, the **Target Management Pack** dialog box appears. Select an unsealed management pack in which to store the form, and click **OK**.  
  
4.  In the **Add custom form** dialog box, type a name in the **Internal name** box. In the **Assembly** box, select the assembly file that contains the custom form that you want to load, and in the **Type** box, select the name of the form from the assembly file that you want to load. Click **Create**. The form that you selected is now displayed in the authoring pane.  
  
5.  Customize the form by dragging controls from the **Form Customizations Toolbox** pane to the form on the authoring pane.  
  
6.  Save the management pack that contains the customizations of the form.  
  
7.  Bundle the form’s original assembly file, the management pack that contains the form customizations that you made in the Authoring Tool, and any other resource files that you need, to create an .mpb file.  
  
## See Also  
 [Forms: Customizing and Authoring](../Topic/Forms:%20Customizing%20and%20Authoring.md)
