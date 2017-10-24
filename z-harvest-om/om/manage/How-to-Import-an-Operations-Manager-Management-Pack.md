---
title: How to Import an Operations Manager Management Pack
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3b7bba9a-04b2-412f-9421-8d702c3ca462
author:mgoedtel
manager:cfreemanwa
---
# How to Import an Operations Manager Management Pack
There are numerous management packs available for [!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)]. You have several options for importing management packs:  
  
-   Import directly from the catalog on the [Microsoft Pinpoint Site](https://go.microsoft.com/fwlink/?LinkId=82105) by using the Operations console.  
  
-   Import from disk \(local storage or a network file share\) by using the Operations console.  
  
-   Use the Operations console to download a management pack from the catalog to import at a later time.  
  
-   Use an Internet browser to download a management pack from the catalog to import at a later time.  
  
> [!NOTE]  
> Using the management pack catalog service requires an Internet connection. If the computer running Operations Manager cannot be connected to the Internet, use another computer to download the management pack, and then copy the files to a shared folder that is accessible to the Operations Manager management server.  
  
The catalog on the [Microsoft Pinpoint Site](https://go.microsoft.com/fwlink/?LinkId=82105) contains management packs not developed by Microsoft. You can obtain management packs directly from these  companies and import them by using the procedure to import from disk. You can also search for management packs created by the community.  
  
The Operations Manager community also maintains a list of Management Packs developed by Microsoft  on the following web site [Microsoft Management Pack list](https://social.technet.microsoft.com/wiki/contents/articles/16174.microsoft-management-packs.aspx)  
  
> [!NOTE]  
> Microsoft neither endorses nor provides support for third\-party products. Please contact the specific provider for support issues.  
  
You should always review the management pack guide before you import a management pack.  
  
### To import a management pack from the catalog  
  
1.  Log on to the computer with an account that is a member of the Operations Manager Administrators role.  
  
2.  In the Operations console, click **Administration**.  
  
3.  Right\-click **Management Packs**, and then click **Import Management Packs**.  
  
4.  The **Import Management Packs** wizard opens. Click **Add**, and then click **Add from catalog**.  
  
    The **Select Management Packs from Catalog** dialog box opens. The default view lists all management packs in the catalog. You can change the view to show the following management packs:  
  
    -   Updates available for management packs that are already imported on this computer  
  
    -   All management packs that have been released within the last three months  
  
    -   All management packs that have been released within the last six months  
  
    You can also use the **Find** field to search for a specific management pack in the catalog.  
  
5.  In the list of management packs, select the management pack that you want to import, click **Select**, and then click **Add**.  
  
    In the list of management packs, you can select a product, or expand the product name to select a specific version, or expand the product version to select a specific management pack file. For example, you can select **SQL Server** for all SQL Server management packs, or you can expand **SQL Server** and select **SQL Server&nbsp;2005** for all SQL Server&nbsp;2005 management packs, or you can expand **SQL Server&nbsp;2005** and select **SQL Server Core Library Management Pack**.  
  
    > [!NOTE]  
    > When a management pack is labeled "\(Online Catalog Only\)", you cannot import the management pack directly from the catalog. You must download the .msi and import from disk.  
  
6.  On the **Select Management Packs** page, the management packs that you selected for import are listed. An icon next to each management pack in the list indicates the status of the selection, as follows:  
  
    -   A green check mark indicates that the management pack can be imported. When all management packs in the list display this icon, click **Import**.  
  
    -   A yellow information icon indicates that the management pack is dependent on one or more management packs that are not in the **Import** list but are available in the catalog. To add the management pack dependencies to the **Import** list, click **Resolve** in the **Status** column. In the **Dependency Warning** dialog box that appears, click **Resolve**.  
  
    -   A red error icon indicates that the management pack is dependent on one or more management packs that are not in the **Import** list and are not available in the catalog. To view the missing management packs, click **Error** in the **Status** column. To remove the management pack with the error from the **Import** list, right\-click the management pack, and then click **Remove**.  
  
    > [!NOTE]  
    > When you click **Import**, any management packs in the **Import** list that display the Information or Error icon are not imported.  
  
7.  The **Import Management Packs** page appears and shows the progress for each management pack. Each management pack is downloaded to a temporary directory, imported to Operations Manager, and then deleted from the temporary directory. If there is a problem at any stage of the import process, select the management pack in the list to view the status details. Click **Close**.  
  
> [!NOTE]  
> When you import a management pack that contains binary files \(.mpb\), you must recycle the OperationsManager application pool in Internet Information Services \(IIS\) Manager.  
  
### To import a management pack from disk  
  
1.  Log on to the computer with an account that is a member of the Operations Manager Administrators role.  
  
2.  In the Operations console, click **Administration**.  
  
3.  Right\-click **Management Packs**, and then click **Import Management Packs**.  
  
4.  The **Import Management Packs** wizard opens. Click **Add**, and then click **Add from disk**.  
  
5.  The **Select Management Packs to import** dialog box appears. If necessary, change to the directory that holds your management pack file. Click one or more management packs to import from that directory, and then click **Open**.  
  
6.  On the **Select Management Packs** page, the management packs that you selected for import are listed. An icon next to each management pack in the list indicates the status of the selection, as follows:  
  
    -   A green check mark indicates that the management pack can be imported. When all management packs in the list display this icon, click **Import**.  
  
    -   A red error icon indicates that the management pack is dependent on one or more management packs that are not in the **Import** list and are not available in the catalog. To view the missing management packs, click **Error** in the **Status** column. To remove the management pack with the error from the **Import** list, right\-click the management pack, and then click **Remove**.  
  
    > [!NOTE]  
    > When you click **Import**, any management packs in the **Import** list that display the Error icon are not imported.  
  
7.  The **Import Management Packs** page appears and shows the progress for each management pack. Each management pack is downloaded to a temporary directory, imported to Operations Manager, and then deleted from the temporary directory. If there is a problem at any stage of the import process, select the management pack in the list to view the status details. Click **Close**.  
  
> [!NOTE]  
> When you import a management pack that contains binary files \(.mpb\), you must recycle the OperationsManager application pool in Internet Information Services \(IIS\) Manager.  
  
### To download a management pack by using the Operations console  
  
1.  Log on to the computer with an account that is a member of the Operations Manager Administrators role.  
  
2.  In the Operations console, click **Administration**.  
  
3.  Right\-click **Management Packs**, and then click **Download Management Packs**.  
  
4.  The **Download Management Packs** wizard opens. Click **Add**.  
  
    The **Select Management Packs from Catalog** dialog box opens. The default view lists all management packs in the catalog. You can change the view to show the following management packs:  
  
    -   Updates available for management packs that are already imported on this computer  
  
    -   All management packs that have been released within the last three months  
  
    -   All management packs that have been released within the last six months  
  
    You can also use the **Find** field to search for a specific management pack in the catalog.  
  
5.  In the list of management packs, select the management pack that you want to import, click **Select**, and then click **Add**.  
  
    In the list of management packs, you can select a product, or expand the product name to select a specific version, or expand the product version to select a specific management pack file. For example, you can select **SQL Server** for all SQL Server management packs, or you can expand **SQL Server** and select **SQL Server&nbsp;2005** for all SQL Server&nbsp;2005 management packs, or you can expand **SQL Server&nbsp;2005** and select **SQL Server Core Library Management Pack**.  
  
6.  The selected management packs are displayed in the **Download** list. In the **Download management packs to this folder** field, enter the path where the management packs should be saved, and then click **Download**.  
  
7.  The **Download Management Packs** page appears and shows the progress for each management pack. If there is a problem with a download, select the management pack in the list to view the status details. Click **Close**.  
  
### To download a management pack by using an Internet browser  
  
1.  Open a browser and go to the catalog on the  [Microsoft Pinpoint Site](https://go.microsoft.com/fwlink/?LinkId=82105).  
  
2.  Browse the list of management packs, or use the **Search Applications** field to locate the management pack that you want to download.  
  
3.  Click the name of the management pack that you want to download.  
  
4.  On the details page for the management pack, click **Download**.  
  
5.  On the management pack download page, click **Download**.  
  
    > [!NOTE]  
    > Some management pack download pages contain a download link for the management pack .msi file and a download link for the management pack guide. Download both the .msi and the guide.  
  
6.  In the **File Download** dialog box, click **Run** to download and extract the management pack files. Or, click **Save** to download the .msi file without extracting the files.  
  
    > [!NOTE]  
    > Before you can import the management pack in Operations Manager, you must run the .msi file to extract the files.  
  
## See Also  
[Creating a Management Pack for Overrides](../../om/manage/Creating-a-Management-Pack-for-Overrides.md)  
[Management Packs Installed with Operations Manager](../../om/manage/Management-Packs-Installed-with-Operations-Manager.md)  
[What Is in an Operations Manager Management Pack?](../../om/manage/What-Is-in-an-Operations-Manager-Management-Pack-.md)  
[Management Pack Life Cycle](../../om/manage/Management-Pack-Life-Cycle.md)  
[How to Remove an Operations Manager Management Pack](../../om/manage/How-to-Remove-an-Operations-Manager-Management-Pack.md)  
[How to Export an Operations Manager Management Pack](../../om/manage/How-to-Export-an-Operations-Manager-Management-Pack.md)  
[How to Add Knowledge to a Management Pack](../../om/manage/How-to-Add-Knowledge-to-a-Management-Pack.md)  
  
