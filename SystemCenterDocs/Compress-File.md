---
title: Compress File
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cdc74cd7-336f-42f7-b5fd-ffad7f926211
---
# Compress File
The Compress File activity compresses files into zip archives. You can use the Compress File activity to archive log files before storage or before sending them to another location using FTP or email.

## Configuring the Compress File Activity
Before you configure the Compress File activity, you need to know which files you will compress.

Use the following information to configure the Compress File activity.

### Details Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Folder**|Type the path to the file, or to the folder that contains the files, that you want to compress, or click the ellipsis **\(...\)** button and browse for the files. You can use wildcards in filenames.  You cannot browse for the folder name; you must type in the full folder name and location and include a trailing slash.|
|**Include files in sub\-folders**|Select this option to include any files that are found within sub\-folders of the folder that you specified.|
|**File**|Type the path and filename of the archive that you are creating. This field will only accept characters from the current system locale. If you use other characters, the activity will fail.|
|**Store relative path in archive**|Select this option to store the files within the same sub\-folders that they were found in. When this option is unselected, the files will be added to the archive with the full path. For example:<br /><br />**Selected**: ..\\subfolder1\\file.txt, and ..\\subfolder1\\subfolder2\\file.txt<br /><br />**Unselected**: C:\\files\\subfolder1\\file.txt, and C:\\files\\subfolder1\\subfolder2\\file.txt|
|**If the destination archive already exists**|Select the action that you want to take if a file with the same name as the archive being created already exists in the destination folder:<br /><br />**Add files to the existing archive**: Select this option to add the files that you specified to the existing archive.<br /><br />**Overwrite the existing archive**: Select this option to overwrite the existing file with the archive that you are creating.<br /><br />**Fail if the archive exists**: Select this option to cause the Compress File activity to fail if the filename already exists.<br /><br />**Create a unique named archive**: Select this option to append a value to the filename to create a unique filename that does not conflict with the existing filename.|
|Compression level|Select the level of compression that you want to use to compress the files into the archive. You can select one of the following levels.<br /><br />-   None<br />-   Low<br />-   Medium<br />-   High<br /><br />Higher compression levels take more time to complete but usually result in smaller files. Lower compression levels create larger archives, but take less time to complete.|

### Published Data
The following table lists the published data items.

|Item|Description|
|--------|---------------|
|Archive name and path|The name and path of the archive file that was created.|
|Number of files within archive|The number of files inside the archive file.|
|Size of archive|The size of the archive file.|

