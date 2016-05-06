---
title: Using Management Packs in System Center 2012 - Service Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7e810d66-978b-43a1-9733-7e054779d89c
---
# Using Management Packs in System Center 2012 - Service Manager
There are two types of management packs: sealed management packs and unsealed management packs. A sealed management pack cannot be modified, but an unsealed management pack can be modified.

Unsealed management packs are used to extend [!INCLUDE[smlong12](../Token/smlong12_md.md)] with the information that you must have to implement all or part of a service management process. You can use unsealed management packs to store the custom objects that you create. For example, you can store the objects you create during your testing or evaluation process in an unsealed management pack. Then, you can export that unsealed management pack to a file and then import the file to another environment, such as a production environment. You can also import the same management pack into multiple environments to ensure configuration consistency across [!INCLUDE[smshort](../Token/smshort_md.md)] deployments, and to increase efficiency.

> [!NOTE]
> Only unsealed management packs can be re\-imported.

An unsealed management pack is an .xml file that contains classes, workflows, views, forms, reports, and knowledge articles. Items such as groups, queues, tasks, templates, connectors, and list items are stored in a management pack, but items such as incidents, change requests, computers, and other instances of classes are not stored in a management pack.

By default, [!INCLUDE[smshort](../Token/smshort_md.md)] contains several pre\-imported, sealed management packs that enable core [!INCLUDE[smshort](../Token/smshort_md.md)] features, such as incident management and change management. Also, by default, [!INCLUDE[smshort](../Token/smshort_md.md)] contains the **Default Management Pack** management pack, in which you can store new items that you create. Additionally, [!INCLUDE[smshort](../Token/smshort_md.md)] contains several pre\-imported, unsealed management packs that enable optional features. You can delete unsealed management packs, which might result in the loss of some views, rules, or lists. However, the removal of these optional features will not prevent [!INCLUDE[smshort](../Token/smshort_md.md)] from functioning. You should consider exporting a management pack before you delete it. You can import the management pack later if you need the optional features in a management pack that you deleted.

To use a management pack, import it into [!INCLUDE[smshort](../Token/smshort_md.md)]. The management pack is stored in a .xml, .mp, or a .mpb file that you can import by using the [!INCLUDE[smcons](../Token/smcons_md.md)].

[!INCLUDE[crabout](../Token/crabout_md.md)] management packs key concepts, management packs best practices and other management packs related topics, see [Management Packs: Working with Management Packs](http://go.microsoft.com/fwlink/p/?LinkId=238192).

## Using Management Packs Topics

-   [How to Create a Management Pack File](../Topic/How-to-Create-a-Management-Pack-File.md)

    Describes how to create a management pack file.

-   [How to Export a Management Pack](../Topic/How-to-Export-a-Management-Pack.md)

    Describes how to export a management pack.

-   [How to Import a Management Pack](../Topic/How-to-Import-a-Management-Pack.md)

    Describes how to import a management pack by using the [!INCLUDE[smcons](../Token/smcons_md.md)].

-   [How to Import the Operations Manager Alert Cube Management Pack](../Topic/How-to-Import-the-Operations-Manager-Alert-Cube-Management-Pack.md)

    Describes how to import the Operations Manager Alert Cube management pack manually.

## Other Resources for This Component

-   TechNet Library main page for [System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=220655)

-   [Administrator’s Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209669)

-   [Planning Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209672)

-   [Operations Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=220656)

