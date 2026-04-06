---
title: Monitor Counter
description: This article describes the Monitor Counter activity that invokes a runbook when a counter has reached a value that you specify.
ms.custom: UpdateFrequency3, engagement-fy23
ms.date: 11/01/2024
ms.update-cycle: 1095-days
ms.service: system-center
ms.reviewer: ""
ms.suite: ""
ms.subservice: orchestrator
ms.tgt_pltfrm: ""
ms.topic: concept-article
ms.assetid: 4994563d-6c43-4760-b6f7-ea009e535213
caps.latest.revision: 11
author: Jeronika-MS
ms.author: v-gajeronika
---
# Monitor Counter

The Monitor Counter activity invokes a runbook when a counter has reached a value that you specify. Each Monitor Counter activity monitors one counter.  

 Use the Monitor Counter activity to monitor a counter that counts the number of times that a runbook has attempted to start a service. When that number reaches the number that you configure in the Monitor Counter activity, the Monitor Counter activity can invoke a [Send Email](send-email.md) activity to notify an administrator to investigate the problem.  

## Configure the Monitor Counter Activity

 Before you configure the Monitor Counter activity, you need to determine the following:  

- The **Counter** you'll be monitoring.  

  > [!WARNING]
  > Before you can use this activity, you must configure a **Counter**.  

- The value that will invoke the runbook.

Use the following information to configure the Monitor Counter activity.  

### Published Data

The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Counter Value|The value of the counter being monitored.|
