---
title: Read Line
description: This article describes the Read Line activity.
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 11/01/2024
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: concept-article
ms.assetid: 0ab7c54c-88fa-41fd-87be-00f959384b7d
caps.latest.revision: 13
author: jyothisuri
ms.author: jsuri
---
# Read Line

The Read Line activity reads lines from a text file. You can use the Read Line activity to read lines from a text file and pass them to another activity using published data.  

 This activity replaces functionality in the Manage Text File legacy activity from Opalis 6.3.  

## Configure the Read Line Activity

 Use the following information to configure the Read Line activity.  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**File**|Enter the path and name of the file that you want to read the text from, or select the ellipsis button **(...)** and browse for it.|  
|**File encoding**|Select the ellipsis button **(...)** and select the format that the file is encoded in from the **File encoding** dropdown list. Verify that you select the correct encoding format. If the file uses a different encoding format, the activity fails.|  
|**Line numbers**|Enter the line numbers of the text that you want to read from the file that you specified.<br /><br /> -   To specify a range of lines, use a hyphen: 1-3. This reads lines 1 to 3.<br />-   To specify specific lines, use a comma: 5,7,9. This reads lines 5, 7, and 9.<br />-   Combine the range and specific lines: 1-3,5,7,9. This reads lines 1 to 3, and lines 5, 7, and 9.<br />-   To specify from a specific line to the last line of the file, enter the line number, hyphen, and END: 4-END. This reads lines 4 to the last line of the file.<br />-   To specify from a specific line to a line relative to the last line of the file, enter the line number, hyphen, the less-than sign, and the line number relative to the end line: 4-END<3. If the file has 20 lines, this reads lines 4 to 17 from the file. <3 represents the third line from the end.<br />-   To specify the last number of lines, enter LASTLINES, colon, and the last number of lines that you want to delete: LASTLINES: 10. This reads the last 10 lines of the file.<br />-   Combine different types of operations: 1-5, 8, 10-END<20, LASTLINES: 10. This reads lines 1 to 5, line 8, line 10 to the 20th line from the end, and the last 10 lines. Don't overlap lines or line ranges when combining operations. For example, 5-END, LASTLINES: 10 fails because the 5-END operation already reads to the end, so the LASTLINES: 10 operation can't succeed because the lines are already read, and the activity fails. **Important:**  Don't specify line numbers that don't exist in the file, and don't specify a line number more than once, or the activity will fail.|  

### Published Data

 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|File name|The file name of the text file that was read.|  
|File encoding|The file encoding format that you selected in the File encoding field.|  
|Line text|The text of the line that was read.|  
|Line number|The line number of the text that was read. A published data item is created for each line that was read.|  
|Line numbers|The line number range that the user entered in the field.|
