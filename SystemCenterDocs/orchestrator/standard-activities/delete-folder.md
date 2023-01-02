---
title: Delete Folder activity
description: This article describes the Delete Folder activity.
ms.custom: ""
ms.date: "05/13/2016"
ms.prod: system-center
ms.reviewer: ""
ms.suite: ""
ms.technology: orchestrator
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center 2012 SP1 - Orchestrator"
  - "System Center 2012 - Orchestrator"
  - "System Center 2012 R2 Orchestrator"
ms.assetid: 7bd72977-b6e1-4d20-af6e-42354f986c5b
caps.latest.revision: 12
author: "jyothisuri"
ms.author: "jsuri"
manager: "evansma"
---
# Delete Folder

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

> [!IMPORTANT]
>
> This version of Orchestrator has reached the end of support. We recommend you to [upgrade to Orchestrator 2019](../index.yml).

::: moniker-end

The Delete Folder activity deletes a folder, subfolders, or the entire folder tree of a directory on the local file system or a network location specified using a UNC path. You can delete temporary folders that were created when a runbook runs or you can use this activity to purge data that has been recently archived.  

## Configuring the Delete Folder Activity  
 Before you configure the Delete Folder activity, you need to determine the following:  

- The folder name you're targeting.  

- Whether you're going to delete the entire tree; delete the subfolders only; or delete just the directory.  

Use the following information to configure the Delete Folder activity.  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Path**|Type the path of the folder that you're targeting.|  
|**Delete the folder only if it is empty**|Select this option to delete the folder only if there are no files or subfolders in it.|  
|**Delete all files and subfolders**|Select this option to delete the specified folder and all subfolders and files contained in that folder.|  

### Published Data  
 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Folder path|The path of the folder that was deleted.|  
|Folder pattern to match|The pattern used to find the sub-folder that was deleted.|  
|Base Folder to start deletion from|The **Path** that was specified on the **Details** tab.|  
|Delete folder options|The options that you selected for the delete folder operation.|  
|Name and path of the folder|The name and path of the folder that was deleted.|