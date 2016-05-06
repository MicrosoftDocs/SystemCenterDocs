---
title: Move Folder
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 011ed34f-7aa9-41bd-99fc-8d6700af179e
---
# Move Folder
The Move Folder activity moves a folder and its sub\-folders from one directory to another. You can also move folders to network shares that are available using UNC paths. In addition, you can take files from a local or network folder that are made publicly available as an FTP location and move them to an internal folder.

## Configuring the Move Folder Activity
Use the following information to configure the Move Folder activity.

### Details Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**Source**|Type the path of the folder that you want to move, or click the ellipsis **\(...\)** button to browse for it. The Move Folder activity does not support the \* and ? wildcards.|
|**Destination**|Type the path and name that you want to move the folder to, or click the ellipsis **\(...\)** button to browse for it.|

### Published Data
The following table lists the published data items.

|Item|Description|
|--------|---------------|
|Origin name of the folder|The path of the original folder that was moved.|
|Destination name of the folder|The destination folder where the folder was moved to.|
|New folder path|The new path of the folder that was moved.|

