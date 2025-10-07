---
ms.assetid: 0cff3a49-a490-4dd4-aa29-f6c9214c5d92
title: Import, Export, and Remove an Operations Manager Management Pack
description: This article describes how to import, export and remove an Operations Manager management pack from the management group.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 08/07/2025
ms.custom: engagement-fy23
ms.service: system-center
ms.subservice: operations-manager
ms.topic: concept-article
---

# Import, export, and remove an Operations Manager management pack

There are numerous management packs available for System Center Operations Manager. A management pack must be installed for use by Operations Manager to discover and monitor one or more components depending on its complexity, and the overall health of the IT service delivered by the organization. Over time, the knowledge of what to discover and monitor, and how to monitor and report on the operational data is updated in newer releases of a management pack.  These management packs must be reimported into the management group when updated by the vendor or internally if developed by the team responsible for it.  When the management pack is no longer required to monitor, you can remove it from the management group.

::: moniker range="sc-om-2019"
>[!NOTE]
> With Operations Manager 2019 UR2, you can track the changes made in management packs. [Learn more](management-pack-change-tracking.md).

::: moniker-end

::: moniker range="sc-om-2022"
>[!NOTE]
> You can track the changes made in management packs. [Learn more](management-pack-change-tracking.md).

::: moniker-end

## Importing a management pack

You have several options for importing management packs:

-   Import a management pack from the Microsoft Catalog by using the Operations console.

-   Import a management pack from disk (local storage or a network file share) by using the Operations console.

-   Download a management pack by using the Operations console to import at a later time.

-   Download a management pack by using an Internet browser to import at a later time.

> [!NOTE]
> Using the management pack catalog service requires an Internet connection and your firewall needs to allow access to the the following URL: `https://www.microsoft.com/mpdownload/ManagementPackCatalogWebService.asmx`. If the computer running Operations Manager Operations console can't connect to the Internet, use another computer to download the management pack, and then copy the files to a shared folder that's accessible from the console.

The Operations Manager community maintains a [list of management packs](/system-center/scom/management-pack-list?view=sc-om-2025&preserve-view=true). You can obtain third-party management packs directly from those companies and import them by following the procedure [Import a management pack from disk](#import-a-management-pack-from-disk).

> [!NOTE]
> Microsoft neither endorses nor provides support for third-party products. Please contact the specific provider for support issues.

You should always review the management pack guide before you import a management pack.

### Import a management pack from the web catalog

> [!IMPORTANT]
> If you receive errors connecting to the management pack web catalog, ensure that .NET is utilizing StrongCrypto settings to communicate with the web service. More information and steps to apply this can be found here: [Transport Layer Security (TLS) best practices with the .NET Framework](/dotnet/framework/network-programming/tls)

1.  Sign in to the computer with an account that is a member of the Operations Manager Administrators role.

2.  In the Operations console, select **Administration**.

3.  Right-click **Management Packs**, and select **Import Management Packs**.

4.  The **Import Management Packs** wizard opens. Select **Add**, and select **Add from catalog**.

    The **Select Management Packs from Catalog** dialog opens. The default view lists all management packs in the catalog. You can change the view to show the following management packs:

    -   Updates available for management packs that are already imported on this computer

    -   All management packs that have been released within the last three months

    -   All management packs that have been released within the last six months

    You can also use the **Find** field to search for a specific management pack in the catalog.

5.  In the list of management packs, select the management pack that you want to import, select **Select**, and select **Add**.

    In the list of management packs, you can select a product, or expand the product name to select a specific version, or expand the product version to select a specific management pack file. For example, you can select **SQL Server** for all SQL Server management packs, or you can expand **SQL Server** and select **SQL Server 2014** for all SQL Server 2014 management packs, or you can expand **SQL Server 2014** and select **SQL Server Core Library Management Pack**.

    > [!NOTE]
    > When a management pack is labeled “(Online Catalog Only)”, you can't import the management pack directly from the catalog. You must download the .msi and import from disk.

6.  On the **Select Management Packs** page, the management packs that you selected for import are listed. An icon next to each management pack in the list indicates the status of the selection, as follows:

    -   A green check mark indicates that the management pack can be imported. When all management packs in the list display this icon, select **Import**.

    -   A yellow information icon indicates that the management pack is dependent on one or more management packs that aren't in the **Import** list but are available in the catalog. To add the management pack dependencies to the **Import** list, select **Resolve** in the **Status** column. In the **Dependency Warning** dialog that appears, select **Resolve**.

    -   A red error icon indicates that the management pack is dependent on one or more management packs that aren't in the **Import** list and aren't available in the catalog. To view the missing management packs, select **Error** in the **Status** column. To remove the management pack with the error from the **Import** list, right-click the management pack, and select **Remove**.

    > [!NOTE]
    > When you select **Import**, any management packs in the **Import** list that display the Information or Error icon aren't imported.

7.  The **Import Management Packs** page appears and shows the progress for each management pack. Each management pack is downloaded to a temporary directory, imported to Operations Manager, and then deleted from the temporary directory. If there's a problem at any stage of the import process, select the management pack in the list to view the status details. Select **Close**.


### Import a management pack from disk

1.  Sign in to the computer with an account that's a member of the Operations Manager Administrators role.

2.  In the Operations console, select **Administration**.

3.  Right-click **Management Packs**, and select **Import Management Packs**.

4.  The **Import Management Packs** wizard opens. Select **Add**, and then select **Add from disk**.

5.  The **Select Management Packs to import** dialog appears. If necessary, change to the directory that holds your management pack file. Select one or more management packs to import from that directory, and select **Open**.

6.  On the **Select Management Packs** page, the management packs that you selected for import are listed. An icon next to each management pack in the list indicates the status of the selection as follows:

    -   A green check mark indicates that the management pack can be imported. When all the management packs in the list display this icon, select **Import**.

    -   A red error icon indicates that the management pack is dependent on one or more management packs that aren't in the **Import** list and aren't available in the catalog. To view the missing management packs, select **Error** in the **Status** column. To remove the management pack with the error from the **Import** list, right-click the management pack, and select **Remove**.

    > [!NOTE]
    > When you select **Import**, any management packs in the **Import** list that display the Error icon aren't imported.

7.  The **Import Management Packs** page appears and shows the progress for each management pack. Each management pack is downloaded to a temporary directory, imported to Operations Manager, and then deleted from the temporary directory. If there's a problem at any stage of the import process, select the management pack in the list to view the status details. Select **Close**.


### Download a management pack by using the Operations console

1.  Sign in to the computer with an account that's a member of the Operations Manager Administrators role.

2.  In the Operations console, select **Administration**.

3.  Right-click **Management Packs**, and select **Download Management Packs**.

4.  The **Download Management Packs** wizard opens. Select **Add**.

    The **Select Management Packs from Catalog** dialog opens. The default view lists all management packs in the catalog. You can change the view to show the following management packs:

    -   Updates available for management packs that are already imported on this computer

    -   All management packs that have been released within the last three months

    -   All management packs that have been released within the last six months

    You can also use the **Find** field to search for a specific management pack in the catalog.

5.  In the list of management packs, select the management pack that you want to import, select **Select**, and select **Add**.

    In the list of management packs, you can select a product, or expand the product name to select a specific version, or expand the product version to select a specific management pack file. For example, you can select **SQL Server** for all SQL Server management packs, or you can expand **SQL Server** and select **SQL Server 2005** for all SQL Server 2005 management packs, or you can expand **SQL Server 2005** and select **SQL Server Core Library Management Pack**.

6.  The selected management packs are displayed in the **Download** list. In the **Download management packs to this folder** field, enter the path where the management packs should be saved, and select **Download**.

7.  The **Download Management Packs** page appears and shows the progress for each management pack. If there's a problem with the download, select the management pack in the list to view the status details. Select **Close**.

### Download a management pack by using an Internet browser

1.  Open a browser and go to the [Microsoft Management Pack List](https://go.microsoft.com/fwlink/?LinkId=82105).

2.  Browse the list of management packs to locate the management pack that you want to download.

3.  Select the name of the management pack that you want to download.

4.  On the Microsoft Download Center page for the management pack, select **Download**.

5.  In the **File Download** dialog, select **Run** to download and extract the management pack files. Or, select **Save** to download the .msi file without extracting the files.

    > [!NOTE]
    > Some management pack download pages contain a download link for the management pack .msi file and a download link for the management pack guide. Download both the .msi and the guide.
    >
    > Before you can import the management pack in Operations Manager, you must run the .msi file to extract the files.

## How to export an Operations Manager management pack

Exporting a management pack allows customizations to a sealed management pack to be saved to a writeable management pack. Because sealed management packs can't be changed, the modifications made to a management pack are saved to a separate, unsealed management pack file. The unsealed management pack can then be imported into a different management group or the same management group depending on the situation. This unsealed management pack is dependent on the original sealed management pack and can be imported only to management groups that have the original sealed management pack.  

> [!NOTE]
> Using the Operations Console, you can only export unsealed management packs. To export a sealed management pack, you must use the Export-SCManagementPack cmdlet. Know that this will break the seal on the MP, and it cannot be used the same as it was before unless resealed. For more information, see [Operations Manager Cmdlet Reference](/powershell/module/operationsmanager/export-scmanagementpack).  
### To export an unsealed management pack   

1.  Sign in to the computer with an account that's a member of the Operations Manager Administrators role.  

2.  In the Operations console, select **Administration**.  

3.  In **Administration**, select **Management Packs** to display the list of imported management packs.  

4.  In the **Management Packs** pane, right\-click the management pack you want to export, and select **Export Management Pack**.  

5.  In the **Browse For Folder** dialog, expand the path for the location to save the file, and select **OK**.  

    The management pack is saved as an Operations Manager XML management pack file and is ready for importing into another management group.  

## How to Remove an Operations Manager Management Pack

When you no longer need a management pack, you can delete it using the Operations console. When you delete a management pack, all the settings and thresholds associated with it are removed from the management group. Also, the .mp or .xml file for that management pack is deleted from the hard disk of the management server. You can delete a management pack only if you've first deleted the dependent management packs.  

### To remove a management pack  

1.  Sign in to the computer with an account that's a member of the Operations Manager Administrators role.  

2.  In the Operations console, select **Administration**.  

3.  In **Administration**, select **Management Packs.**  

4.  In the **Management Packs** pane, right\-click the management pack you would like to remove and select **Delete**.  

5.  On the message stating that deleting the management pack might affect the scoping of some user roles, select **Yes**.  

> [!NOTE]  
> If any other imported management packs depend on the management pack you're trying to remove, the **Dependent Management Packs** error message is displayed. You must remove the dependent management packs before you can continue.  

## Next steps

- To learn how to create a custom writeable management pack to store your overrides, see [How to Create a Management Pack for Overrides](manage-mp-create-unsealed-mp.md).

- If you want to create your own custom knowledge for specific alerts generated by rules or monitors from a sealed management pack, review [How to Add Knowledge to a Management Pack](manage-mp-add-knowledge.md).

- To understand the basic concepts for managing the monitoring configuration of an application or service defined in a management pack, see [Management Pack Lifecycle](manage-mp-lifecycle.md).
