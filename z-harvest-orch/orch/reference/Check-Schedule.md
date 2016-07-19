---
title: Check Schedule
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3f949c61-c495-4639-aa71-d7ad0b197b74
author:bwren
manager:cfreemanwa
---
# Check Schedule
The Check schedule activity verifies that a runbook is allowed to run at the current time according to the permitted times or interval configured in a schedule. To use this activity, you can create a schedule and configure the permitted times, denied times, or interval at which the runbook can run. Then you can insert the activity into a runbook following a [Monitor Date and Time](../../orch/reference/Monitor-Date-and-Time.md) activity and configure it to check the schedule to verify whether a runbook is allowed to run at the current time. You can also use the Check Schedule activity in a runbook that monitors systems for availability. If a problem is encountered, the Check Schedule activity can verify whether the current time is during business hours, or in or out of a maintenance window.  
  
## Configuring the Check Schedule Activity  
Use the following information to configure the Check Schedule activity.  
  
#### To configure the Check Schedule activity  
  
1.  From the **Activity pane**, drag a **Check Schedule** activity to the runbook.  
  
2.  Double\-click the **Check Schedule** activity icon to open the **Properties** dialog box.  
  
3.  Select the **Details** tab, and next to the **Schedule Template** box, click the ellipsis **\(...\)** button and in the **Select a Schedule** dialog box, select the **Schedule** that you want to verify.  
  
### Published Data  
The following table lists published data items.  
  
|Item|Description|  
|--------|---------------|  
|Conforms to schedule|Determines whether the current time is within the schedule specified. This value can be either True or False.|  
  
