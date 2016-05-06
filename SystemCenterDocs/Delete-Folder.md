---
title: Delete Folder
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7bd72977-b6e1-4d20-af6e-42354f986c5b
---
# Delete Folder
The Delete Folder activity deletes a folder, sub\-folders, or the entire folder tree of a directory on the local file system or a network location specified using a UNC path. You can delete temporary folders that were created when a runbook runs or you can use this activity to purge data that has been recently archived.

## Configuring the Delete Folder Activity
Before you configure the Delete Folder activity, you need to determine the following:

-   The folder name you are targeting.

-   Whether you are going to delete the entire tree; delete the sub\-folders only; or delete just the directory.

Use the following information to configure the Delete Folder activity.

### Details Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Path**|Type the path of the folder that you are targeting.|
|**Delete the folder only if it is empty**|Select this option to delete the folder only if there are no files or sub\-folders in it.|
|**Delete all files and sub\-folders**|Select this option to delete the specified folder and all sub\-folders and files contained in that folder.|

### Published Data
The following table lists the published data items.

|Item|Description|
|--------|---------------|
|Folder path|The path of the folder that was deleted.|
|Folder pattern to match|The pattern used to find the sub\-folder that was deleted.|
|Base Folder to start deletion from|The **Path** that was specified on the **Details** tab.|
|Delete folder options|The option that you selected for the delete folder operation.|
|Name and path of the folder|The name and path of the folder that was deleted.|


