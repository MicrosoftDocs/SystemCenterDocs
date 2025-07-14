---
title: Append Line
description: This article describes the functionality of Append Line Activity.
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: concept-article
ms.assetid: 652ce6db-3ca9-42bc-87f3-82e796f65e2c
caps.latest.revision: 14
author: jyothisuri
ms.author: jsuri
---
# Append Line

The Append Line activity appends a line of text into a text file. Use the Append Line activity to append lines to a log file to create audits trails of runbooks.  

 This activity replaces functionality in the Manage Text File legacy activity from Opalis 6.3.  

## Configure the Append Line Activity

 Before you configure the Append Line activity, you need to determine the following:  

- The file name you want to append to.  

- The type of file encoding that the file you're appending to uses.  

- The text you append.  

Use the following information to configure the Append Line activity.  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**File**|Enter the path and name of the file that you want to append the text to, or select the ellipsis button **(...)** and browse for it.|  
|**File encoding**|Select the ellipsis button **(...)** and select the format that the file is encoded in from the **File encoding** dropdown list. Verify that you select the correct encoding format. If the file uses a different encoding format, the activity fails.|  
|**Text**|Enter the text that you want to append to the file that you specified.|  

### Published Data

 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|File path|The path and file name of the text file to which the line is appended.|  
|File encoding|The file encoding format that you selected in the **File encoding** field.|  
|Line text|The text of the line that was appended to the text file.|  
|Line number|The line number where the text was appended.|
