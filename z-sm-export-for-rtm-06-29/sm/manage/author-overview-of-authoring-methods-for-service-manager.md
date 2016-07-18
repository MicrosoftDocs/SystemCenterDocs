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
 

















---
# Overview of Authoring Methods for Service Manager
There are three methods that you can use to customize System Center 2012 - Service Manager. While all three methods result in changes to a management pack file, they differ in scope and in the complexity of the customization that they provide.  
  
 The three methods for customizing and extending Service Manager are as follows:  
  
-   Using the Service Manager console  
  
-   Using the System Center 2016 - Service Manager Authoring Tool  
  
-   Directly modifying and authoring management pack files  
  
 In general, we recommend that you use the Service Manager console or the Authoring Tool for simple customizations and that you work directly with the management pack files only for customizations that the Service Manager console and the Authoring Tool do not support.  
  
## Using the Service Manager Console  
 In System Center 2012 - Service Manager, the **Administration** pane and the **Authoring** pane in the Service Manager console provide for limited ad hoc customization of Service Manager features. When you customize Service Manager features in the Service Manager console, the customizations are stored in new or existing unsealed management packs and in the Service Manager database. \(Unsealed management packs are management packs that you can modify. For more information about sealed and unsealed management packs, see [Management Packs: Key Concepts](../Topic/Management%20Packs:%20Key%20Concepts.md)\).  
  
 The Service Manager console provides for the following customizations:  
  
-   In the **Administration** pane, you can customize settings for activities, change management, incident management, and notifications. For example, you can configure the list notification recipients when an incident changes status.  
  
-   In the **Authoring** pane, you can make simple customizations to objects, such as queues, lists, and views.  
  
 For more information about customizations you can make from the Service Manager console, see the [Administrator's Guide for System Center 2012 \- Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209669).  
  
## Using the Authoring Tool  
 The Authoring Tool provides an environment in which you can open, view, customize, extend, and author Service Manager management packs. You can use the Authoring Tool to modify some class properties, customize forms in a graphical form designer, and modify and create Service Manager workflows.  
  
 You can also use the Authoring Tool to create advanced customizations that require testing and verification before implementation. The Authoring Tool does not require advanced user skills or advanced knowledge of the internal architecture of Service Manager.  
  
## Directly Modifying and Authoring Management Pack Files  
 For extensive or complex customizations and for customizations that require coding \(such as extending the data in the Service Manager database, customizing forms, or modifying the default behavior of a feature’s workflow\), you have to edit the .xml file of the corresponding management pack directly. Working directly with management pack files requires in\-depth knowledge in several areas, such as the System Center Common Schema and the structure of management packs. Also, manual editing is prone to errors.  
  
## See Also  
 [Introduction to the Service Manager Authoring Guide](../../../sm/manage/author/Introduction-to-the-Service-Manager-Authoring-Guide.md)
