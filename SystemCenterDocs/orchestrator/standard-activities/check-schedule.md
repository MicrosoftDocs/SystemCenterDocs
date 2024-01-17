---
title: Check Schedule
description: This article describes the check schedule activity.
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 04/27/2023
ms.prod: system-center
ms.reviewer: ""
ms.suite: ""
ms.technology: orchestrator
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3f949c61-c495-4639-aa71-d7ad0b197b74
caps.latest.revision: 11
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
---
# Check Schedule

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

> [!IMPORTANT]
>
> This version of Orchestrator has reached the end of support. We recommend you to [upgrade to Orchestrator 2019](../index.yml).

::: moniker-end

The Check schedule activity verifies that a runbook is allowed to run at the current time according to the permitted times or interval configured in a schedule. To use this activity, you can create a schedule and configure the permitted times, denied times, or interval at which the runbook can run. Then you can insert the activity into a runbook following a [Monitor Date/Time](monitor-date-time.md) activity and configure it to check the schedule to verify whether a runbook is allowed to run at the current time. You can also use the Check Schedule activity in a runbook that monitors systems for availability. If a problem is encountered, the Check Schedule activity can verify whether the current time is during business hours or in or out of a maintenance window.  

## Configuring the Check Schedule Activity  
 Use the following information to configure the Check Schedule activity.  

#### To configure the Check Schedule activity  

1.  From the **Activity pane**, drag a **Check Schedule** activity to the runbook.  

2.  Double-click the **Check Schedule** activity icon to open the **Properties** dialog.  

3.  Select the **Details** tab, and next to the **Schedule Template** box, select the ellipsis **(...)** button and in the **Select a Schedule** dialog, select the **Schedule** that you want to verify.  

### Published Data  
 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Conforms to schedule|Determines whether the current time is within the schedule specified. This value can be either True or False.|