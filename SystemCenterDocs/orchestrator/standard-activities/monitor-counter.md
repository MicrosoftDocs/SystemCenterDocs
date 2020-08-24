---
title: "Monitor Counter | Microsoft Docs"
ms.custom: ""
ms.date: "05/13/2016"
ms.prod: system-center
ms.reviewer: ""
ms.suite: ""
ms.technology: orchestrator
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center 2012 SP1 - Orchestrator"
  - "System Center 2012 - Orchestrator"
  - "System Center 2012 R2 Orchestrator"
ms.assetid: 4994563d-6c43-4760-b6f7-ea009e535213
caps.latest.revision: 11
author: "bwren"
ms.author: "bwren"
manager: "cfreeman"
---
# Monitor Counter

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

> [!IMPORTANT]
>
> This version of Orchestrator has reached the end of support, we recommend you to [upgrade to Orchestrator 2019](https://docs.microsoft.com/system-center/orchestrator/?view=sc-orch-2019).

::: moniker-end

The Monitor Counter activity invokes a runbook when a counter has reached a value that you specify. Each Monitor Counter activity monitors one counter.  

 Use the Monitor Counter activity to monitor a counter that counts the number of times that a runbook has attempted to start a service. When that number reaches the number that you configure in the Monitor Counter activity, the Monitor Counter activity can invoke a [Send Email](send-email.md) activity to notify an administrator to investigate the problem.  

## Configuring the Monitor Counter Activity  
 Before you configure the Monitor Counter activity, you need to determine the following:  

- The **Counter** you will be monitoring.  

  > [!WARNING]
  >  Before you can use this activity, you must configure a **Counter**.  

- The value that will invoke the runbook  

Use the following information to configure the Monitor Counter activity.  

### Published Data  
 The following table lists the published data items.  

|Item|Description|  
|----------|-----------------|  
|Counter Value|The value of the counter being monitored|
