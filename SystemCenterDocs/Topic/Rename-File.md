---
title: Rename File
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c2f45811-c1de-4b38-b52d-e4f329c36868
---
# Rename File
The Rename File activity renames files on the local file system or on a network location specified using a UNC path. You can automatically rename files to a standard format according to your data center procedures.

## Configuring the Rename File Activity
Before you configure the Rename File activity, you need to determine the following:

-   The original file name you are renaming.

-   The new name of the file

Use the following information to configure the Rename File activity.

### Details Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Folder**|Type the path of the folder that contains the files that you want to rename.|
|**Include sub\-folders**|Select this option to rename any files in the subfolders of the folder that you specified that match the file names that you want to rename.|
|**Destination**|This list displays all the file names that will be renamed when this activity runs. To add a filename, click **Add** to open the **Rename Properties** dialog box, and specify the **Old name** and then specify the file **New name**.<br /><br />To edit the list of file names, click **Edit**. To remove file names, click **Remove**.|

### Advanced Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**File age**|Specify **Is less than** or **Is more than** to rename the files that are older or newer, respectively, than the number of days that you specify.|
|**days**|Type the number of days that you will use with the **File age** measure.|
|**Date of rename**|Select this option to set the date of the file at the destination to the date when it was renamed.|
|**Same as original**|Select this option to set the date of the file at the destination to the date of the original file.|
|**Destination already exists**|Select the action that you want to take if a file with the same name already exists in the folder:<br /><br />**Overwrite**: Select this option to overwrite the existing file with the file that is being renamed.<br /><br />**Fail**: Select this option to cause the Rename File activity to fail if the filename already exists.<br /><br />**Create a file with a unique name**: Select this option to append a value to the filename to create a unique name that does not conflict with an existing name.|

### Published Data
The following table lists the published data items.

|Item|Description|
|--------|---------------|
|File path|The path of the file that was renamed.|
|Include sub\-folders|Indicates whether this option was selected.|
|Destination folder|The destination folder of the file that was renamed.|
|If destination exists|The option that was selected for handling the filename if the file existed in the destination folder.|
|Modified date option|The option that was selected for assigning a modified date to the file in the destination folder.|
|File age days|The number of days used in the File age filter.|
|Destination date|The option that was selected for assigning a destination date to the file in the destination folder.|
|Total number of files to be renamed|The number of files that were renamed by the operation.|
|Number of successful file operations|The number of successful operations that occurred.|
|Number of failed file operations|The number of failed operations that occurred.|
|Origin folder|The folder where the file originated from.|
|Name and path of the destination file|The name and path of the destination file.|
|File name|The filename of the origin file.|
|Name and path of the file relative to the origin folder|The relative path of the file, relative to the origin folder.|
|Name and path of the origin file|The name and path of the origin file.|
|File operation status|The status of the rename operation.|
|Pattern that matched file|The pattern that the user entered that matched the file or files that were found.|
|Pattern file renamed to|The pattern that the file or files were renamed.|

