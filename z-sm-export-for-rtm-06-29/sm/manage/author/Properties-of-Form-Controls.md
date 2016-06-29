---
title: Properties of Form Controls
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7d62ce9b-fd6d-4521-932d-f2ede5920955
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
# Properties of Form Controls
The table in this topic lists the properties of [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] form controls. This information can help you customize and create forms in the [!INCLUDE[smatfull2012](../../../sm/manage/author/includes/smatfull2012_md.md)].  
  
## Table of Control Properties  
 Most properties of [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] forms are based on Windows Presentation Foundation \(WPF\) properties, and other properties are defined by [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)]. The following table provides details about the WPF\-based property groups and their respective properties, when they are applicable. For more information about WPF properties, see [System.Windows.Controls Namespace](http://go.microsoft.com/fwlink/p/?LinkID=204425) on MSDN.  
  
|[!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] property group|[!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] property name|Source of property|WPF\-based property group\/property|Additional information|  
|------------------------------------------|-----------------------------------------|------------------------|-----------------------------------------|----------------------------|  
|Appearance|Opacity|WPF|UIElement\/Opacity||  
||Visibility|WPF|UIElement\/Visibility||  
|Binding|Binding Mode|WPF|Binding\/Mode||  
||Binding Path|[!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] and WPF|Binding\/Path|Binds the control to the property that the control displays. The control dynamically displays the property that it is bound to, updating the value as it changes. The type of the control and the type of the displayed property must match; for example, the type of the **Binding Path** property of a **Date Picker** control must be **Date**.|  
||Binds directly to source|WPF|Binding\/BindsDirectlyToSource||  
|Date|Date Format|[!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)]|N\/A|The format in which the control displays the date, such as “Full date and time”, and “Short”.|  
|Drawing|Source Path|[!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)]|N\/A|A path to the image file in an **Image** control.|  
||Stretch|WPF|Image\/Stretch||  
||Stretch Direction|WPF|Viewbox\/StretchDirection||  
|Brush|Background Brush|N\/A|N\/A|The background color in the control.|  
||Foreground Brush|N\/A|N\/A|The foreground color in the control, basically, the color of text.|  
|Instance|Instance Type|[!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)]|N\/A|The type of the instance in a **Single Instance Picker** control. The value is a class, such as **Activity**, **Computer**, or a custom class.|  
||Instance type internal name|[!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)]|N\/A|The internal name of the **Instance Type** property.|  
|Label|Content|WPF|ContentControl\/Content|A fixed string to be displayed in the label.|  
||Font Family|WPF|TextBlock\/FontFamily||  
||Font Size|WPF|TextBlock\/FontSize||  
||Font Style|WPF|TextBlock\/FontStyle||  
||Font Weight|WPF|TextBlock\/FontWeight||  
||Label Binding Mode|WPF|Binding\/Mode||  
||Label Binding Path|[!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] and WPF|N\/A|Included in almost all controls. Binds the label of the control to the property that this control displays.|  
||Label binds directly to source|WPF|Binding\/BindsDirectlyToSource||  
|Layout|Height|WPF|FrameworkElement\/Height|Can be set to **Auto** or to **NaN**, allowing for dynamic adjustment of size.|  
||Horizontal Alignment|WPF|FrameworkElement\/HorizontalAlignment||  
||Minimum Height|WPF|FrameworkElement\/MinHeight|Can be set to **Auto** or to **NaN**, allowing for dynamic adjustment of size.|  
||Minimum Width|WPF|FrameworkElement\/MinWidth|Can be set to **Auto** or to **NaN**, allowing for dynamic adjustment of size.|  
||Vertical Alignment|WPF|FrameworkElement\/VerticalAlignment||  
||Width|WPF|FrameworkElement\/Width|Can be set to **Auto** or to **NaN**, allowing for dynamic adjustment of size.|  
|List|List type|[!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)]|N\/A|The type of list that this control displays. This can be an existing list or a custom list.|  
||List type internal name|[!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)]|N\/A|The internal name of the **List type** property.|  
|Margin|Bottom|WPF|Control\/Bottom|Can be set to **Auto** or to **NaN**, allowing for dynamic adjustment of size.|  
||Left|WPF|Control\/Left|Can be set to **Auto** or to **NaN**, allowing for dynamic adjustment of size.|  
||Right|WPF|Control\/Right|Can be set to **Auto** or to **NaN**, allowing for dynamic adjustment of size.|  
||Top|WPF|Control\/Top|Can be set to **Auto** or to **NaN**, allowing for dynamic adjustment of size.|  
|Miscellaneous|Flow Direction|WPF|FrameworkElement\/FlowDirection||  
||Focusable|WPF|UIElement\/Focusable||  
||Is Enabled|WPF|UIElement\/IsEnabled||  
||Name|WPF|FrameworkElement\/Name||  
|Text|Accepts the Enter key|WPF|TextBox\/AcceptsReturn||  
||Content|WPF|ContentControl\/Content||  
||Font Family|WPF|TextBlock\/FontFamily||  
||Font Size|WPF|TextBlock\/FontSize||  
||Font Style|WPF|TextBlock\/FontStyle||  
||Font Weight|WPF|TextBlock\/FontWeight||  
||Horizontal Scroll Bar Visibility|WPF|TextBox\/HorizontalScrollBarVisibility||  
||Max Lines|WPF|TextBox\/MaxLines||  
||Text|WPF|TextBox\/Text||  
||Text Wrapping|WPF|TextBlock\/TextWrapping||  
||Vertical Scroll Bar Visibility|WPF|TextBox\/VerticalScrollBarVisibility||  
  
## See Also  
 [Working with Forms in the Authoring Tool](assetId:///605c375d-4421-47c0-8b96-fbcbb5385f0c)