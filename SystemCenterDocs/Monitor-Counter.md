---
title: Monitor Counter
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4994563d-6c43-4760-b6f7-ea009e535213
---
# Monitor Counter
The Monitor Counter activity invokes a runbook when a counter has reached a value that you specify. Each Monitor Counter activity monitors one counter.

Use the Monitor Counter activity to monitor a counter that counts the number of times that a runbook has attempted to start a service. When that number reaches the number that you configure in the Monitor Counter activity, the Monitor Counter activity can invoke a [Send Email](../Topic/Send-Email.md) activity to notify an administrator to investigate the problem.

## Configuring the Monitor Counter Activity
Before you configure the Monitor Counter activity, you need to determine the following:

-   The **Counter** you will be monitoring.

    > [!WARNING]
    > Before you can use this activity, you must configure a **Counter**.

-   The value that will invoke the runbook

Use the following information to configure the Monitor Counter activity.

### Published Data
The following table lists the published data items.

|Item|Description|
|--------|---------------|
|Counter Value|The value of the counter being monitored|

