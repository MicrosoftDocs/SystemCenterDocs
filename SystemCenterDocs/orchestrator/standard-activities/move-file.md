---
title: Move File
description: This article provides the details about Move File activity.
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: concept-article
ms.assetid: 83c535d6-c827-4107-9b39-87d5716c6663
caps.latest.revision: 13
author: Jeronika-MS
ms.author: v-gajeronika
---
# Move File

The Move File activity moves a file from one directory to another. You can move files to network shares that are available using UNC paths. You can also move files from a local or publicly available network folder, such as an FTP location, to an internal folder.  

## Configure the Move File Activity

 Before you configure the Move File activity, you need to determine the following:  

- The files you're moving.  

- The destination path where you'll move the files.  

Use the following information to configure the Move File activity.  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**File**|Enter the path and name of the file that you want to move. You can use the * and ? wildcards to specify the filename and path. These wildcards behave the same way as in the Windows Command Prompt.|  
|**Include sub-folders**|Select this option to move any files within the sub-folders of the path you've specified that match the filename that you've specified.|  
|**Folder**|Enter the path of the folder where you want the files to be moved to.|  
|**If the destination exists**|Select the action that you want to take if a file with the same name already exists in the destination folder:<br /><br /> **Overwrite**: Select this option to overwrite the existing file with the file that is being moved.<br /><br /> **Fail**: Select this option to cause the Move File activity to fail if the filename already exists.<br /><br /> **Create a file with a unique name**: Select this option to append a value to the filename to create a unique name that doesn't conflict with an existing name.|  

### Advanced Tab

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**File age**|Select **Is less than** or **Is more than** from the dropdown list to move the files that are older or newer, respectively, than the number of **days** that you specify.|  
|**days**|Enter the number of **days** that you'll use with the **File age** measure.|  
|**Date of transfer**|Set the file date at the destination to the date when it was copied to the folder.|  
|**Same as original**|Set the date of the file at the destination to the date of the original file.|  

### Published Data

 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Origin folder|The path of the base folder where the file was moved from.|  
|Destination folder|The destination folder where the file was moved to.|  
|Total number of files to be transferred|The number of files that matched the file that you specified.|  
|Number of successful file operations|The number of files that were successfully moved.|  
|Number of failed file operations|The number of files that failed to move.|  
|File operation status|Determines whether the move operation succeeded or failed.|  
|File path|The path of the file that was moved.|  
|File name|The name of the file that was moved.|  
|Name and path of the file relative to the origin folder|The relative path of the file starting from the origin folder.|  
|If destination exists|The option that was selected to handle the operation if the destination file already exists.|  
|File age date option|The option that was selected to evaluate the file age.|  
|File age days|The number of days that was provided to evaluate the file age.|  
|Modified date option|The option that was selected for the date to be assigned to the destination file.|  
|Name and path of the destination file|The name and path that the file was moved to.|  
|Name and path of the origin file|The name and path that the file was moved from.|  
|Include sub-folders|Indicates whether the **Include sub-folders** checkbox was selected.|
