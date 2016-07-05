---
title: Overview of Authoring Methods for Service Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3a58eba0-186c-41db-a8cd-0a10e1d2dcc5
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
# Overview of Authoring Methods for Service Manager
There are three methods that you can use to customize [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)]. While all three methods result in changes to a management pack file, they differ in scope and in the complexity of the customization that they provide.  
  
 The three methods for customizing and extending [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] are as follows:  
  
-   Using the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)]  
  
-   Using the [!INCLUDE[smatfull2012](../../../sm/manage/author/includes/smatfull2012_md.md)]  
  
-   Directly modifying and authoring management pack files  
  
 In general, we recommend that you use the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)] or the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)] for simple customizations and that you work directly with the management pack files only for customizations that the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)] and the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)] do not support.  
  
## Using the Service Manager Console  
 In [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)], the **Administration** pane and the **Authoring** pane in the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)] provide for limited ad hoc customization of [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] features. When you customize [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] features in the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], the customizations are stored in new or existing unsealed management packs and in the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database. \(Unsealed management packs are management packs that you can modify. For more information about sealed and unsealed management packs, see [Management Packs: Key Concepts](../Topic/Management%20Packs:%20Key%20Concepts.md)\).  
  
 The [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)] provides for the following customizations:  
  
-   In the **Administration** pane, you can customize settings for activities, change management, incident management, and notifications. For example, you can configure the list notification recipients when an incident changes status.  
  
-   In the **Authoring** pane, you can make simple customizations to objects, such as queues, lists, and views.  
  
 [!INCLUDE[crabout](../../../sm/deploy/deploy-guide/includes/crabout_md.md)] customizations you can make from the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], see the [Administrator's Guide for System Center 2012 \- Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209669).  
  
## Using the Authoring Tool  
 The [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)] provides an environment in which you can open, view, customize, extend, and author Service Manager management packs. You can use the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)] to modify some class properties, customize forms in a graphical form designer, and modify and create [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] workflows.  
  
 You can also use the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)] to create advanced customizations that require testing and verification before implementation. The [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)] does not require advanced user skills or advanced knowledge of the internal architecture of [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)].  
  
## Directly Modifying and Authoring Management Pack Files  
 For extensive or complex customizations and for customizations that require coding \(such as extending the data in the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database, customizing forms, or modifying the default behavior of a feature’s workflow\), you have to edit the .xml file of the corresponding management pack directly. Working directly with management pack files requires in\-depth knowledge in several areas, such as the System Center Common Schema and the structure of management packs. Also, manual editing is prone to errors.  
  
## See Also  
 [Introduction to the Service Manager Authoring Guide](../../../sm/manage/author/Introduction-to-the-Service-Manager-Authoring-Guide.md)