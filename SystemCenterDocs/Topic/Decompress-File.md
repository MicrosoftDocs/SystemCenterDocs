---
title: Decompress File
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ca5b4132-d8bd-4052-95f3-d7df76ae426a
---
# Decompress File
The Decompress File activity decompresses the files contained in a zip archive file. You can extract files from zip archives that are downloaded using email or FTP.

## Configuring the Decompress File Activity
Before you configure the Decompress File activity, you need to determine the following:

-   The archive file name that you want to decompress.

-   The files names within the archive that you want to extract.

Use the following information to configure the Decompress File activity.

### Details Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**File**|Type the path of the archive file that you want to extract files from.|
|**Files to extract**|Type the name of the file that you want to extract. You can use the \* and ? wildcards to specify the file name. These wildcards behave in the same way as in the Windows Command Prompt.|
|**Folder**|Type the folder name to which the files will be extracted, or click the ellipsis **\(...\)** button and browse for it.|
|**Reproduce tree**|Select this option to extract the files to the same relative paths that they were saved in. To use this feature, the relative paths must have been stored in the zip archive when it was created.|
|**If the destination file exists**|Select the action that you want to take if a file with the same name as the file being extracted exists in the destination folder:<br /><br />**Create a file with a unique name**: Select this option to append a value to the filename to create a unique filename that does not conflict with an existing filename.<br /><br />**Overwrite**: Select this option to overwrite the existing file with the file that you are extracting.<br /><br />**Fail**: Select this option to cause the **Decompress File** activity to fail if the file name already exists.|

### Published Data
The following table lists published data items.

|Item|Description|
|--------|---------------|
|Archive name and path|The name of the archive file that was decompressed.|
|Number of files within archive|The total number of files that are inside the archive file.|
|Size of archive|The size of the archive file.|
|Size of the decompressed files|The total size of the files decompressed.|

