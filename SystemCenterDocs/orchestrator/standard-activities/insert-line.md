---
title: Insert Line 
description: This article describes inserts lines into a text file on a line number that you specify.
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ae2bc14f-7027-484e-95c0-4cad77b8f5ef
caps.latest.revision: 13
author: jyothisuri
ms.author: jsuri
---
# Insert Line

The Insert Line activity inserts lines into a text file on a line number that you specify.  

 This activity replaces functionality in the Manage Text File legacy activity from Opalis 6.3.  

## Configure the Insert Line Activity

 Before you configure the Insert Line File activity, you need to determine the following:  

- The name of the file you want to insert text into.  

- The file encoding type of the file you want to insert text into.  

- The line number location where you want to insert the text.  

Use the following information to configure the Insert Line activity.  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**File**|Enter the path and name of the file that you want to insert the text into, or select the ellipsis button **(...)** and browse for it.|  
|**File encoding**|Select the ellipsis button **(...)** and select the format that the file is encoded in from the **File encoding** dropdown list. Verify that you select the correct encoding format. If the file uses a different encoding format, the activity fails.|  
|**Text**|Enter the text that you want to insert into the file.|  
|**Line number**|Enter the line number where the text will be inserted.|  

### Published Data

 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|File name|The name of the file that the text was inserted into.|  
|File encoding|The file encoding format that you selected in the File encoding field.|  
|Line text|The text of the line that was inserted.|  
|Line number|The line number that was inserted, if only one line was inserted.|
