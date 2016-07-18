---
title: How to Customize a Form in the Authoring Tool
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 07f4da17-8077-4fdb-8ed1-2972126e7da0


















---
# How to Customize a Form in the Authoring Tool
You can use the System Center 2016 - Service Manager Authoring Tool to customize some properties of a form. For example, you can change the layout of the form’s fields, and you can add an icon to the form.  
  
 To customize a form, you open the management pack file that contains the original form definition. After you complete the customizations, you save the changes to a management pack file. If the original form is defined in an unsealed management pack, you save your customizations to that management pack. If the original form is defined in a sealed management pack, you must save your customizations to an unsealed management pack that is already open in the Authoring Tool or to an unsealed management pack that you create.  
  
 To use the custom form in Service Manager, import the management pack that contains the custom form into the Service Manager console. Then, when you run a task that requires that form, the custom form is displayed instead of the default form.  
  
 Use the following procedure to customize an existing form.  
  
> [!IMPORTANT]  
>  You cannot perform two customizations to the same form at the same time. Additionally, the Authoring Tool option **Undo all customizations** does not fully delete information from the management pack. If you want to remove all artifacts, delete the customized form, which removes it and any associated type projection from the management pack.  
  
### To customize an existing form  
  
1.  In the Authoring Tool, click **File**, and then click **Open**.  
  
2.  In the **Open File** dialog box, select the management pack that contains the form that you want to customize, and then click **Open**. For example, select the Change Management Library management pack. The path might be *Authoring Tool installation drive*\\Program Files \(x86\)\\Microsoft System Center\\Service Manager 2012 Authoring\\Library\\ServiceManager.ChangeManagement.Library.mp.  
  
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
  
## See Also  
 [Forms: Customizing and Authoring](../Topic/Forms:%20Customizing%20and%20Authoring.md)
