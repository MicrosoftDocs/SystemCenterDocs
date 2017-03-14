---
title: Work with management packs in the Authoring Tool
description: Describes how to work with management packs in the Service Manager Authoring Tool.
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
ms.assetid: 16ddf6aa-46d8-4b31-99d0-569a63565407
---

# Work with management packs in the Service Manager Authoring Tool

>Applies To: System Center 2016 - Service Manager

Service Manager objects are stored in management packs. To modify an object using the Service Manager Authoring Tool, you open the management pack file that contains that object. To capture changes that you made in the Authoring Tool, you then save the changes in the original management pack file or in a new management pack file. If the original object that you changed is defined in a sealed management pack, you must save your changes in a new or an existing unsealed management pack. Unlike Service Manager, to save modified objects the Authoring Tool manipulates the actual management pack files on the hard drive-in an offline mode, without direct interaction with the Service Manager database.  

 Later, to implement these changes, you import the management pack file into the Service Manager console, which updates the Service Manager database with the information from the management pack file. You can also import the management pack file into a different environment, such as a production environment. When you import a management pack, the Service Manager server examines the XML code in the management pack file. If the management pack file contains XML code that is not valid, the management pack is not imported.  

 The procedures in this section describe how to work with management pack files in the Authoring Tool.  

## Open a management pack file in the Authoring Tool

If you want to customize objects that are defined in a management pack in Service Manager, you have to open the management pack file that contains these objects in the Service Manager Authoring Tool. You can use the following procedure to open a management pack file in the Authoring Tool.  

 The **Management Pack Explorer** pane in the Authoring Tool displays all the management packs that are open. A management pack that you open and change is designated with an asterisk \(\*\) -for example, CustomMP\* -until it is saved.  

 When you select a management pack file to open, the system opens the specified management pack. In addition, it opens the following management packs:  

-   All the other management packs that are located in the same folder as the management pack that you are opening  

-   All the management packs in the Library folder in the Service Manager installation folder, for example, in the \\Program Files \(x86\)\\Microsoft System Center\\Service Manager 2016 Authoring\\Library folder  

 This is important because the definitions from all open management packs co\-exist in the Authoring Tool; therefore, they cannot contradict each other.  

> [!NOTE]  
>  You cannot create new management pack files in the \<Authoring Tool Installation\>\\Library folder.  

### To open a management pack file  

1.  On your desktop, click **Start**.  

2.  Click **Service Manager Authoring Tool**, and wait for the Authoring Tool to open.  

3.  In the Authoring Tool, on the menu bar, click **File**, and then click **Open**.  

4.  In the **Open File** dialog box, select the management pack file that you want to open, and then click **Open**. The file that you select must have an .xml or .mp file name extension. For example, select **Management Packs** as the file type, and then select the following management pack file:  

     \<Authoring Tool installation drive\>\\Program Files \(x86\)\\Microsoft System Center\\Service Manager 2016 Authoring\\Library\\ServiceManager.IncidentManagement.Library.mp  

5.  Wait for the management pack to open, and then verify that it is displayed in the **Management Pack Explorer** pane.  

 You can now select the management pack file that you opened, and you can expand **Classes**, **Forms**, **Workflows**, or **References** to view the objects of the management pack.

## Create a new management pack file in the Authoring Tool

To be able to implement customizations that you make in the Service Manager Authoring Tool, you have to save them to a management pack file.  

 If you customize an object from a sealed management pack, you will not be able to save that customization in the original sealed management pack. In this case, you can either use an existing unsealed management pack or you can create a new management pack, which by default will be unsealed.  

 You can use the following procedure to create a new management pack file.  

### To create a new management pack file  

1.  On your desktop, click **Start**.  

2.  Click **Service Manager Authoring Tool**, and wait for the Authoring Tool to open.  

3.  In the Authoring Tool, on the menu bar, click **File**, and then click **New**.  

4.  In the **New Management Pack** dialog box, enter a file name and a location for the new management pack file.  

     Ensure that the file name that you enter does not contain spaces or special characters, and do not specify the Authoring Tool installation folder as the location for new and customized management pack files.  

5.  Click **Open**.  

6.  In the **Management Pack Explorer**, verify that the new management pack is listed.  
