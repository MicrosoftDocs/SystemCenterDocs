---
title: Print File
description: This article describes the functionality of Print File Activity.
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 04/27/2023
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1bec7174-4cf0-464b-aeb3-c179d52fb1dd
caps.latest.revision: 13
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
---
# Print File

The Print File activity prints text files to a printer that you specify. You can use this activity to print log files for paper filing before the data is moved or deleted from a server.  

## Configure the Print File Activity

 Before you configure the Print File activity, you need to determine the following:  

- File name you're printing.  

- Printer name  

Use the following information to configure the Print File activity.  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**File**|Enter the path and name of the file that you want to print.|  
|**Printer**|Enter the path of the printer that will print the file.|  
|**Age**|Specify **is less than** or **is more than** to print the files that are older or newer, respectively, than the number of days that you specify.|  
|**days**|Enter the number of **days** that you'll use with the **Age** measure.|  

### Published Data

 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Origin folder|The path of the base folder where the file was printed from.|  
|Number of successful file operations|The number of files that were successfully printed.|  
|Number of failed file operations|The number of files that failed to print.|  
|For each file:|  
|Name and path of the file|The path of the file that was printed.|  
|Name of the printer|The printer that was used to print the file.|
