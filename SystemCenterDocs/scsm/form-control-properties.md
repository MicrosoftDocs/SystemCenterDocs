---
title: Form control properties
description: Provides a reference for form control properties in the Service Manager Authoring Tool.
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
ms.assetid: 7d62ce9b-fd6d-4521-932d-f2ede5920955
---

# Form control properties in the Service Manager Authoring Tool

>Applies To: System Center 2016 - Service Manager

The table in this topic lists the properties of Service Manager form controls. This information can help you customize and create forms in the Service Manager Authoring Tool.  

 Most properties of Service Manager forms are based on Windows Presentation Foundation (WPF) properties, and other properties are defined by Service Manager. The following table provides details about the WPF-based property groups and their respective properties, when they are applicable. For more information about WPF properties, see [System.Windows.Controls Namespace](http://go.microsoft.com/fwlink/p/?LinkID=204425) on MSDN.  

**Group** | **Name** | **Source** | **WPF** | **Details**
--- | --- | --- | --- | ---
**Appearance** | Opacity | WPF | UIElement/Opacity |
 | Visibility | WPF | UIElement/Visibility |  
**Binding** | Binding Mode | WPF | Binding/Mode |
 | Binding Path | Service Manager/WPF | Binding/Path | Binds the control dynamically to the its displayed property.<br/><br/> The value it updated as it changes.<br/><br/> The control and displayed property types must match. Example: the **Binding Path** property type of a **Date Picker** control must be **Date**.
 |Binds directly to source | WPF | Binding/BindsDirectlyToSource |   
**Date** | Date Format | Service Manager | N/A | The date format. Example:"Full date and time", "Short".
**Drawing** | Source Path |Service Manager | N/A | Image file path in an **Image** control.|  
 | Stretch | WPF | Image/Stretch |   
 | Stretch Direction | WPF | Viewbox/StretchDirection |   
**Brush** | Background Brush | N/A | N/A | The background color in the control.  
 | Foreground Brush | N/A | N/A  |The foreground color in the control (text color).
**Instance** | Instance Type | Service Manager | N/A | The type of the instance in a **Single Instance Picker** control. The value is a class, such as **Activity**, **Computer**, or a custom class.  
 | Instance type internal name | Service Manager | N/A | The internal name of the **Instance Type** property.  
**Label** | Content | WPF | ContentControl/Content |A fixed string in the label.
 | Font Family | WPF | TextBlock/FontFamily |  
 | Font Size | WPF | TextBlock/FontSize |   
 | Font Style | WPF | TextBlock/FontStyle |   
 | Font Weight | WPF | TextBlock/FontWeight |   
 | Label Binding Mode | WPF | Binding/Mode |  
 | Label Binding Path |Service Manager and WPF | N/A | Included in almost all controls. Binds the control label to the property displayed by the control.  
 | Label binds directly to source | WPF | Binding/BindsDirectlyToSource |   
**Layout** | Height | WPF | FrameworkElement/Height | Can be set to **Auto** or to **NaN**, allowing for dynamic adjustment of size.
 | Horizontal Alignment |WPF | FrameworkElement/HorizontalAlignment |   
 | Minimum Height | WPF | FrameworkElement/MinHeight | Can be set to **Auto** or to **NaN**, allowing for dynamic adjustment of size.
 | Minimum Width | WPF | FrameworkElement/MinWidth | Can be set to **Auto** or **NaN**, allowing for dynamic size adjustment  
 | Vertical Alignment | WPF | FrameworkElement/VerticalAlignment |   
 | Width | WPF | FrameworkElement/Width | Can be set to **Auto** or to **NaN**, allowing for dynamic adjustment of size.  
**List** | List type | Service Manager | N/A | The type of existing or custom list that this control displays.  
 | List type internal name | Service Manager | N/A | The internal name of the **List type** property.  
**Margin | Bottom | WPF | Control/Bottom | Can be set to **Auto** or to **NaN**, allowing for dynamic adjustment of size.
 | Left** | WPF | Control/Left | Can be set to **Auto** or to **NaN**, allowing for dynamic adjustment of size.
 |Right | WPF | Control/Right | Can be set to **Auto** or to **NaN**, allowing for dynamic adjustment of size.  
 |Top | WPF | Control/Top | Can be set to **Auto** or to **NaN**, allowing for dynamic adjustment of size.  
**Miscellaneous** | Flow Direction | WPF |FrameworkElement/FlowDirection |   
 | Focusable | WPF | UIElement/Focusable |   
 | Is Enabled | WPF | UIElement/IsEnabled |   
 | Name |WPF | FrameworkElement/Name |   
**Text** | Accepts the Enter key | WPF | TextBox/AcceptsReturn |  
 | Content | WPF |ContentControl/Content |   
 | Font Family | WPF | TextBlock/FontFamily |   
 | Font Size | WPF | TextBlock/FontSize |   
 | Font Style | WPF |TextBlock/FontStyle |   
 | Font Weight | WPF | TextBlock/FontWeight |  
 | Horizontal Scroll Bar Visibility | WPF | TextBox/HorizontalScrollBarVisibility |  
 | Max Lines | WPF | TextBox/MaxLines |   
 | Text | WPF | TextBox/Text |    
 | Text Wrapping | WPF | TextBlock/TextWrapping |
 | Vertical Scroll Bar Visibility | WPF | TextBox/VerticalScrollBarVisibility | &nbsp;  
