---
title: Add a check box control to a form
description: You can add a check box control to a form in the Service Manager Authoring Tool.
manager: carmonmm
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
ms.assetid: c03108fe-66f6-453d-a8b3-10cf47d6a37d
---

# Add a check box control to a form in the Authoring Tool

>Applies To: System Center 2016 - Service Manager

A **Check Box** control in the Service Manager Authoring Tool presents an option on the form, and lets the user choose that option. You can modify the properties of the **Check Box** control to customize characteristics such as the label that is displayed on the check box.  

 Use the following procedure to add a **Check Box** control to a form.  

### To add a Check Box control to a form  

1.  Ensure that the **Form Customization Toolbox** pane is open and that the form that you want to customize is open in the authoring pane.  

2.  Drag the **Check Box** icon from the **Form Customization Toolbox** pane to the form. Click the **Check Box** control on the form.  

3.  In the **Details** pane, select the **Content** property and set its value to text that will be displayed on the check box.  

4.  In the **Details** pane, select the **Binding Path** property, and then click the ellipsis \(**...**\) icon. In the **Binding Path** dialog box, expand the classes, and then select a **Boolean** property for the control to bind to. Note that the **Content** property is automatically set to the display name of the property that the control is bound to.  

5.  Click any other property, such as **Font Family**, in the **Details** pane to customize the properties of the **Check Box** control.  

6.  Click **File**, and then click **Save All** to save the custom form to a management pack.  
