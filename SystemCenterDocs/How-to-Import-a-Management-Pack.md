---
title: How to Import a Management Pack
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e824fe75-e7ce-4c55-a819-a0ea3f5c196b
robots: noindex,nofollow
---
# How to Import a Management Pack
Before you can use a management pack in [!INCLUDE[smlong12](Token/smlong12_md.md)], you must import the management pack by using one of the following methods:

-   Use the [!INCLUDE[smcons](Token/smcons_md.md)], as described in this topic.

-   Use the **Import\-SCSMManagementPack** cmdlet from the [!INCLUDE[smshort](Token/smshort_md.md)] module for Windows PowerShell. For more information about this cmdlet, see [Import\-SCSMManagementPack](http://go.microsoft.com/fwlink/p/?LinkID=225396).

When you reimport a sealed management pack, the version of the new management pack must be greater than the version of the initial management pack. The imported, sealed management pack must pass backward\-compatibility verification, and then the objects of the new management pack and the objects of the initial management pack are merged. When you reimport an unsealed management pack, the objects from the new management pack overwrite the objects from the initial management pack.

If the management pack that you want to import depends on other management packs, multi\-select the dependent management packs and import them in a single operation. [!INCLUDE[smshort](Token/smshort_md.md)] will import the management packs in the correct dependency order.

Use the following procedure to import a single management pack, or a management pack bundle \(.mpb file name extension\), by using the [!INCLUDE[smcons](Token/smcons_md.md)]. [!INCLUDE[crabout](Token/crabout_md.md)] working with custom management packs, sealed and unsealed management packs, and bundling management packs, see the [Authoring Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=210314).

### To import a management pack by using the Service Manager console

1.  In the [!INCLUDE[smcons](Token/smcons_md.md)], click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Management Packs**.

3.  In the **Tasks** pane, under **Management Packs**, click **Import**.

4.  In the **Select Management Packs to Import** dialog box, select the management pack file, and then click **Open**.

5.  In the **Import Management Packs** dialog box, click **Add**.

6.  After you have added all the management packs that you want to import, click **Import**, and then click **OK**.

### To validate the import of a management pack

-   In the [!INCLUDE[smcons](Token/smcons_md.md)], select the **Management Packs** view, and ensure that the intended management packs appear in the **Management Packs** list.

![](Image/PSSymbol.gif)You can use Windows PowerShell commands to complete these and other related tasks, as follows:

-   For information about how to use Windows PowerShell to import a management pack, see [Import\-SCSMManagementPack](http://go.microsoft.com/fwlink/p/?LinkID=225396).

-   For information about how to use Windows PowerShell to test the validity of a management pack, see [Test\-SCSMManagementPack](http://go.microsoft.com/fwlink/p/?LinkID=225419).

-   For information about how to use Windows PowerShell to retrieve objects that represent management packs that have been imported, see [Get\-SCSMManagementPack](http://go.microsoft.com/fwlink/p/?LinkID=225404).


