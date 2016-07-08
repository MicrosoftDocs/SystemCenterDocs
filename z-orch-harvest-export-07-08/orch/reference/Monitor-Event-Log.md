---
title: Monitor Event Log
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 244f37c3-48e0-46a4-b3bc-2bd7046ba544
author:bwren
manager:cfreemanwa
---
# Monitor Event Log
The Monitor Event Log activity invokes runbooks when new events that match a filter that you specify appear in the Windows Event Log. You can use the Monitor Event Log activity to run runbooks that will escalate, investigate, or correct any issues in response to events being generated to the Windows Event Log. For example, a security audit failure appears in the security log which will send an email to an administrator to notify them of the problem.  The second mode invokes your runbook when the size of the Windows Event Log reaches the maximum size allowed.  
  
## Configuring the Monitor Event Log Activity  
Before you configure the Monitor Event Log activity, you need to determine the following:  
  
-   Name of the event log you are monitoring  
  
-   Details about the events that will invoke the runbook  
  
Use the following steps to configure the Monitor Event Log activity.  
  
#### To configure the Monitor Event Log activity  
  
1.  From the **Activity pane**, drag a **Monitor Event Log** activity to the runbook.  
  
2.  Double\-click the **Monitor Event Log** activity icon to open the **Properties** dialog box.  
  
3.  Configure the settings on the **Details** tab and on the **Advanced** tab. Configuration instructions are listed in the following tables.  
  
### Details Tab  
  
|Settings|Configuration Instructions|  
|------------|------------------------------|  
|**Computer**|Type the name of the computer that stores the Windows Event Log that you want to monitor. You can also browse for the computer using the ellipsis **\(...\)** button. The runbook server that runs this activity must have the appropriate rights to monitor the Windows Event Log on that computer.|  
|**Event log**|Type the name of the Windows Event Log that you are monitoring. You can also browse for the Windows Event Log using the ellipsis **\(...\)** button. Windows includes three Event Logs by default: Application, Security, and System. The computer that you are connecting to may contain other Event Logs.|  
|**Message filters**|The list shows all the filters that have been configured to filter the events that are generated in the log that you have specified. To edit or remove an item in the list, select it and click **Edit** or **Remove** as applicable.<br /><br />**To add an event filter**<br />1.  Click **Add** to open the **Filter Properties** dialog box.<br />2.  Select the property of the event log entry that you are filtering against. You can filter against the **Category**, **Description**, **Event ID**, **Source**, and **Type** that is attributed to the event.<br />3.  Specify the relation you are using to compare the value of the event property to the filter value. If you select **Category**, **Description**, **Type**, and **Source** you can specify **Contains** or **Does not contain**. For **Event ID** you can specify **is different than**, **is equal to** , **is lower than**, **is lower than or equals**, **is more than**, and **is more than or equals**.<br />4.  Specify the filter value that you are comparing the event property against. For **Category**, **Description**, and **Source**, enter the string that is contained within the property. For **Event ID**, enter the numeric value that will be compared against the ID of the event. For the **Type** condition, select the specific type of event that you want to filter for such as **Error**, **Warning**, **Information**, **Success Audit**, or **Failure Audit**.|  
  
### Published Data  
The following table lists the published data items.  
  
|Item|Description|  
|--------|---------------|  
|Event log name|The name of the Windows Event Log being monitored.|  
|Computer|The name of the computer where the Windows Event Log is stored.|  
|Log entry description|The text that is contained in the Event Log entry description.|  
|Log Entry ID|The ID of the Event Log entry.|  
|Log Entry source|The source of the event.|  
|Log Entry computer|The computer where the event occurred.|  
|Log Entry type|The type of event.|  
|Log Entry date|The date the event was logged.|  
|Log Entry time|The time the event was logged.|  
  
