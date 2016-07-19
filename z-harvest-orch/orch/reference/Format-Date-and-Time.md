---
title: Format Date and Time
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0148fedb-ffba-462f-a8fb-49778b4210f2
author:bwren
manager:cfreemanwa
---
# Format Date and Time
The Format Date\/Time activity enables you to transform existing date and time formats into custom formats that you create.  
  
## Configuring the Format Date\/Time Activity  
Before you configure the Format Date\/Time activity, you need to determine the following:  
  
-   The existing date and time format you want to transform.  
  
-   The new date and time format you want it to become.  
  
Use the following information to configure the Format Date\/Time activity.  
  
### Details Tab  
  
|Settings|Configuration Instructions|  
|------------|------------------------------|  
|**Date\/Time**|Type the time that you want to convert.|  
|**Format**|Type the format of the time that you want to convert. See the Date\/Time Format Codes table for format codes and examples.|  
|**Format**|Type the format that you want to convert the input time to.|  
|**Output Adjustments**|Type a number in any of the following fields to adjust the output time from the input time. For example, if the input time is coming from a server that is three hours ahead of your local time, type \-3 in the Hours field to set the output time \(your local time\) to three hours behind the input time. If the input time is three hours behind your local time, type 3 to set the output time to three hours ahead of the input time.<br /><br />You can adjust the output time using the following time units:<br /><br />Days<br /><br />Months<br /><br />Years<br /><br />Hours<br /><br />Minutes<br /><br />Seconds|  
  
To specify a date\/time format, you must enter the codes that represent each part of the date and time.  
  
### Date\/Time Format Codes  
  
|Code|Description|  
|--------|---------------|  
|y|The last digit of the year. For example, 2005 would be represented as 5.|  
|yy|The last two digits of the year number. For example, in this format 2005 would be represented as 05.|  
|yyyy|The year number in four digits. For example, in this format 2005 would be represented as 2005.|  
|M|Month as a number from 1 to 12. If the month number is a single\-digit number, it is displayed without a leading zero.|  
|MM|Month in two digits. If the month number is a single\-digit number, it is displayed with a leading zero.|  
|MMM|The name of the month in three letters. For example, August would be represented as Aug.|  
|MMMM|The name of the month spelled in full. This format is supported only for output time. **Note:** This format is only supported for the output format.|  
|d|Day as a number from 1 to 31. If the day number is a single\-digit number, it is displayed without a leading zero.|  
|dd|Day in two digits. If the day number is a single\-digit number, it is displayed with a leading zero.|  
|ddd|The abbreviated name of the day of the week in three letters. For example, Saturday is abbreviated as “Sat”.|  
|dddd|The full name of the day of the week. For example, Saturday is displayed in full. **Note:** This format is only supported for the output format.|  
|h|Hour as a number from 1 to 12 when using the 12\-hour clock. If the hour number is a single\-digit number, it is displayed without a leading zero.|  
|hh|Hour in two digits using the 12\-hour clock. If the hour number is a single\-digit number, it is displayed with a leading zero.|  
|H|Hour as a number from 0 to 23 when using the 24\-hour clock. For example, in this format 1 pm would be represented as 13. If the hour number is a single\-digit number, it is displayed without a leading zero.|  
|HH|Hour in two digits using the 24\-hour clock. For example, in this format 1 pm would be represented as 13. If the hour number is a single\-digit number, it is displayed with a leading zero|  
|m|Minutes as a number from 0 to 59. If the minute number is a single\-digit number, it is displayed without a leading zero.|  
|mm|Minutes in two digits. If the minute number is a single\-digit number, it is displayed with a leading zero.|  
|s|Seconds as a number from 0 to 59. If the second number is a single\-digit number, it is displayed without a leading zero.|  
|ss|Seconds in two digits. If the second number is a single\-digit number, it is displayed with a leading zero.|  
|tt|A.M. or P.M. as two letters: A.M. or P.M. as defined on your system.|  
  
Here are some examples of dates and times and their corresponding format:  
  
|Format|Date|  
|----------|--------|  
|MM\/dd\/yyyy hh:mm:ss tt|08\/05\/2006 03:05:15 PM|  
|M\/d\/yy h:m:s tt|8\/5\/06 3:5:15 PM|  
|ddd MMM dd yyyy|Sat Aug 05 2006|  
|dddd, MMMM dd yyyy|Saturday, August 05 2006|  
  
### Published Data  
The following table lists the published data items.  
  
|Item|Description|  
|--------|---------------|  
|Format Result|The result of the format in the specified form.|  
|Format Result without adjustments|The formatted result, but without any adjustments made to it.|  
|Input Time|The input time.|  
|Input Format|The format of the date and time that was entered as the input time.|  
|Output Format|The format of the date and time that was entered as the output time.|  
  
