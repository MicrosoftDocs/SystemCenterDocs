---
title: Use management packs
description: You use management packs to add functionality to Service Manager.
ms.topic: article
author: jyothisuri
ms.author: jsuri
ms.service: system-center
keywords:
ms.date: 11/01/2024
ms.subservice: service-manager
ms.assetid: 3c42925f-74f3-4c18-934e-8d1cd2edaa3b
ms.custom: UpdateFrequency3, engagement-fy24
---

# Use management packs to add functionality to Service Manager



There are two types of management packs: sealed management packs and unsealed management packs. A sealed management pack can't be modified, but an unsealed management pack can be modified.

Unsealed management packs are used to extend Service Manager with the information that you must have to implement all or part of a service management process. You can use unsealed management packs to store the custom objects that you create. For example, you can store the objects you create during your testing or evaluation process in an unsealed management pack. Then, you can export that unsealed management pack to a file and then import the file to another environment, such as a production environment. You can also import the same management pack into multiple environments to ensure configuration consistency across Service Manager deployments and to increase efficiency.

> [!NOTE]
> Only unsealed management packs can be reimported.

An unsealed management pack is an .xml file that contains classes, workflows, views, forms, reports, and knowledge articles. Items such as groups, queues, tasks, templates, connectors, and list items are stored in a management pack, but items such as incidents, change requests, computers, and other instances of classes aren't stored in a management pack.

By default, Service Manager contains several pre-imported, sealed management packs that enable core Service Manager features, such as incident management and change management. Also, by default, Service Manager contains the **Default Management Pack** management pack, in which you can store new items that you create. Additionally, Service Manager contains several pre-imported, unsealed management packs that enable optional features. You can delete unsealed management packs, which might result in the loss of some views, rules, or lists. However, the removal of these optional features won't prevent Service Manager from functioning. You should consider exporting a management pack before you delete it. You can import the management pack later if you need the optional features in a management pack that you deleted.

To use a management pack, import it into Service Manager. The management pack is stored in a .xml, .mp, or a .mpb file that you can import by using the Service Manager console.

For more information about management packs key concepts, management packs best practices, and other management pack related articles, see [Management Packs: Working with Management Packs](/previous-versions/system-center/system-center-2012-R2/hh519661(v=sc.12)).

## Create a management pack file

You can use the following procedures to create a management pack file in Service Manager. After you create the management pack file, you can use it to store objects that you create.

For more information about how to create and customize management packs, see [Management Packs: Working with Management Packs](/previous-versions/system-center/system-center-2012-R2/hh519661(v=sc.12)).

1. In the Service Manager console, select **Administration**.

2. In the **Administration** pane, expand **Administration**, and select **Management Packs**.

3. In the **Tasks** pane, under **Management Packs**, select **Create Management Pack**.

4. In the **Create Management Pack** dialog, enter a name, such as **Sample Management Pack**, and then enter a description for the new management pack. Select **OK**.

### Validate the creation of a management pack file

- In the Service Manager console, open the **Management Packs** view, and verify that the new management pack appears in the **Management Packs** pane.

![PowerShell symbol](./media/management-packs/pssymbol.png)You can use Windows PowerShell commands to complete these tasks, as follows:

- For information about how to use Windows PowerShell to create a new management pack, see [New-SCSMManagementPack](/previous-versions/system-center/powershell/system-center-2012-r2/hh316283(v=sc.20)).

- For information about how to use Windows PowerShell to seal a management pack, preventing it from being modified, see [Protect-SCSMManagementPack](/previous-versions/system-center/powershell/system-center-2012-r2/hh316266(v=sc.20)).

- For information about how to use Windows PowerShell to remove management packs, see [Remove-SCSMManagementPack](/previous-versions/system-center/powershell/system-center-2012-r2/hh316264(v=sc.20)).

## Export a management pack

After you create a management pack in Service Manager, you can export the unsealed management pack as a file to back up any customizations in the management pack. The exported management pack is a valid XML-formatted file. After you export an unsealed management pack, you can later import it to restore the objects that the management pack contains.

When you export a sealed management pack, from the Service Manager console or by using the Windows PowerShell cmdlet [Export-SCSMManagementPack](/previous-versions/system-center/powershell/system-center-2012-r2/hh316281(v=sc.20)), Service Manager generates an equivalent, unsealed management pack and stores it as a .XML file on the hard drive. You can then edit this management pack file to increase the version of the management pack, and reseal it so it can be reimported into Service Manager.

Use the following procedures to export an unsealed management pack and then validate the export.

To export a management pack, follow these steps:

1. In the Service Manager console, select **Administration**.

2. In the **Administration** pane, expand **Administration**, and select **Management Packs**.

3. In the **Management Packs** pane, select the management pack that you want to export.

4. In the **Tasks** pane, under the name of the management pack that you want to export, select **Export**.

5. In the **Browse For Folder** dialog, select a location for the file, and select **OK**.

    > [!NOTE]
    > You can't change the default name of the management pack file.

### Validate the export of a management pack

- In Windows Explorer, ensure that you can locate the management pack file.

![PowerShell symbol](./media/management-packs/pssymbol.png)You can use Windows PowerShell commands to complete this task. For information about how to use Windows PowerShell to export a management pack as a valid XML-formatted file that you can later import into Service Manager or Operations Manager, see [Export-SCSMManagementPack](/previous-versions/system-center/powershell/system-center-2012-r2/hh316281(v=sc.20)).

## Import a management pack

Before you can use a management pack in Service Manager, you must import the management pack by using one of the following methods:

- Use the Service Manager console, as described in this article.

- Use the **Import-SCSMManagementPack** cmdlet from the Service Manager module for Windows PowerShell. For more information about this cmdlet, see [Import-SCSMManagementPack](/previous-versions/system-center/powershell/system-center-2012-r2/hh316284(v=sc.20)).

When you reimport a sealed management pack, the version of the new management pack must be greater than the version of the initial management pack. The imported, sealed management pack must pass backward-compatibility verification, and then the objects of the new management pack and the objects of the initial management pack are merged. When you reimport an unsealed management pack, the objects from the new management pack overwrite the objects from the initial management pack.

If the management pack that you want to import depends on other management packs, multi-select the dependent management packs and import them in a single operation. Service Manager will import the management packs in the correct dependency order.

Use the following procedure to import a single management pack, or a management pack bundle (.mpb file name extension), by using the Service Manager console.

### Import a management pack by using the Service Manager console

1. In the Service Manager console, select **Administration**.

2. In the **Administration** pane, expand **Administration**, and select **Management Packs**.

3. In the **Tasks** pane, under **Management Packs**, select **Import**.

4. In the **Select Management Packs to Import** dialog, select the management pack file, and select **Open**.

5. In the **Import Management Packs** dialog, select **Add**.

6. After you've added all the management packs that you want to import, select **Import**, and select **OK**.

### Validate the import of a management pack

- In the Service Manager console, select the **Management Packs** view, and ensure that the intended management packs appear in the **Management Packs** list.

![PowerShell symbol](./media/management-packs/pssymbol.png)You can use Windows PowerShell commands to complete these and other related tasks, as follows:

- For information about how to use Windows PowerShell to import a management pack, see [Import-SCSMManagementPack](/previous-versions/system-center/powershell/system-center-2012-r2/hh316284(v=sc.20)).

- For information about how to use Windows PowerShell to test the validity of a management pack, see [Test-SCSMManagementPack](/previous-versions/system-center/powershell/system-center-2012-r2/hh316272(v=sc.20)).

- For information about how to use Windows PowerShell to retrieve objects that represent management packs that have been imported, see [Get-SCSMManagementPack](/previous-versions/system-center/powershell/system-center-2012-r2/hh316260(v=sc.20)).

## Import the Operations Manager Alert Cube Management Pack

By default, Service Manager doesn't automatically import the System Center Alert Management Cube management pack when you register Operations Manager as a data source.

Instead, you must manually create a data source for Operations Manager. For more information, see [How to Register the System Center Data Warehouse to Operations Manager](register-sources-to-dw.md). Afterward, use the following procedure to import the management pack.

To import the Operations Manager alert cube management pack, do the following:

1. In the Service Manager console, select **Data Warehouse**, select **Management Packs**, and confirm that **System Center Datawarehouse Operations Manager Library** is listed.

2. On the Data Warehouse Management Server, enter the following Windows PowerShell commands to manually import the management pack. (This example assumes that Service Manager is on drive C and that you installed Service Manager using the default path).

    ```powershell
    cd 'C:\Program Files\Microsoft System Center\Service Manager 2016 R2\PowerShell'
    Import-Module .\System.Center.Service.Manager.psd1
    Import-SCSMManagementPack ..\AlertCube.mpb
    ```

## Next steps

- [Use connectors to import data](import-data-connectors.md) into Service Manager.
