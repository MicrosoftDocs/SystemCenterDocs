---
title: How to Add a Single Instance Picker Control to a Form in the Authoring Tool
manager: cfreeman
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 2016-10-12
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b415bdf0-413c-4516-be09-748bc1ac4281
---

# How to Add a Single Instance Picker Control to a Form in the Authoring Tool

>Applies To: System Center 2016 - Service Manager

A **Single Instance Picker** control in the Service Manager Authoring Tool is a custom control. It is used for presenting a list of instances of a certain class, and it lets the user select an instance from that list. This control resembles the **User Picker** control, but instead of being based on the **User** class, it is based on any class that you specify, including custom classes. You can modify properties of the **Single Instance Picker** control to customize characteristics such as the class whose instances will populate the list.  

 Use the following procedure to add a **Single Instance Picker** control to a form.  

### To add a Single Instance Picker control to a form  

1.  Ensure that the **Form Customization Toolbox** pane is open and that the form that you want to customize is open in the authoring pane.  

2.  Drag the **Single Instance Picker** icon from the **Form Customization Toolbox** pane to the form. Click the **Single Instance Picker** control on the form.  

3.  In the **Details** pane, select the **Binding Path** property, and then click the ellipsis \(**...**\) icon. In the **Binding Path** dialog box, select the related class whose instances will populate the control's instances list on the form.  

4.  Click any other property, such as **Width** or **Height**, in the **Details** pane to customize other properties of the **Single Instance Picker** control.  

5.  Click **File**, and then click **Save All** to save the custom form to a management pack.  
