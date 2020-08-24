---
title: "Print File | Microsoft Docs"
ms.custom: ""
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
ms.assetid: 1bec7174-4cf0-464b-aeb3-c179d52fb1dd
caps.latest.revision: 13
author: "bwren"
ms.author: "bwren"
manager: "cfreeman"
---
# Print File

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

> [!IMPORTANT]
>
> This version of Orchestrator has reached the end of support, we recommend you to [upgrade to Orchestrator 2019](https://docs.microsoft.com/system-center/orchestrator/?view=sc-orch-2019).

::: moniker-end

The Print File activity prints text files to a printer that you specify. You can use this activity to print log files for paper filing before the data is moved or deleted from a server.  

## Configuring the Print File Activity  
 Before you configure the Print File activity, you need to determine the following:  

- File name you are printing.  

- Printer name  

Use the following information to configure the Print File activity.  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**File**|Type the path and name of the file that you want to print.|  
|**Printer**|Type the path of the printer that will print the file.|  
|**Age**|Specify **is less than** or **is more than** to print the files that are older or newer, respectively, than the number of days that you specify.|  
|**days**|Enter the number of **days** that you will use with the **Age** measure.|  

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
