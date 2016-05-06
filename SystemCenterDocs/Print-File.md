---
title: Print File
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1bec7174-4cf0-464b-aeb3-c179d52fb1dd
---
# Print File
The Print File activity prints text files to a printer that you specify. You can use this activity to print log files for paper filing before the data is moved or deleted from a server.

## Configuring the Print File Activity
Before you configure the Print File activity, you need to determine the following:

-   File name you are printing.

-   Printer name

Use the following information to configure the Print File activity.

### Details Tab

|Settings|Configuration Instructions|
|------------|------------------------------|
|**File**|Type the path and name of the file that you want to print.|
|**Printer**|Type the path of the printer that will print the file.|
|**Age**|Specify **is less than** or **is more than** to print the files that are older or newer, respectively, than the number of days that you specify.|
|**days**|Enter the number of **days** that you will use with the **Age** measure.|

### Published Data
The following table lists the published data items.

|Item|Description|
|--------|---------------|
|Origin folder|The path of the base folder where the file was printed from.|
|Number of successful file operations|The number of files that were successfully printed.|
|Number of failed file operations|The number of files that failed to print.|
|For each file:|
|Name and path of the file|The path of the file that was printed.|
|Name of the printer|The printer that was used to print the file.|


