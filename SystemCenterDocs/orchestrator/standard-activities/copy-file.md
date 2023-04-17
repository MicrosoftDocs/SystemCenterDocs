---
title: Copy File
description: This article describes the functionality of Copy File activity.
ms.custom: UpdateFrequency3
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
ms.assetid: 9f718d16-c8d9-48ba-8c84-907d3ec69437
caps.latest.revision: 13
author: "jyothisuri"
ms.author: "jsuri"
manager: mkluck
---
# Copy File

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

> [!IMPORTANT]
>
> This version of Orchestrator has reached the end of support. We recommend you to [upgrade to Orchestrator 2019](../index.yml).

::: moniker-end

The Copy File activity copies a file from one directory to another. You can also copy files to network shares that are available using UNC paths. Use the Copy File activity to copy important files that have been created or modified in a folder that's being monitored by the Monitor Folder activity to a backup location.  

## Configuring the Copy File Activity  
 Before you configure the Copy File activity, you need to know which files you're copying and the destination path where you'll put the copies.  

 Use the following information to configure the Copy File activity.  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**File**|Enter the path and name of the file that you want to copy. You can use the * and ? wildcards to specify the file name or path. These wildcards behave the same way as in the Windows Command Prompt.|  
|**Include sub-folders**|Select this option to copy any files within the sub-folders of the path you've specified that match the filename that you've specified.|  
|**Folder**|Enter the path of the folder where you want the files to be copied to.|  
|**If the destination exists**|Select the action that you want to take if a file with the same name already exists in the destination folder:<br /><br /> **Overwrite**: Select this option to overwrite the existing file with the file that's being copied.<br /><br /> **Fail**: Select this option to cause the Copy File activity to fail if the filename already exists.<br /><br /> **Create a file with a unique name**: Select this option to append a value to the filename to create a unique name that doesn't conflict with an existing name.|  

### Advanced Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**File age**|Specify **Is less than** or **Is more than** to copy the files that are older or newer, respectively, than the number of days that you specify.|  
|**days**|Enter the number of **days** that you'll use with the **File age** measure.|  
|**Date of transfer**|Set the date of the file at the destination to the date when it was copied to the folder.|  
|**Same as original**|Set the date of the file at the destination to the date of the original file.|  

### Published Data  
 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Origin folder|The path of the base folder where the file was copied from.|  
|Destination folder|The destination folder where the file was copied to.|  
|Total number of files to be transferred|The number of files that matched the criteria that you specified.|  
|Number of successful file operations|The number of files that were successfully copied.|  
|Number of failed file operations|The number of files that failed to copy.|  
|File operation status|Determines whether the copy succeeded or failed.|  
|File path|The path of the file that was copied.|  
|File name|The name of the file that was copied.|  
|Name and path of the file relative to the origin folder|The relative path of the file starting from the origin folder.|  
|If destination exists|The option that was selected to handle the operation if the destination file already exists.|  
|File age date options|The option that was selected to evaluate the file age.|  
|File age days|The number of days that was provided to evaluate the file age.|  
|Modified date option|The option that was selected for the date to be assigned to the destination file.|  
|Name and path of the destination file|The name and path that the file was copied to.|  
|Name and path of the origin file|The name and path that the file was copied from.|  
|Include sub-folders|Indicates whether the Include sub-folders check box was selected.|  
|Origin folder|The path of the base folder where the file was copied from.|  
|Destination folder|The destination folder where the file was copied to.|  
|Total number of files to be transferred|The number of files that matched the criteria that you specified.|  
|Number of successful file operations|The number of files that were successfully copied.|  
|Number of failed file operations|The number of files that failed to copy.|  
|File operation status|Determines whether the copy succeeded or failed.|  
|File path|The path of the file that was copied.|  
|File name|The name of the file that was copied.|  
|Name and path of the file relative to the origin folder|The relative path of the file starting from the origin folder.|  
|If destination exists|The option that was selected to handle the operation if the destination file already exists.|  
|File age date options|The option that was selected to evaluate the file age.|  
|File age days|The number of days that was provided to evaluate the file age.|  
|Modified date option|The option that was selected for the date to be assigned to the destination file.|  
|Name and path of the destination file|The name and path that the file was copied to.|  
|Name and path of the origin file|The name and path that the file was copied from.|  
|Include sub-folders|Indicates whether the Include sub-folders checkbox was selected.|