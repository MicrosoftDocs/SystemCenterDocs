---
title: Send Platform Event
description: This article describes the Send Platform Event activity that creates an activity event with text that you specify.
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: concept-article
ms.assetid: 58d4359b-155b-4406-8978-8b40fc87f5d0
caps.latest.revision: 15
author: jyothisuri
ms.author: jsuri
---
# Send Platform Event

The Send Platform Event activity creates an activity event with text that you specify. You can use the Send Platform Event activity to create notifications of any problems or general information that occur in the runbook.  

For more information about activity events, see [Activity Events](../activity-events.md).  

## Activity Properties  

### Details Tab  

|Settings|Configuration Instructions|  
|--------------|--------------------------------|  
|**Type**|Type of event to create. You can select from the following values:<br /><br /> -   Information<br />-   Warning<br />-   Error|  
|**Summary**|Summary of the event that displays in the list in the Events tab of the Runbook Designer. This has a limit of 200 characters.|  
|**Details**|Details of the event that display when the event is opened. This has a limit of 2,000 characters.|  

> [!WARNING]
> The Runbook Designer doesn't warn you when you configure this activity and you exceed the limits for the **Summary** or **Details** settings. If you exceed these limits, the Runbook Designer doesn't allow you to check-in the runbook and a generic error is shown. The runbook server generates an error if it attempts to process data that exceeds these limits.  

## Published Data  

|Item|Description|  
|----------|-----------------|  
|Type|The type of event that was generated.|  
|Summary|The summary text of the event.|  
|Details|The detailed description of the event.|
