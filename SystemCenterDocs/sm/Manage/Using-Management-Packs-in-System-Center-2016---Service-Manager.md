---
title: Using Management Packs in System Center 2016 - Service Manager
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3c42925f-74f3-4c18-934e-8d1cd2edaa3b
---
# Using Management Packs in System Center 2016 - Service Manager
There are two types of management packs: sealed management packs and unsealed management packs. A sealed management pack cannot be modified, but an unsealed management pack can be modified.

Unsealed management packs are used to extend [!INCLUDE[scsm_threshold_1](../../includes/scsm_threshold_1_md.md)] with the information that you must have to implement all or part of a service management process. You can use unsealed management packs to store the custom objects that you create. For example, you can store the objects you create during your testing or evaluation process in an unsealed management pack. Then, you can export that unsealed management pack to a file and then import the file to another environment, such as a production environment. You can also import the same management pack into multiple environments to ensure configuration consistency across [!INCLUDE[smshort12](../../includes/smshort12_md.md)] deployments, and to increase efficiency.

> [!NOTE]
> Only unsealed management packs can be re\-imported.

An unsealed management pack is an .xml file that contains classes, workflows, views, forms, reports, and knowledge articles. Items such as groups, queues, tasks, templates, connectors, and list items are stored in a management pack, but items such as incidents, change requests, computers, and other instances of classes are not stored in a management pack.

By default, [!INCLUDE[smshort12](../../includes/smshort12_md.md)] contains several pre\-imported, sealed management packs that enable core [!INCLUDE[smshort12](../../includes/smshort12_md.md)] features, such as incident management and change management. Also, by default, [!INCLUDE[smshort12](../../includes/smshort12_md.md)] contains the **Default Management Pack** management pack, in which you can store new items that you create. Additionally, [!INCLUDE[smshort12](../../includes/smshort12_md.md)] contains several pre\-imported, unsealed management packs that enable optional features. You can delete unsealed management packs, which might result in the loss of some views, rules, or lists. However, the removal of these optional features will not prevent [!INCLUDE[smshort12](../../includes/smshort12_md.md)] from functioning. You should consider exporting a management pack before you delete it. You can import the management pack later if you need the optional features in a management pack that you deleted.

To use a management pack, import it into [!INCLUDE[smshort12](../../includes/smshort12_md.md)]. The management pack is stored in a .xml, .mp, or a .mpb file that you can import by using the [!INCLUDE[smcons](../../includes/smcons_md.md)].

[!INCLUDE[crabout](../../includes/crabout_md.md)] management packs key concepts, management packs best practices and other management packs related topics, see [Management Packs: Working with Management Packs](http://go.microsoft.com/fwlink/p/?LinkId=238192).

## How to Create a Management Pack File

You can use the following procedures to create a management pack file in Service Manager. After you create the management pack file, you can use it to store objects that you create.

For more information about how to create and customize management packs, see [Management Packs: Working with Management Packs](http://go.microsoft.com/fwlink/p/?LinkID=207159).

### To create a management pack file

1.  In the [!INCLUDE[smcons](../../includes/smcons_md.md)], click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Management Packs**.

3.  In the **Tasks** pane, under **Management Packs**, click **Create Management Pack**.

4.  In the **Create Management Pack** dialog box, enter a name, such as **Sample Management Pack**, and then enter a description for the new management pack. Click **OK**.

### To validate the creation of a management pack file

-   In the [!INCLUDE[smcons](../../includes/smcons_md.md)], open the **Management Packs** view, and verify that the new management pack appears in the **Management Packs** pane.

![](../../media/pssymbol.png)You can use Windows PowerShell commands to complete these tasks, as follows:

-   For information about how to use Windows PowerShell to create a new management pack, see [New\-SCSMManagementPack](http://go.microsoft.com/fwlink/p/?LinkID=225411).

-   For information about how to use Windows PowerShell to seal a management pack, preventing it from being modified, see [Protect\-SCSMManagementPack](http://go.microsoft.com/fwlink/p/?LinkID=225413).

-   For information about how to use Windows PowerShell to remove management packs, see [Remove\-SCSMManagementPack](http://go.microsoft.com/fwlink/p/?LinkID=225416).

 

## How to Export a Management Pack

After you create a management pack in Service Manager, you can export the unsealed management pack as a file to back up any customizations in the management pack. The exported management pack is a valid XML\-formatted file. After you export an unsealed management pack, you can later import it to restore the objects that the management pack contains.

When you export a sealed management pack, from the [!INCLUDE[smcons](../../includes/smcons_md.md)] or by using the Windows PowerShell cmdlet [Export\-SCSMManagementPack](http://go.microsoft.com/fwlink/p/?LinkID=225398), [!INCLUDE[smshort](../../includes/smshort_md.md)] generates an equivalent, unsealed management pack and stores it as a .XML file on the hard drive. You can then edit this management pack file to increase the version of the management pack, and re\-seal it so it can be re\-imported into [!INCLUDE[smshort](../../includes/smshort_md.md)].

Use the following procedures to export an unsealed management pack and then validate the export.

### To export a management pack

1.  In the [!INCLUDE[smcons](../../includes/smcons_md.md)], click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Management Packs**.

3.  In the **Management Packs** pane, select the management pack that you want to export.

4.  In the **Tasks** pane, under the name of the management pack that you want to export, click **Export**.

5.  In the **Browse For Folder** dialog box, select a location for the file, and then click **OK**.

    > [!NOTE]
    > You cannot change the default name of the management pack file.

### To validate the export of a management pack

-   In Windows Explorer, ensure that you can locate the management pack file.

![](../../media/pssymbol.png)You can use Windows PowerShell commands to complete this task. For information about how to use Windows PowerShell to export a management pack as a valid XML\-formatted file that you can later import into [!INCLUDE[smshort](../../includes/smshort_md.md)] or [!INCLUDE[om12short](../../includes/om12short_md.md)], see [Export\-SCSMManagementPack](http://go.microsoft.com/fwlink/p/?LinkID=225398).


## How to Import a Management Pack

Before you can use a management pack in [!INCLUDE[smshort](../../includes/smshort_md.md)], you must import the management pack by using one of the following methods:

-   Use the [!INCLUDE[smcons](../../includes/smcons_md.md)], as described in this topic.

-   Use the **Import\-SCSMManagementPack** cmdlet from the [!INCLUDE[smshort](../../includes/smshort_md.md)] module for Windows PowerShell. For more information about this cmdlet, see [Import\-SCSMManagementPack](http://go.microsoft.com/fwlink/p/?LinkID=225396).

When you reimport a sealed management pack, the version of the new management pack must be greater than the version of the initial management pack. The imported, sealed management pack must pass backward\-compatibility verification, and then the objects of the new management pack and the objects of the initial management pack are merged. When you reimport an unsealed management pack, the objects from the new management pack overwrite the objects from the initial management pack.

If the management pack that you want to import depends on other management packs, multi\-select the dependent management packs and import them in a single operation. [!INCLUDE[smshort](../../includes/smshort_md.md)] will import the management packs in the correct dependency order.

Use the following procedure to import a single management pack, or a management pack bundle \(.mpb file name extension\), by using the [!INCLUDE[smcons](../../includes/smcons_md.md)].

### To import a management pack by using the Service Manager console

1.  In the [!INCLUDE[smcons](../../includes/smcons_md.md)], click **Administration**.

2.  In the **Administration** pane, expand **Administration**, and then click **Management Packs**.

3.  In the **Tasks** pane, under **Management Packs**, click **Import**.

4.  In the **Select Management Packs to Import** dialog box, select the management pack file, and then click **Open**.

5.  In the **Import Management Packs** dialog box, click **Add**.

6.  After you have added all the management packs that you want to import, click **Import**, and then click **OK**.

### To validate the import of a management pack

-   In the [!INCLUDE[smcons](../../includes/smcons_md.md)], select the **Management Packs** view, and ensure that the intended management packs appear in the **Management Packs** list.

![](../../media/pssymbol.png)You can use Windows PowerShell commands to complete these and other related tasks, as follows:

-   For information about how to use Windows PowerShell to import a management pack, see [Import\-SCSMManagementPack](http://go.microsoft.com/fwlink/p/?LinkID=225396).

-   For information about how to use Windows PowerShell to test the validity of a management pack, see [Test\-SCSMManagementPack](http://go.microsoft.com/fwlink/p/?LinkID=225419).

-   For information about how to use Windows PowerShell to retrieve objects that represent management packs that have been imported, see [Get\-SCSMManagementPack](http://go.microsoft.com/fwlink/p/?LinkID=225404).



## How to Import the Operations Manager Alert Cube Management Pack
By default, Service Manager does not automatically import the System Center Alert Management Cube management pack when you register Operations Manager as a data source.

Instead you must manually create a data source for Operations Manager. For more information, see [How to Register the System Center Data Warehouse to Operations Manager](How-to-Register-the-System-Center-Data-Warehouse-to-Operations-Manager.md). Afterward, use the following procedure to import the management pack.

### To import the Operations Manager alert cube management pack

1.  In the [!INCLUDE[smcons](../../includes/smcons_md.md)], click **Data Warehouse**, click **Management Packs**, and confirm that **System Center Datawarehouse Operations Manager Library** is listed.

2.  On the Data Warehouse Management Server, type the following Windows PowerShell commands to manually import the management pack. \(This example assumes that Service Manager is on drive C and that you installed Service Manager using the default path\).

    ```
    cd 'C:\Program Files\Microsoft System Center\Service Manager 2016 R2\PowerShell'
    Import-Module .\System.Center.Service.Manager.psd1
    Import-SCSMManagementPack ..\AlertCube.mpb
    ```

 

