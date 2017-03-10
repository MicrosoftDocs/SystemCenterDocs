---
title: Add a user picker control to a form
description: You can add a user picker control to a form in the Service Manager Authoring Tool.
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
ms.assetid: b6f8143f-04b5-4bc4-b6ab-4b44a82f0216
---

# Add a user picker control to a form in the Authoring Tool

>Applies To: System Center 2016 - Service Manager

The **User Picker** control is a Service Manager custom control that is used for choosing a user from a drop\-down list of users. You can modify the properties of the **User Picker** control in the Service Manager Authoring Tool to customize characteristics such as the layout and the list of users to bind to.  

 Use the following procedure to add a **User Picker** control to a form.  

### To add a User Picker control to a form  

1.  Ensure that the **Form Customization Toolbox** pane is open and that the form that you want to customize is open in the authoring pane.  

2.  Drag the **User Picker** icon from the **Form Customization Toolbox** pane to the form. Click the **User Picker** control on the form.  

3.  In the **Details** pane, select the **Binding Path** property, and then click the ellipsis \(**...**\) icon. In the **Binding Path** dialog box, select the related user class that represents the user instances that you want this control to bind to. On the deployed form, the user can use this control to view and pick one of the user instances of the specified related user class.  

4.  Click any property in the **Details** pane to customize the properties of the **User Picker** control.  

5.  Click **File**, and then click **Save All** to save the custom form to a management pack.  
