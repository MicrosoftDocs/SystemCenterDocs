---
title: Read Text Log
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4b1150e4-ef0c-4fba-a358-53db2106399e
author:bwren
manager:cfreemanwa
---
# Read Text Log
The Read Text Log activity will read lines in a structured text log file. If you have log files that change names, you can configure the Read Text Log activity to read from the newest file in a folder that matches a file name pattern. The Read Text Log activity can be used to check a log for errors and then take corrective action on the server that is creating the log or send an email to an administrator to escalate the issue.  
  
> [!IMPORTANT]  
> For the Read Text Log activity to work correctly, every line in the text log file must begin with a timestamp.  
  
## Configuring the Read Text Log Activity  
Before you configure the Read Text Log activity, you need to determine the following:  
  
-   The log file name you are reading.  
  
-   The timestamps format in the log.  
  
Use the following information to configure the Read Text Log activity.  
  
### Details Tab  
  
|Settings|Configuration Instructions|  
|------------|------------------------------|  
|**File**|Select and type the name of the log file that will be read. You can also use the ellipsis **\(...\)** button to browse for the file.|  
|**The most recent file in this folder**|Select and type the folder where the most recent file that matches the pattern that you specify will be read. You can also use the ellipsis **\(...\)** button to browse for the folder.|  
|**Matching this pattern**|Type the file name pattern that will be used to find the log file that will be read. You can use the \* and ? wildcards to specify the pattern. These wildcards behave in the same way as the Windows Command Prompt.|  
|**Read**|Select and specify the dates that the lines you are reading are from:<br /><br />**lines between the dates…**: Select and specify the begin date and end date that make up the range that will be read. The dates that you specify must match the **Timestamp format**.<br /><br />**lines more recent than…**: Select and specify the oldest date of the logs that will be read. The date that you specify must match the entered **Timestamp format**.<br /><br />**new lines**: Select to read all the logs that have not previously been read by the Read Text Log activity.|  
|**Timestamp format**|Specify the format of the timestamp of the logs. For more information on how to specify the timestamp format, see the following Timestamp Format Codes table.|  
|**Read the last lines**|Enter the number of lines.|  
  
### Timestamp Format Codes  
  
|Code|Description|  
|--------|---------------|  
|%y|Year in two digits. For example, in this format '2005' would be represented as '05'.|  
|%Y|Year in four digits.|  
|%m|Month in two digits. For example, in this format 'September' would be represented as '09'.|  
|%d|Day in two digits.|  
|%H|Hour in two digits in the 24 hour format. For example, in this format '1 pm' would be represented as '13'|  
|%M|Minutes in two digits.|  
|%S|Seconds in two digits.|  
|%s|Milliseconds in three digits.|  
  
Here are some examples of dates and their corresponding timestamp format.  
  
|Date|Format|  
|--------|----------|  
|03\/26\/2010 14:07:46|%m\/%d\/%Y %H:%M:%S|  
|\[03\/26\/2010\] \[14:07:46\]|\[%m\/%d\/%Y\] \[%H:%M:%S|  
|15\-11\-10 02:09:45:056|%d\-%m\-%y %H:%M:%S:%s|  
  
### Published Data  
The following table lists the published data items.  
  
|Item|Description|  
|--------|---------------|  
|Full path and name of the log file|The full path of the log file that is being read.|  
|Number of lines matching the condition|The number of lines that were read.|  
|For each line read|  
|Full line matching the filter, including timestamp|The entire line as it appears in the log file.|  
|Timestamp of matching line|The timestamp of the line that was read.|  
|Message of matching line|The log message of the line that was read.|  
  
