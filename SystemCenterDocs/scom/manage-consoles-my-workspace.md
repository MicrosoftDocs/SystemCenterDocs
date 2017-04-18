---
title: Using My Workspace
description: This article describes how to use My Workspace in the Operations Manager Operations console create personalized views of operational data for your specific needs.  
author: mgoedtel
ms.author: magoedte
ms.manager: cfreeman
ms.date: 12/05/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
ms.assetid: 91b1dd4c-6ce2-442b-826f-21a265ed3ac7
---

# Using My Workspace 

>Applies To: System Center 2016 - Operations Manager

My Workspace provides you with a private area in the Operations console that you can customize for your specific needs.  Using My Workspace, you can create folders to organize the workspace, add shortcuts to favorite views, save useful searches, and create views that are only visible to you. Your configuration of My Workspace will be available to you in any Operations or Web console that you log in to using the same Windows credentials.  
  
## Create folders in My Workspace  

My Workspace contains two default folders: **Favorite Views** and **Saved Searches**. You can create additional folders to better organize your workspace. All new folders that you create will be created under **Favorite Views**.  
  
### To create a new folder in My Workspace  
  
1.  Right-click in the navigation pane.  
  
    > [!NOTE]  
    > To create a nested folder, right-click the folder in which you want to create a child folder, and then continue to step 2.  
  
2.  Point to **New** and click **Folder**.  
  
3.  Type a folder name, and then click **OK**.  
  
## Add Shortcuts to views  

In My Workspace, you can add shortcuts to any existing views in the Monitoring workspace.  
  
### To add a view to My Workspace  
  
1.  In the **Monitoring** workspace, select a view, right-click, and then click **Add to My Workspace**.  
  
2.  Specify the folder in My Workspace where you want the view to appear.  
  
3.  Click **OK**.  
  
When you go to My Workspace, you will see the view that you added listed in the navigation pane.  
  
## Save searches  

You can save useful searches in My Workspace to run at any time.  
  
### To save a search in My Workspace  
  
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
  
    Each object type will display a unique set of criteria for your search. For more information on advanced search criteria, see [Using Advanced Search](manage-console-using-adv-search.md).  
  
4.  In the displayed criteria for the object type, select the condition that you want to search against.  
  
5.  Each condition that you select is added to the **Criteria description**. Click the underlined value in each condition to edit the value. After you edit a value, click **OK** and then edit the next value. Continue until all conditions have values specified.  
  
6.  Click **Save parameters to My Favorites**.  
  
7.  Enter a name for the saved search and click **OK**.  
  
You can run saved searches right-clicking a search in the list and then clicking **Search Now**.  
  
## Create views  

Views that you create in My Workspace are unique views, not shortcuts to existing views. As an operator, you can create views in the My Workspace pane. You must have the rights of the Author role to create a view in the Monitoring workspace.  
  
> [!NOTE]  
> The general instructions in the following procedure do not apply to Diagram, Web Page, or Dashboard views. For more information on creating a view, see the specific view type in [How to Create and Scope Views in Operations Manager](manage-console-scope-views.md).  
  
### To create a view in My Workspace  
  
1.  Right-click in the folder where you want to store the view and point to **New**. You can select any view type. For more information on the view types available, see [View Types in Operations Manager](manage-console-view-types.md).  
  
2.  In the view properties, enter a name and description for the view. The view properties dialog box contains two tabs: **Criteria** and **Display**.  
  
    On the **Criteria** tab, in the **Show data related to** field, specify the item to target. The item you select will display related conditions in the **Select conditions** section. For more information, see [Creating and Scoping Views in Operations Manager](manage-console-scope-views.md).  
  
    After you select a condition, you can edit the value for that condition in the **Criteria description** section.  
  
3.  In the **Show data contained in a specific group** field, you can select a group to limit the search results to members of that group.  
  
4.  On the **Display** tab, select the columns that you want displayed in the view. You can also specify how to sort the columns and group the items.  
  
5.  After you have specified the conditions and values for the view, click **OK**. The new view will appear in the navigation pane.  
  
## Next steps 

- In the Operations console, you view monitoring data, manage monitoring configuration, create your own custom views and dashboards that are personalized for your experience, and perform management group administration by [Using the Operations Manager Operations console](../om/manage/using-the-operations-console-in-operations-manager.md).  
  
- For more information on using Health Explorer, see [Using Health Explorer to Investigate Problems](manage-health-using-healthexplorer.md).  

- To learn how to customize views in the Operations console defined in management packs imported in the management group, see [How to Personalize a View in Operations Manager](manage-console-personalize-views.md).  