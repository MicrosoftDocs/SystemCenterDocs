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
 

















---
# Working with Management Packs in the Authoring Tool
System Center 2012 - Service Manager objects are stored in management packs. To modify an object using the System Center 2016 - Service Manager Authoring Tool, you open the management pack file that contains that object. To capture changes that you made in the Authoring Tool, you then save the changes in the original management pack file or in a new management pack file. If the original object that you changed is defined in a sealed management pack, you must save your changes in a new or an existing unsealed management pack. Unlike Service Manager, to save modified objects the Authoring Tool manipulates the actual management pack files on the hard drive-in an offline mode, without direct interaction with the Service Manager database.  
  
 Later, to implement these changes, you import the management pack file into the Service Manager console, which updates the Service Manager database with the information from the management pack file. You can also import the management pack file into a different environment, such as a production environment. When you import a management pack, the Service Manager server examines the XML code in the management pack file. If the management pack file contains XML code that is not valid, the management pack is not imported.  
  
 The procedures in this section describe how to work with management pack files in the Authoring Tool.  
  
## Working with Management Packs in the Authoring Tool Topics  
  
-   [How to Open a Management Pack File in the Authoring Tool](../../../sm/manage/author/How-to-Open-a-Management-Pack-File-in-the-Authoring-Tool.md)  
  
     Describes how to open a management pack file.  
  
-   [How to Create a New Management Pack File in the Authoring Tool](../../../sm/manage/author/How-to-Create-a-New-Management-Pack-File-in-the-Authoring-Tool.md)  
  
     Describes how to create a new management pack file.
