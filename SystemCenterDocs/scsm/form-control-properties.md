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

## Control properties  
 Most properties of Service Manager forms are based on Windows Presentation Foundation (WPF) properties, and other properties are defined by Service Manager. The following table provides details about the WPF-based property groups and their respective properties, when they are applicable. For more information about WPF properties, see [System.Windows.Controls Namespace](http://go.microsoft.com/fwlink/p/?LinkID=204425) on MSDN.  

|Service Manager property group|Service Manager property name|Source of property|WPF-based property group/property|Additional information|  
|------------------------------------------|-----------------------------------------|------------------------|-----------------------------------------|----------------------------|  
|Appearance|Opacity|WPF|UIElement/Opacity||  
||Visibility|WPF|UIElement/Visibility||  
|Binding|Binding Mode|WPF|Binding/Mode||  
||Binding Path|Service Manager and WPF|Binding/Path|Binds the control to the property that the control displays. The control dynamically displays the property that it is bound to, updating the value as it changes. The type of the control and the type of the displayed property must match; for example, the type of the **Binding Path** property of a **Date Picker** control must be **Date**.|  
||Binds directly to source|WPF|Binding/BindsDirectlyToSource||  
|Date|Date Format|Service Manager|N/A|The format in which the control displays the date, such as "Full date and time", and "Short".|  
|Drawing|Source Path|Service Manager|N/A|A path to the image file in an **Image** control.|  
||Stretch|WPF|Image/Stretch||  
||Stretch Direction|WPF|Viewbox/StretchDirection||  
|Brush|Background Brush|N/A|N/A|The background color in the control.|  
||Foreground Brush|N/A|N/A|The foreground color in the control, basically, the color of text.|  
|Instance|Instance Type|Service Manager|N/A|The type of the instance in a **Single Instance Picker** control. The value is a class, such as **Activity**, **Computer**, or a custom class.|  
||Instance type internal name|Service Manager|N/A|The internal name of the **Instance Type** property.|  
|Label|Content|WPF|ContentControl/Content|A fixed string to be displayed in the label.|  
||Font Family|WPF|TextBlock/FontFamily||  
||Font Size|WPF|TextBlock/FontSize||  
||Font Style|WPF|TextBlock/FontStyle||  
||Font Weight|WPF|TextBlock/FontWeight||  
||Label Binding Mode|WPF|Binding/Mode||  
||Label Binding Path|Service Manager and WPF|N/A|Included in almost all controls. Binds the label of the control to the property that this control displays.|  
||Label binds directly to source|WPF|Binding/BindsDirectlyToSource||  
|Layout|Height|WPF|FrameworkElement/Height|Can be set to **Auto** or to **NaN**, allowing for dynamic adjustment of size.|  
||Horizontal Alignment|WPF|FrameworkElement/HorizontalAlignment||  
||Minimum Height|WPF|FrameworkElement/MinHeight|Can be set to **Auto** or to **NaN**, allowing for dynamic adjustment of size.|  
||Minimum Width|WPF|FrameworkElement/MinWidth|Can be set to **Auto** or to **NaN**, allowing for dynamic adjustment of size.|  
||Vertical Alignment|WPF|FrameworkElement/VerticalAlignment||  
||Width|WPF|FrameworkElement/Width|Can be set to **Auto** or to **NaN**, allowing for dynamic adjustment of size.|  
|List|List type|Service Manager|N/A|The type of list that this control displays. This can be an existing list or a custom list.|  
||List type internal name|Service Manager|N/A|The internal name of the **List type** property.|  
|Margin|Bottom|WPF|Control/Bottom|Can be set to **Auto** or to **NaN**, allowing for dynamic adjustment of size.|  
||Left|WPF|Control/Left|Can be set to **Auto** or to **NaN**, allowing for dynamic adjustment of size.|  
||Right|WPF|Control/Right|Can be set to **Auto** or to **NaN**, allowing for dynamic adjustment of size.|  
||Top|WPF|Control/Top|Can be set to **Auto** or to **NaN**, allowing for dynamic adjustment of size.|  
|Miscellaneous|Flow Direction|WPF|FrameworkElement/FlowDirection||  
||Focusable|WPF|UIElement/Focusable||  
||Is Enabled|WPF|UIElement/IsEnabled||  
||Name|WPF|FrameworkElement/Name||  
|Text|Accepts the Enter key|WPF|TextBox/AcceptsReturn||  
||Content|WPF|ContentControl/Content||  
||Font Family|WPF|TextBlock/FontFamily||  
||Font Size|WPF|TextBlock/FontSize||  
||Font Style|WPF|TextBlock/FontStyle||  
||Font Weight|WPF|TextBlock/FontWeight||  
||Horizontal Scroll Bar Visibility|WPF|TextBox/HorizontalScrollBarVisibility||  
||Max Lines|WPF|TextBox/MaxLines||  
||Text|WPF|TextBox/Text||  
||Text Wrapping|WPF|TextBlock/TextWrapping||  
| | Vertical Scroll Bar Visibility | WPF | TextBox/VerticalScrollBarVisibility | &nbsp; |  
