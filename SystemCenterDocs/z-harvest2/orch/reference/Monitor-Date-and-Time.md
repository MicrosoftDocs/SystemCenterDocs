---
title: Monitor Date and Time
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e9baa069-6d81-43bc-8781-bdcc6d7ca5d3
author:bwren
manager:cfreemanwa
---
# Monitor Date and Time
The Monitor Date\/Time activity invokes runbooks at a time or interval that you specify. Use the Monitor Date\/Time activity to invoke your runbooks at a specific time once a day, week, or month. You can also schedule runbooks to be invoked when a specific number of seconds have passed since it was last invoked, or immediately after the runbook is deployed.  
  
The Monitor Date\/Time activity uses the system clock of the operating system on the computer that runs the runbook server, not Coordinated Universal Time \(UTC\), to verify the runbook’s launch time. This enables the Monitor Date\/Time activity to function in virtual machine environments, and to continue running even when the system clock is adjusted because of the move into or out of Daylight Saving Time. However, if a runbook is scheduled to start during an hour that is skipped when the system clock is adjusted forward by one hour, that starting time is skipped, and the runbook starts at the next scheduled time. If a runbook is scheduled to start during an hour that occurs twice because the system clock is adjusted backwards by one hour, the runbook launches twice.  
  
Depending on the practices in your time zone, the usual official time to change the system clocks at the start or finish of Daylight Saving Time is 2:00 A.M., or 02:00. We recommend that you configure a schedule to prevent your runbooks from being skipped or processed twice when the system clock changes.  
  
The Monitor Date\/Time activity becomes inactive when the schedule does not allow the runbook to run.  
  
The Monitor Date\/Time activity is best suited for scenarios where you need to run routines regularly that do not rely on events in other systems. For example, nightly backup procedures or periodically reading and processing mail in a customer service inbox.  
  
## Additional Use Cases  
The Monitor Date\/Time activity starts according to its configured interval and passes the runbook run to the Check Schedule activity. The Check Schedule activity verifies that the runbook is allowed to run at the current time.  
  
If the runbook is permitted to run at that time, the Check Schedule activity publishes a published data value of True. It passes the runbook run to the next activity if there is a link to the next activity with a invoke condition of “Conforms to schedule from Check Schedule equals true”. If the runbook is not permitted to run at that time, the Check Schedule activity publishes a published data value of False. It passes the runbook run to the next activity if there is a link to the next activity with an invoke condition of “Conforms to schedule from Check Schedule equals false.” This is useful when you want to implement conditional link branches according to the results of the Schedule verification.  
  
## Configuring the Monitor Date\/Time Activity  
Before you configure the Monitor Date\/Time activity, you need to determine the time or interval you want to use to invoke the runbook.  
  
Use the following the information to configure the Monitor Date\/Time activity.  
  
### Details Tab  
  
|Settings|Configuration Instructions|  
|------------|------------------------------|  
|**At**|Select an absolute time for the runbook to run. The Monitor Date\/Time activity will invoke every day at the time that you specify.|  
|**Every \[x\] days \[y\] hours \[z\] minutes**|Select to specify intervals of days, hours, and minutes for the runbook to run.<br /><br />**Starting**: Select to specify the number of minutes past the hour to invoke the runbook. This option is only available if you have specified 0 minutes and at least 1 **Day** or 1 **hour** .<br /><br />**At time slices within the hour**: Select to invoke the runbook at times that are multiples of **minutes** you have specified. This option is only available when 0 days and 0 hours are specified. For example, if **minutes** is set to 15 then the Monitor Date\/Time activity will invoke at 0, 15, 30, 45 minutes past each hour.<br /><br />**Trigger immediately**: Select to invoke the runbook immediately after deploying.|  
|**Every \[x\] seconds**|Select to specify the interval, in seconds, between each time the runbook is ran.|  
  
The Monitor Date\/Time activity accepts the following inputs when configuring times and intervals:  
  
### Configuring Time and Intervals  
  
|Unit|Accepted Input|  
|--------|------------------|  
|Seconds|5 \- 300|  
|Minutes|0 \- 59 \(0 is allowed only when hours\/days are also specified\)|  
|Hours|0 \- 23 \(0 is allowed when days\/minutes are also specified\)|  
|Days|0 \- 48 \(0 is allowed when hours\/minutes are also specified\)|  
|Time slices|1, 2, 3, 4, 5, 6, 10, 12, 15, 20, 30|  
  
### Published Data  
This activity does not generate published data items.  
  
