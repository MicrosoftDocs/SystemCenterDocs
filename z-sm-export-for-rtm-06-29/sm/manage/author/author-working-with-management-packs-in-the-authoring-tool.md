---
title: Working with Management Packs in the Authoring Tool
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 16ddf6aa-46d8-4b31-99d0-569a63565407
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
# Working with Management Packs in the Authoring Tool
[!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] objects are stored in management packs. To modify an object using the [!INCLUDE[smatfull2012](../../../sm/manage/author/includes/smatfull2012_md.md)], you open the management pack file that contains that object. To capture changes that you made in the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)], you then save the changes in the original management pack file or in a new management pack file. If the original object that you changed is defined in a sealed management pack, you must save your changes in a new or an existing unsealed management pack. Unlike [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)], to save modified objects the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)] manipulates the actual management pack files on the hard drive—in an offline mode, without direct interaction with the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database.  
  
 Later, to implement these changes, you import the management pack file into the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)], which updates the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database with the information from the management pack file. You can also import the management pack file into a different environment, such as a production environment. When you import a management pack, the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] server examines the XML code in the management pack file. If the management pack file contains XML code that is not valid, the management pack is not imported.  
  
 The procedures in this section describe how to work with management pack files in the [!INCLUDE[scauthoringshort](../../../sm/manage/author/includes/scauthoringshort_md.md)].  
  
## Working with Management Packs in the Authoring Tool Topics  
  
-   [How to Open a Management Pack File in the Authoring Tool](../../../sm/manage/author/How-to-Open-a-Management-Pack-File-in-the-Authoring-Tool.md)  
  
     Describes how to open a management pack file.  
  
-   [How to Create a New Management Pack File in the Authoring Tool](../../../sm/manage/author/How-to-Create-a-New-Management-Pack-File-in-the-Authoring-Tool.md)  
  
     Describes how to create a new management pack file.