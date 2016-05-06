---
title: How to Create a Management Pack File
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 003af002-b23b-4a12-a208-705de4621b8a
robots: noindex,nofollow
---
# How to Create a Management Pack File
You can use the following procedures to create a management pack file in [!INCLUDE[smlong12](../Token/smlong12_md.md)]. After you create the management pack file, you can use it to store objects that you create.

For more information about how to create and customize management packs, see [Management Packs: Working with Management Packs](http://go.microsoft.com/fwlink/p/?LinkID=207159).

### To create a management pack file

1.  In the [!INCLUDE[smcons](../Token/smcons_md.md)], click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Management Packs**.

3.  In the **Tasks** pane, under **Management Packs**, click **Create Management Pack**.

4.  In the **Create Management Pack** dialog box, enter a name, such as **Sample Management Pack**, and then enter a description for the new management pack. Click **OK**.

### To validate the creation of a management pack file

-   In the [!INCLUDE[smcons](../Token/smcons_md.md)], open the **Management Packs** view, and verify that the new management pack appears in the **Management Packs** pane.

![](../Image/PSSymbol.gif)You can use Windows PowerShell commands to complete these tasks, as follows:

-   For information about how to use Windows PowerShell to create a new management pack, see [New\-SCSMManagementPack](http://go.microsoft.com/fwlink/p/?LinkID=225411).

-   For information about how to use Windows PowerShell to seal a management pack, preventing it from being modified, see [Protect\-SCSMManagementPack](http://go.microsoft.com/fwlink/p/?LinkID=225413).

-   For information about how to use Windows PowerShell to remove management packs, see [Remove\-SCSMManagementPack](http://go.microsoft.com/fwlink/p/?LinkID=225416).

