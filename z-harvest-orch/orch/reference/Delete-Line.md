---
title: Delete Line
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d100cc47-7340-4072-a6dc-77c4d2241566
author:bwren
manager:cfreemanwa
---
# Delete Line
The Delete Line activity deletes lines from a text file.  Use the Delete Line activity to delete outdated lines of text from a text file.  
  
This activity replaces functionality in the Manage Text File legacy activity from Opalis 6.3.  
  
## Configuring the Delete Line Activity  
Before you configure the Delete Line activity you need to determine the following:  
  
-   The name of the file that you want to delete the line from.  
  
-   The file encoding type that the file you want to delete the line from uses.  
  
-   The line numbers of the lines that you want to delete.  
  
Use the following information to configure the Delete Line activity.  
  
### Details Tab  
  
|Settings|Configuration Instructions|  
|------------|------------------------------|  
|**File**|Type the path and name of the file that you want to delete the text from, or click the ellipsis button \(...\) and browse for it.|  
|**File encoding**|Click the ellipsis button **\(...\)** and select the format that the file is encoded in from the File encoding drop\-down list. Verify that you select the correct encoding format. If the file uses a different encoding format, the activity fails.|  
|**Line numbers**|Type the line numbers of the text that you want to delete from the file that you specified.<br /><br />To specify a range of lines, use a hyphen: 1\-3. This deletes lines 1 to 3.<br /><br />To specify specific lines, use a comma: 5,7,9. This deletes lines 5, 7, and 9.<br /><br />Combine the range and specific lines: 1\-3,5,7,9. This deletes lines 1 to 3, and lines 5, 7, and 9.<br /><br />To specify from a specific line to the last line of the file, type the line number, hyphen, and END: 4\-END. This deletes lines 4 to the last line of the file.<br /><br />To specify from a specific line to a line relative to the last line of the file, type the line number, hyphen, the less\-than sign, and the line number relative to the end line: 4\-END<3. If the file has 20 lines, this deletes lines 4 to 17 from the file. <3 represents the third line from the end.<br /><br />To specify the last number of lines, type LASTLINES, colon, and the last number of lines that you want to delete: LASTLINES:10. This deletes the last 10 lines of the file.<br /><br />Combine different types of operations: 1\-5, 8, 10\-END<20, LASTLINES:10. This deletes lines 1 to 5, line 8, line 10 to the 20th line from the end, and the last 10 lines. Do not overlap lines or line ranges when combining operations. For example, 5\-END, LASTLINES:10 fails because the 5\-END operation already deletes to the end, so the LASTLINES:10 operation cannot succeed because the lines are already deleted, and the activity fails. **Important:** Do not specify lines numbers that do not exist in the file, and do not specify a line number more than once, or the activity fails.|  
  
### Published Data  
The following table lists the published data items.  
  
|Item|Description|  
|--------|---------------|  
|File name|The file name of the text file from which the line is deleted.|  
|File encoding|The file encoding format that you selected in the File encoding field.|  
|Line number|The line number of each line that was deleted. A Published Data item is created for each line that was deleted.|  
|Line numbers|The line number range that the user typed in the field.|  
|Deleted text|The text that was deleted from the file.|  
|Number of deletions|The number of deletions that occurred.|  
  
