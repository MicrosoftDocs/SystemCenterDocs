---
title: Using My Workspace in Operations Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 91b1dd4c-6ce2-442b-826f-21a265ed3ac7
---
# Using My Workspace in Operations Manager
My Workspace provides you with a private area in the Operations console that you can customize for your specific needs.  Using My Workspace, you can create folders to organize the workspace, add shortcuts to favorite views, save useful searches, and create views that are only visible to you. Your configuration of My Workspace will be available to you in any Operations console that you log in to using the same Windows credentials.

This topic contains the following procedures:

-   [Create Folders in My Workspace](Using-My-Workspace-in-Operations-Manager.md#bkmk_createfoldersinmyworkspace)

-   [Add Shortcuts to Views](Using-My-Workspace-in-Operations-Manager.md#BKMK_AddShortcutstoViews)

-   [Save Searches](Using-My-Workspace-in-Operations-Manager.md#bkmk_savesearches)

-   [Create Views](Using-My-Workspace-in-Operations-Manager.md#bkmk_createviews)

## <a name="bkmk_createfoldersinmyworkspace"></a>Create Folders in My Workspace
My Workspace contains two default folders: **Favorite Views** and **Saved Searches**. You can create additional folders to better organize your workspace. All new folders that you create will be created under **Favorite Views**.

#### To create a new folder in My Workspace

1.  Right\-click in the navigation pane.

    > [!NOTE]
    > To create a nested folder, right\-click the folder in which you want to create a child folder, and then continue to step 2.

2.  Point to **New** and click **Folder**.

3.  Type a folder name, and then click **OK**.

## <a name="BKMK_AddShortcutstoViews"></a>Add Shortcuts to Views
In My Workspace, you can add shortcuts to any existing views in the Monitoring workspace.

#### To add a view to My Workspace

1.  In the **Monitoring** workspace, select a view, right\-click, and then click **Add to My Workspace**.

2.  Specify the folder in My Workspace where you want the view to appear.

3.  Click **OK**.

When you go to My Workspace, you will see the view that you added listed in the navigation pane.

## <a name="bkmk_savesearches"></a>Save Searches
You can save useful searches in My Workspace to run at any time.

#### To save a search in My Workspace

1.  Click **Saved Searches**.

2.  In the **Tasks** pane, click **Create New Search**.

3.  In the **Advanced Search** window, select the object type for your search. Your options are:

    -   Alerts

    -   Events

    -   Managed Objects

    -   Monitors

    -   Object Discoveries

    -   Rules

    -   Tasks

    -   Views

    Each object type will display a unique set of criteria for your search. For more information on advanced search criteria, see [Using Advanced Search](Using-Advanced-Search.md).

4.  In the displayed criteria for the object type, select the condition that you want to search against.

5.  Each condition that you select is added to the **Criteria description**. Click the underlined value in each condition to edit the value. After you edit a value, click **OK** and then edit the next value. Continue until all conditions have values specified.

6.  Click **Save parameters to My Favorites**.

7.  Enter a name for the saved search and click **OK**.

You can run saved searches right\-clicking a search in the list and then clicking **Search Now**.

## <a name="bkmk_createviews"></a>Create Views
Views that you create in My Workspace are unique views, not shortcuts to existing views. As an operator, you can create views in the My Workspace pane. You must have the rights of the Author role to create a view in the Monitoring workspace.

> [!NOTE]
> The general instructions in the following procedure do not apply to Diagram, Web Page, or Dashboard views. For more information on creating a view, see the specific view type in [Creating Views in Operations Manager](Creating-Views-in-Operations-Manager.md).

#### To create a view in My Workspace

1.  Right\-click in the folder where you want to store the view and point to **New**. You can select any view type. For more information on the view types available, see [View Types in Operations Manager](View-Types-in-Operations-Manager.md).

2.  In the view properties, enter a name and description for the view. The view properties dialog box contains two tabs: **Criteria** and **Display**.

    On the **Criteria** tab, in the **Show data related to** field, specify the item to target. The item you select will display related conditions in the **Select conditions** section. For more information, see [Guidance for Scoping and Targeting Views](Guidance-for-Scoping-and-Targeting-Views.md).

    After you select a condition, you can edit the value for that condition in the **Criteria description** section.

3.  In the **Show data contained in a specific group** field, you can select a group to limit the search results to members of that group.

4.  On the **Display** tab, select the columns that you want displayed in the view. You can also specify how to sort the columns and group the items.

5.  After you have specified the conditions and values for the view, click **OK**. The new view will appear in the navigation pane.

## See Also
[Standard Views in Operations Manager](Standard-Views-in-Operations-Manager.md)
[How to Personalize a View in Operations Manager](How-to-Personalize-a-View-in-Operations-Manager.md)
[Using Advanced Search](Using-Advanced-Search.md)
[Guidance for Scoping and Targeting Views](Guidance-for-Scoping-and-Targeting-Views.md)
[Using the Reporting Workspace in Operations Manager](Using-the-Reporting-Workspace-in-Operations-Manager.md)
[Using the Administration Workspace in Operations Manager](Using-the-Administration-Workspace-in-Operations-Manager.md)
[Using the Authoring Workspace in Operations Manager](Using-the-Authoring-Workspace-in-Operations-Manager.md)
[Using Health Explorer in Operations Manager](Using-Health-Explorer-in-Operations-Manager.md)
[Using the Monitoring Workspace in Operations Manager](Using-the-Monitoring-Workspace-in-Operations-Manager.md)
[How to Connect to the Web Console](How-to-Connect-to-the-Web-Console.md)
[How to Connect to the Operations Console](How-to-Connect-to-the-Operations-Console.md)
[Using the Operations Manager Consoles](Using-the-Operations-Manager-Consoles.md)


