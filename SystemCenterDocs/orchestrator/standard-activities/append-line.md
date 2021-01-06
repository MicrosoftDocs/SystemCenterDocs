---
title: "Append Line | Microsoft Docs"
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
ms.assetid: 652ce6db-3ca9-42bc-87f3-82e796f65e2c
caps.latest.revision: 14
author: "bwren"
ms.author: "bwren"
manager: "cfreeman"
---
# Append Line

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

> [!IMPORTANT]
>
> This version of Orchestrator has reached the end of support, we recommend you to [upgrade to Orchestrator 2019](https://docs.microsoft.com/system-center/orchestrator/).

::: moniker-end

The Append Line activity appends a line of text into a text file.  Use the Append Line activity to append lines to a log file to create audits trails of runbooks.  

 This activity replaces functionality in the Manage Text File legacy activity from Opalis 6.3.  

## Configuring the Append Line Activity  
 Before you configure the Append Line activity, you need to determine the following:  

- The file name you want to append to.  

- The type of file encoding that the file you are appending to uses.  

- Text you append.  

Use the following information to configure the Append Line activity.  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**File**|Type the path and name of the file that you want to append the text to, or click the ellipsis button **(...)** and browse for it.|  
|**File encoding**|Click the ellipsis button **(...)** and select the format that the file is encoded in from the **File encoding** drop-down list. Verify that you select the correct encoding format. If the file uses a different encoding format, the activity fails.|  
|**Text**|Type the text that you want to append to the file that you specified.|  

### Published Data  
 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|File path|The path and file name of the text file to which the line is appended.|  
|File encoding|The file encoding format that you selected in the **File encoding** field.|  
|Line text|The text of the line that was appended to the text file.|  
|Line number|The line number where the text was appended.|
