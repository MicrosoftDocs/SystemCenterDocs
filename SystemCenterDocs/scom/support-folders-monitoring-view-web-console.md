---
ms.assetid: b883945e-734a-4b04-a63c-54db9c8cb7d9
title: Create folders from web console in System Center Operations Manager
description: This article describes the procedure on how to create folders using Operations Manager web console, and store dashboards inside them.
author: JYOTHIRMAISURI
ms.author: V-jysur
manager: vvithal
ms.date: 06/15/2020
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
MonikerRange: 'sc-om-2019'
---


# Create folders from Web console

You can create folders using the web console and save the dashboard inside them.

In Operations Manager 2016 and later, you can create a folder and place dashboards/views inside it using the Operations console. However, this feature is not available from the Web console. With 2019 UR2, using the web console, you can create folders and place dashboards inside them. These folders can be saved in unsealed management packs.

> [!NOTE]
> Folders and views created from operations console can be viewed in the web console but the dashboards created from the web console will not be visible in the operations console.


## Create a new folder

Use the following steps:

1. Open the web console and navigate to **Monitoring**.
2. Click **New dashboard**. This opens a right panel like before where **Monitoring** is selected by default.

   ![New dashboard](./media/support-for-folders/new-dashboard.png)

3. Select the management pack where you want to save this new folder from the drop-down menu. For e.g. currently, **Client monitoring overrides management pack** is selected.
4. Click **New folder** and enter the name of the new folder. For example, **Folder\_in\_client** as shown in the below image:

   ![Monitoring](./media/support-for-folders/create-in-monitoring.png)

5. Click **OK**.

   The new folder is saved in the selected management pack, and displays in the list of folders.

   ![Create folder](./media/support-for-folders/create-folder-in-client.png)

> [!NOTE]
> - You can save a folder inside a preexisting folder. To do this, select the desired folder instead of Monitoring, and follow the same procedure mentioned above.
> - These folders can be deleted from the operations console.


## Save a dashboard inside a folder

1. Open the web console and navigate to **Monitoring**.
2. Click **New dashboard**.
3. Enter the name of the dashboard.
4. Select the folder from the list where you want to store the dashboard.
   Management pack selection will be based on root folder.
6. Click **Save**.
   The dashboard is stored inside the selected folder, and can be seen in the left navigation pane.

   ![New dashboard](./media/support-for-folders/new-dashboard-folder-in-client.png)

   > [!NOTE]
   >  You can create a dashboard at the root monitoring level as before, by not selecting any folder and clicking the monitoring root.

> [!NOTE]
> This reference of the Representational State Transfer (REST) API is applicable to System Center Operations Manager 2019 UR2 and later versions.

**Data/monitoringTreeForRootFolders**

  - Data/monitoringTreeForRootfolders is a GET request that returns all the folders stored in unsealed management packs inside which users can store dashboards and folders.

All the data required in the calls mentioned below are obtained from this endpoint. All the calls mentioned below are POST requests.


**monitoring/folder**

  - Create a new folder inside a management pack.

      Parameters required:

      | Name | Type  | Definition |
      |----|---|------|
      |  path  | string  |Name of the new folder. |
      | mpId|string| Id of the management pack where you want to create the new folder.  |

  - Create a new folder inside a pre-existing folder

      Parameters required:

      | Name | Type  | Definition |
      |----|---|------|
      |  componentId  | string  |Folder id of the parent where you want to store the new folder. |
      | path|string| Name of the new folder.  |

**monitoring/dashboard/**

  - Save a dashboard inside a new folder.

     Parameters required:

     | Name | Type  | Definition |
     |----|------|-----|
     |  name | string  |Name of the new dashboard. |
     | path|string| Folder id where you want to save the new dashboard.  |


  - Save a dashboard inside the root monitoring.

     Parameters required:

     | Name | Type  | Definition |
     |----|----|-----|
     |  mpId  | string  |Id of the management pack where you want to store the dashboard. |
     | name |string| Name of the new dashboard.  |


## Next Steps
- [See standard views in management pack](manage-console-standard-views.md)

- [Scope the views in management packs](manage-console-scope-views.md)

- [Data Retrieve Items In Monitoring Tree View](https://docs.microsoft.com/rest/api/operationsmanager/data/retrieve%20items%20in%20monitoring%20tree%20view)

- [Component - Add Dashboard](https://docs.microsoft.com/rest/api/operationsmanager/component/add%20dashboard)
