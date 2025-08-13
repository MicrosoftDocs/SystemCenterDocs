---
ms.assetid: b883945e-734a-4b04-a63c-54db9c8cb7d9
title: Create Folders from Web console in System Center Operations Manager
description: This article describes the procedure on how to create folders using Operations Manager web console, and store dashboards inside them.
author: jyothisuri
ms.author: jsuri
ms.date: 04/15/2025
ms.topic: how-to
ms.service: system-center
ms.subservice: operations-manager
MonikerRange: '>=sc-om-2019'
ms.custom: UpdateFrequency2, engagement-fy24
---


# Create folders from Web console

You can create folders using the web console and save the dashboard inside them.

This article describes the procedure on how to create folders using Operations Manager web console, and store dashboards inside them.

::: moniker range="sc-om-2019"

In Operations Manager 2016 and later, you can create a folder and place dashboards/views inside it using the Operations console. However, this feature isn't available from the Web console. With 2019 UR2, using the Web console, you can create folders and place dashboards inside them. These folders can be saved in unsealed management packs.

::: moniker-end

::: moniker range=">=sc-om-2022"

In Operations Manager, you can create a folder and place dashboards/views inside it using the Operations console and Web console. You can also create folders and place dashboards inside them. These folders can be saved in unsealed management packs.

::: moniker-end

> [!NOTE]
> Folders and views created from operations console can be viewed in the web console, but the dashboards created from the web console won't be visible in the operations console.

## Create a folder

To create a folder, follow these steps:

1. Open the web console and navigate to **Monitoring**.
2. Select **New dashboard**. This opens a right panel like before where **Monitoring** is selected by default.

   ![Screenshot of New dashboard.](./media/support-for-folders/new-dashboard.png)

3. Select the management pack where you want to save this new folder from the dropdown menu. For example, currently **Client monitoring overrides management pack** is selected.
4. Select **New folder**, and enter the name of the new folder. For example, **Folder\_in\_client** as shown in the below image:

   ![Screenshot of Monitoring.](./media/support-for-folders/create-in-monitoring.png)

5. Select **OK**.

   The new folder is saved in the selected management pack, and displays in the list of folders.

   ![Screenshot of Create folder.](./media/support-for-folders/create-folder-in-client.png)

> [!NOTE]
> - You can save a folder inside a preexisting folder. To do this, select the desired folder instead of Monitoring, and follow the same procedure mentioned above.
> - These folders can be deleted from the operations console.

## Save a dashboard inside a folder

To save a dashboard inside a folder, follow these steps:

1. Open the web console and navigate to **Monitoring**.
2. Select **New dashboard**.
3. Enter the name of the dashboard.
4. Select the folder from the list where you want to store the dashboard.
   Management pack selection will be based on root folder.
5. Select **Save**.
   The dashboard is stored inside the selected folder and can be seen in the left navigation pane.

   ![Screenshot of save dashboard.](./media/support-for-folders/new-dashboard-folder-in-client.png)

   > [!NOTE]
   > You can create a dashboard at the root monitoring level as before by not selecting any folder and selecting the monitoring root.

## Create folders in Web console using REST API

To create folders in Web console using REST API, follow these steps:

You can use the following REST APIs to create folders in Web console and save dashboards inside them.

> [!NOTE]
> This feature is applicable to System Center Operations Manager 2019 UR2 and later versions.

**Data/monitoringTreeForRootFolders**

- Data/monitoringTreeForRootfolders is a GET request that returns all the folders stored in unsealed management packs inside which users can store dashboards and folders. The output of this request can be used for below POST requests.

**monitoring/folder**

- Request of type POST to create a new folder inside a management pack.

    Parameters required:

    | Name | Type  | Definition |
    |----|---|------|
    |  path  | string  |Name of the new folder. |
    | mpId|string| ID of the management pack where you want to create the new folder.  |

- Request of type POST to create a new folder inside a pre-existing folder

    Parameters required:

    | Name | Type  | Definition |
    |----|---|------|
    |  component ID  | string  |Folder ID of the parent where you want to store the new folder. |
    | path|string| Name of the new folder.  |

**monitoring/dashboard/**

- Request of type POST to save a dashboard inside a new folder.

     Parameters required:

     | Name | Type  | Definition |
     |----|------|-----|
     |  name | string  |Name of the new dashboard. |
     | path|string| Folder ID where you want to save the new dashboard.  |

- Request of type POST to save a dashboard inside the root monitoring.

     Parameters required:

     | Name | Type  | Definition |
     |----|----|-----|
     |  mpId  | string  |ID of the management pack where you want to store the dashboard. |
     | name |string| Name of the new dashboard.  |

## Next Steps

- [Standard views in management pack](manage-console-standard-views.md).
- [Scope the views in management packs](manage-console-scope-views.md).
- [Data - Retrieve Items in Monitoring Tree View](/rest/api/operationsmanager/data/retrieve%20items%20in%20monitoring%20tree%20view).
- [Component - Add Dashboard](/rest/api/operationsmanager/monitoring/add-dashboard).
