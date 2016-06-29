---
title: Upgrading Management Packs to Work with the Authoring Tool in System Center 2012 - Service Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0bd5c809-4ccc-40e0-9b67-68d7ccece193
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
# Upgrading Management Packs to Work with the Authoring Tool in System Center 2012 - Service Manager
During an upgrade of [!INCLUDE[smlong](../../../sm/deploy/upgrade/includes/smlong_md.md)] to [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)], all [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] customized, unsealed. \(Unsealed management packs are management packs that you can modify. For more information about sealed and unsealed management packs, see [Management Packs: Key Concepts](../Topic/Management%20Packs:%20Key%20Concepts.md)\).management packs are copied to the new [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] folders without any further upgrade\-related processing. Using these custom management packs that were authored in [!INCLUDE[smlong](../../../sm/deploy/upgrade/includes/smlong_md.md)] in [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] is supported. However, there are some issues to be aware of, and you may have to make some updates to these management packs to ensure that they work properly and as intended after the upgrade to [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)].  
  
## Forms  
 The placement of a control in a form is determined by its top, bottom, left, and right margins in relation to either its parent control or to the form itself. In a customized form, this method can cause controls to be adjusted improperly when the margins of the parent control or of the form are modified.  
  
 As a result of new styles that were implemented in [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)], some custom forms that were authored in [!INCLUDE[smlong](../../../sm/deploy/upgrade/includes/smlong_md.md)] might have layout issues when they are imported into [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)]. Depending on the customization, some controls might be placed incorrectly, causing issues such as overlapping and clipping. Some of these issues affect only how the form looks, and other issues can prevent some intended functionality of the form.  
  
 The following sections describe the issues that you might encounter when you import into [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] forms that were authored in [!INCLUDE[smlong](../../../sm/deploy/upgrade/includes/smlong_md.md)]. These sections also describe how you can use the [!INCLUDE[smatfull2012](../../../sm/manage/author/includes/smatfull2012_md.md)] to rectify these issues to ensure that these forms look and function as intended.  
  
### Clipping and Overlapping Controls  
 Some controls on a form might appear clipped, with incomplete border lines and cut\-off text. Sometimes this issue appears in conjunction with another issue in which controls overlap each other. Also, some controls on a form might not be visible, causing some functionality of the form to be unavailable.  
  
 To rectify these issues, you may have to use the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)] to adjust the control’s properties as follows. You may have to try several remedies, and you may have to make several attempts before the control is placed correctly.  
  
-   Select the affected control, and check the value of its **Margin** properties: **Bottom**, **Left**, **Right**, and **Top**. For example, set the values of these properties to 0, or to a positive value, to ensure that there are no negative values that cause the control to be placed incorrectly.  
  
-   Check the values of the affected control’s **Layout** group properties: **Horizontal Alignment** and **Vertical Alignment**. You may have to set the values of these properties to **Stretch** for better control alignment.  
  
-   Place the affected control in a grid inside a **Panel** control for better control alignment.  
  
-   Set the parent control’s dimensions to **Auto** to allow its size to shrink or grow dynamically.  
  
-   Set the **Height** property of the container of the affected control to **Auto**. This allows the width and the height of controls to be automatically adjusted correctly to fit the container of the object.  
  
### Shuffling of Controls  
 Some controls on a form might be shuffled with each other, resulting in controls not being placed in their designated location on the form.  
  
 To rectify this issue, use the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)] to do one of the following:  
  
-   Drag controls to their desired location on the form.  
  
-   Select the control that is shuffled. In the **Details** pane, in the **Margin** properties group, adjust properties such as **Bottom** or **Left** to place the control in the desired location.  
  
-   Select the control that contains the shuffled control. In the **Details** pane, modify its properties such as **Bottom** or **Left**, in the **Margin** properties group.  
  
## Workflows  
 Workflows that were developed in [!INCLUDE[smlong](../../../sm/deploy/upgrade/includes/smlong_md.md)] are supported in [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)].  
  
### Virtual Machine Management Activities  
 The Virtual Machine Management workflow activities in [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] support [!INCLUDE[vmlongname2008R2](../../../sm/manage/author/includes/vmlongname2008R2_md.md)]. However, these activities do not support [!INCLUDE[vmm12long](../../../sm/manage/author/includes/vmm12long_md.md)].  
  
 If you are trying to automate IT processes that require the use of an activity that supports [!INCLUDE[vmm12long](../../../sm/manage/author/includes/vmm12long_md.md)], using [!INCLUDE[orchlong](../../../sm/manage/author/includes/orchlong_md.md)] runbooks and [!INCLUDE[vmm12short](../../../sm/manage/author/includes/vmm12short_md.md)] instead might be helpful.  
  
## See Also  
 [Overview of the Authoring Tool for System Center 2012 – Service Manager](../Topic/Overview%20of%20the%20Authoring%20Tool%20for%20System%20Center%202012%20%E2%80%93%20Service%20Manager.md)