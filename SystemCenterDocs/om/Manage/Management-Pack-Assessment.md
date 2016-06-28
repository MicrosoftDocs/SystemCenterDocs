---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  mgoedtel
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-27
title:  Management Pack Assessment
ms.technology:  operations-manager
ms.assetid:  5e0d9e0d-bb13-4c6e-8d32-901e757eb9fe
---



# Management Pack Assessment

>Applies To: System Center 2016 Technical Preview - Operations Manager


Operations Manager includes a new feature called Updates and Recommendations, to help you proactively identify new technologies or components (i.e. workloads) deployed in your IT infrastructure that were not monitored by Operations Manager or are not monitored using the latest version of a management pack.

>[!NOTE] This feature only works with management packs released by Microsoft, it currently does not support third party management packs.  

If there are Management Packs in the catalog that are designed to monitor those workloads, they will be displayed on the Updates and Recommendations screen. You will also find a list of any updates that are available for Management Packs that are installed in your management group.

When a new workload is deployed in your IT infrastructure that was never monitored by Operations Manager, it will be detected and highlighted under the Updates and Recommendations node.  The management packs required to monitor that workload will be presented with a status of **Not Installed**.  If the necessary management pack files for a particular workload are not installed, for example the library management pack file is installed but not the corresponding discovery and monitoring management pack files, the Updates and Recommendations feature will list that workload with a status of **Partially Installed**.  

This feature includes the following capabilities:
|  Option |  Description  
|----------|-------------
|  **Get MP**  | Installs the management packs for the selected workload
|  **Get All MPs**  |  Installs the management packs for all of the workloads displayed 
|  **View Guide**  |  Downloads the management pack guide from the web browser, for the selected workload, to your computer
|  **View DLC Page**  | Open from the web browser, the page on the Microsoft Download Center, to download the management pack file
|  **More information**  | Highlights all impacted agent-managed systems and management pack details of selected workload (depending on the status of the workload)

>[!NOTE] In order to use the options highlighted in the table above, the computer you are running the Operations console from requires an Internet connection.

>[!NOTE] Configuring the frequency and control the discovery of workloads cannot be performed directly from the Operations console with Technical Preview 5.  If you wish to modify those settings of this feature, you can download a PowerShell script from the [Microsoft Script Center](https://gallery.technet.microsoft.com/scriptcenter/Script-to-modify-settings-246c84af#content).
   
## Importing a Management Pack using Get MP
The following procedure describes how to use the Get MP option to download a management pack for a selected workload.  

1. Log on to the computer with an account that is a member of the Operations Manager Administrators role.

2. In the Operations console, click **Administration**.

3. Click on **Updates and Recommendations**  under **Management Packs**.

4. If a management pack is recommended for either an update or a new installation, select it and click **Get MP** from the **Actions** pane.

5. The **Connecting to Management Pack Catalog Web Service** window appears and after it successfully connects and synchronizes, the **Import Management Packs** wizard opens.

6. On the **Select Management Packs** page, in the list of management packs will be the management packs identified in the **Import Type** column with the value of **Not installed** if missing but applicable, or **Update available** if the management pack file is not the most recent version.
  
   The management pack language matches the default language of the currently installed management pack files.   You can choose to import in another language by clicking on the option **Languages** and in the **Select Languages** dialog box select the appropriate language and then click **OK**.  The **Select Management Packs** page will update the list of management pack files which include the selected languages.
  
7. On the **Select Management Packs** page, the management packs that you selected for import are listed. An icon next to each management pack in the list indicates the status of the selection, as follows:
   - A green check mark indicates that the management pack can be imported. When all management packs in the list display this icon, click **Install**.
   - A yellow information icon indicates that the management pack is dependent on one or more management packs that are not in the **Import** list but are available in the catalog. To add the management pack dependencies to the **Import** list, click **Resolve** in the **Status** column. When the **Dependency Warning** dialog box that appears, click **Resolve**.
   - A red error icon indicates that the management pack is dependent on one or more management packs that are not in the **Import** list and are not available in the catalog. To view the missing management packs, click **Error** in the **Status** column. To remove the management pack with the error from the **Import** list, right-click the management pack, and then click **Remove**.
   
>[!NOTE] When you click **Install**, any management packs in the Install list that display the **Information** or **Error** icon are not imported.

8. The **Import Management Packs** page appears and shows the progress for each management pack. Each management pack is downloaded to a temporary directory, imported to Operations Manager, and then deleted from the temporary directory. If there is a problem at any stage of the import process, select the management pack in the list to view the status details. Click **Close**.

## Importing a Management Pack using Get All MPs
The following procedure describes how to use the Get All MPs option to download management pack for a selected workload.  
1. Log on to the computer with an account that is a member of the Operations Manager Administrators role.

2. In the Operations console, click **Administration**.

3. Click on **Updates and Recommendations** under **Management Packs**.

4. If there are multiple management packs recommended for either an update or a new installation, you can download and import all of them by clicking **Get All MPs** from the **Actions** pane.

5. The **Connecting to Management Pack Catalog Web Service** window appears and after it successfully connects and synchronizes, the **Import Management Packs** wizard opens.

6. On the **Select Management Packs** page, in the list of management packs will be the management packs identified in the **Import Type** column with the value of **Not installed** if missing but applicable, or **Update available** if the management pack file is not the most recent version.
  
7. On the **Select Management Packs** page, the management packs that you selected for import are listed. An icon next to each management pack in the list indicates the status of the selection, as follows:
   - A green check mark indicates that the management pack can be imported. When all management packs in the list display this icon, click **Install**.
   - A yellow information icon indicates that the management pack is dependent on one or more management packs that are not in the **Import** list but are available in the catalog. To add the management pack dependencies to the **Import** list, click **Resolve** in the **Status** column. When the **Dependency Warning** dialog box that appears, click **Resolve**. 
   - A red error icon indicates that the management pack is dependent on one or more management packs that are not in the **Import** list and are not available in the catalog. To view the missing management packs, click **Error** in the **Status** column. To remove the management pack with the error from the **Import** list, right-click the management pack, and then click **Remove**.

>[!NOTE]  When you click **Install**, any management packs in the **Install** list that display the **Information** or **Error** icon are not imported.

8. The **Import Management Packs** page appears and shows the progress for each management pack. Each management pack is downloaded to a temporary directory, imported to Operations Manager, and then deleted from the temporary directory. If there is a problem at any stage of the import process, select the management pack in the list to view the status details. Click **Close**.


