---
title: Event Monitor Reset
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - operations-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d05005cc-56d7-4345-93be-09d836da44a1
author:markgalioto
---
# Event Monitor Reset
Unlike other kinds of monitors in [!INCLUDE[om12long](../../om/manage/includes/om12long_md.md)], it may be difficult to define the criteria to return an event monitor to a healthy state. This is because applications often generate an event when a problem occurs but do not create a corresponding event when the problem has been corrected. For this reason, you have the following options for setting the healthy state for an event monitor.  
  
|Reset Logic|Description|  
|---------------|---------------|  
|Event Reset|A single specific event indicates that monitor should be reset.|  
|Manual Reset|The monitor is never automatically reset. The user must manually reset the monitor.|  
|Timer Reset|The monitor is automatically reset after a specified time.|  
  
Each of these methods is discussed at length in the following sections:  
  
## Event Reset  
With *event reset*, the monitor is reset when a single occurrence of a specific event is detected. The event must be the same type as the event used for detecting the error condition. For example, a Windows event monitor might specify an event with a particular event source and number to indicate an error condition. Another Windows event with the same event source but a different number might indicate that the error in the application was corrected.  
  
Event reset can only be used if the application provides an event indicating the particular error was corrected. Many applications create an event when an error occurs but may not create a corresponding event that indicates that the error was corrected. Event reset cannot be used in this case.  
  
## Manual reset  
With *manual reset*, the monitor never returns to a healthy state automatically. The user must determine whether the problem was corrected and then select the monitor in the Health Explorer and select **Reset Health**.  
  
The advantage to this strategy is that a monitor can be used for issues that do not create an event that indicates a healthy state. The monitor can affect the health state of the managed object instead of creating a simple alert from a rule. The downtime will be recorded for the object in the State Change Events in the Operations Console and in any availability reports.  
  
There are multiple implications of this strategy that should be considered. The first is the additional work required from the user because the monitor will never automatically reset. It can also result in too much downtime being recorded if the user waits a long time before performing the reset. The problem may have been corrected fairly quickly, but the healthy state will not be recorded until the user performs the reset.  
  
Use of manual reset should be especially cautioned for monitors where there is a potential for a single problem to affect multiple instances of the target class. Because users cannot reset the monitor for multiple instances in the Operations Console, the user would be required to manually open the Health Explorer for each instance to perform this action. Depending on the number of instances, this could result in significant effort for the user.  
  
## Timer Reset  
A timer reset acts the same as a manual reset except that if the user does not manually reset the monitor after a specified time, it will reset automatically. One use of this kind of reset is for issues that continuously log error events until the problem is corrected. Instead of using another event to indicate that the problem was corrected, the previously detected error event for a specified period can be used as the success criteria.  
  
The timer reset can be used in the place of a manual reset providing the advantage of automatically resetting after a while if the user does not perform a manual reset.  
  
## Which reset should I use?  
  
-   If the application you’re monitoring creates an event when the problem has been corrected, use Event Reset. This is the preferred method since the monitor will return to a healthy state as soon as soon as is appropriate without any user intervention. Any alert generated from the monitor can also be closed automatically.  
  
-   If the application you’re monitoring does not create an event when the problem has been corrected, then you should use Manual Reset or Timer Reset. Refer to the descriptions of each above to determine which strategy is most appropriate for your specific purposes.  
  
## See Also  
[Event Monitors and Rules](../../om/manage/Event-Monitors-and-Rules.md)  
[Windows Events](../../om/manage/Windows-Events.md)  
[Text Logs](../../om/manage/Text-Logs.md)  
  
