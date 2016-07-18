---
title: Delete File
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c79a70d9-2956-4898-a6fe-d1c54bf10fd0
author:bwren
manager:cfreemanwa
---
# Delete File
The Delete File activity deletes files from the local file system or from a network location specified using a UNC path. You can purge a folder that contains old log files.  
  
## Configuring the Delete File Activity  
Before you configure the Delete File activity, you need to know which files you are deleting.  
  
Use the following information to configure the Delete File activity.  
  
### Details Tab  
  
|Settings|Configuration Instructions|  
|------------|------------------------------|  
|**Path**|Type the path and name of the file that you want to delete. You can use the \* and ? wildcards to specify the file name. These wildcards behave in the same way as the Windows Command Prompt.|  
|**Delete files from sub\-folders**|Select this option to delete any files within the sub\-folders of the path you have specified that match the file name that you have specified.|  
|**File age**|Select the **Is less than** or **Is more than** option from the drop\-down list to delete the files that are older or newer, respectively, than the number of days that you specify.|  
|**days**|Type the number of days that you will use with the file age measure.|  
  
### Published Data  
The following table lists the published data items.  
  
|Item|Description|  
|--------|---------------|  
|File age days|The number of days that was provided to evaluate the file age.|  
|File age option|The option that was selected to evaluate the file age.|  
|Name and path of the file|The name and path of the file that was deleted.|  
|File name|The name of the file that was deleted.|  
|Name and path of the file relative to the origin folder|The relative path of the file starting from the origin folder.|  
|File operation status|Determines whether the delete operation succeeded or failed.|  
|Origin folder|The path of the base folder where the file was deleted from.|  
|Number of failed file operations|The number of files that were not deleted.|  
|Number of successful file operations|The number of files that were successfully deleted.|  
|Total number of files|The number of files that matched the file that you specified.|  
|File path|The path of the file that was deleted.|  
|Delete files from sub\-folders|Indicates whether the Delete files from sub\-folders check box was selected.|  
  
