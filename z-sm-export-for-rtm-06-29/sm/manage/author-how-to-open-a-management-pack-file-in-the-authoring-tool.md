---
title: How to Open a Management Pack File in the Authoring Tool
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4bdf68fc-5ff9-48b0-bedf-d7364b38b0e5


















---
# How to Open a Management Pack File in the Authoring Tool
If you want to customize objects that are defined in a management pack in System Center 2012 - Service Manager, you have to open the management pack file that contains these objects in the System Center 2016 - Service Manager Authoring Tool. You can use the following procedure to open a management pack file in the Authoring Tool.  
  
 The **Management Pack Explorer** pane in the Authoring Tool displays all the management packs that are open. A management pack that you open and change is designated with an asterisk \(\*\)-for example, CustomMP\*-until it is saved.  
  
 When you select a management pack file to open, the system opens the specified management pack. In addition, it opens the following management packs:  
  
-   All the other management packs that are located in the same folder as the management pack that you are opening  
  
-   All the management packs in the Library folder in the Service Manager installation folder, for example, in the \\Program Files \(x86\)\\Microsoft System Center\\Service Manager&nbsp;2012 Authoring\\Library folder  
  
 This is important because the definitions from all open management packs co\-exist in the Authoring Tool; therefore, they cannot contradict each other.  
  
> [!NOTE]  
>  You cannot create new management pack files in the \<Authoring Tool Installation\>\\Library folder.  
  
### To open a management pack file  
  
1.  On your desktop, click **Start**.  
  
2.  Click **Service Manager Authoring Tool**, and wait for the Authoring Tool to open.  
  
3.  In the Authoring Tool, on the menu bar, click **File**, and then click **Open**.  
  
4.  In the **Open File** dialog box, select the management pack file that you want to open, and then click **Open**. The file that you select must have an .xml or .mp file name extension. For example, select **Management Packs** as the file type, and then select the following management pack file:  
  
     \<Authoring Tool installation drive\>\\Program Files \(x86\)\\Microsoft System Center\\Service Manager&nbsp;2012 Authoring\\Library\\ServiceManager.IncidentManagement.Library.mp  
  
5.  Wait for the management pack to open, and then verify that it is displayed in the **Management Pack Explorer** pane.  
  
 You can now select the management pack file that you opened, and you can expand **Classes**, **Forms**, **Workflows**, or **References** to view the objects of the management pack.  
  
## See Also  
 [Working with Management Packs in the Authoring Tool](../../../sm/manage/author/Working-with-Management-Packs-in-the-Authoring-Tool.md)
