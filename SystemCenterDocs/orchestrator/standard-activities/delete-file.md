---
title: Delete File activity
description: This article describes the delete file activity.
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: concept-article
ms.assetid: c79a70d9-2956-4898-a6fe-d1c54bf10fd0
caps.latest.revision: 11
author: jyothisuri
ms.author: jsuri
---
# Delete File

The Delete File activity deletes files from the local file system or from a network location specified using a UNC path. You can purge a folder that contains old log files.  

## Configure the Delete File Activity

 Before you configure the Delete File activity, you need to know which files you're deleting.  

 Use the following information to configure the Delete File activity.  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Path**|Enter the path and name of the file that you want to delete. You can use the `*` and `?` wildcards to specify the file name. These wildcards behave in the same way as the Windows Command Prompt.|  
|**Delete files from subfolders**|Select this option to delete any files within the subfolders of the path you've specified that match the file name that you've specified.|  
|**File age**|Select the **Is less than** or **Is more than** option from the dropdown list to delete the files that are older or newer, respectively, than the number of days that you specify.|  
|**days**|Enter the number of days that you'll use with the file age measure.|  

### Published Data

 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|File age days|The number of days that was provided to evaluate the file age.|  
|File age option|The option that was selected to evaluate the file age.|  
|Name and path of the file|The name and path of the file that was deleted.|  
|File name|The name of the file that was deleted.|  
|Name and path of the file relative to the origin folder|The relative path of the file starting from the origin folder.|  
|File operation status|Determines whether the delete operation succeeded or failed.|  
|Origin folder|The path of the base folder where the file was deleted from.|  
|Number of failed file operations|The number of files that weren't deleted.|  
|Number of successful file operations|The number of files that were successfully deleted.|  
|Total number of files|The number of files that matched the file that you specified.|  
|File path|The path of the file that was deleted.|  
|Delete files from subfolders|Indicates whether the Delete files from subfolders checkbox was selected.|
