---
title: "Insert Line | Microsoft Docs"
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
ms.assetid: ae2bc14f-7027-484e-95c0-4cad77b8f5ef
caps.latest.revision: 13
author: "bwren"
ms.author: "bwren"
manager: "cfreeman"
---
# Insert Line

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

> [!IMPORTANT]
>
> This version of Orchestrator has reached the end of support, we recommend you to [upgrade to Orchestrator 2019](https://docs.microsoft.com/system-center/orchestrator/?view=sc-orch-2019).

::: moniker-end

The Insert Line activity inserts lines into a text file on a line number that you specify.  

 This activity replaces functionality in the Manage Text File legacy activity from Opalis 6.3.  

## Configuring the Insert Line Activity  
 Before you configure the Insert Line File activity, you need to determine the following:  

- The name of the file you want to insert text into.  

- The file encoding type of the file you want to insert text into.  

- The line number location where you want to insert the text.  

Use the following information to configure the Insert Line activity.  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**File**|Type the path and name of the file that you want to insert the text into, or click the ellipsis button **(...)** and browse for it.|  
|**File encoding**|Click the ellipsis button **(...)** and select the format that the file is encoded in from the **File encoding** drop-down list. Verify that you select the correct encoding format. If the file uses a different encoding format, the activity fails.|  
|**Text**|Type the text that you want to insert into the file.|  
|**Line number**|Type the line number where the text will be inserted.|  

### Published Data  
 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|File name|The name of the file that the text was inserted into.|  
|File encoding|The file encoding format that you selected in the File encoding field.|  
|Line text|The text of the line that was inserted.|  
|Line number|The line number that was inserted, if only one line was inserted.|
