---
title: Starting Point
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 570561e5-e42e-4056-8503-1fa5dd154053
---
# Starting Point
A runbook can only have one starting point. A starting point is an activity that automatically runs when the runbook is started. Each activity in the runbook runs after the previous activity in the workflow is completed.

If a runbook starts with any activity other than a monitor activity, the runbook begins processing and attempts to run  to completion. If the runbook starts with a monitoring activity, the monitor loads and waits for the trigger condition. When the condition is met, a runbook instance is created to run the remaining activities in the runbook. The monitor continues to run and waits for another occurrence of the trigger condition. Runbooks that start with monitors continue to run until you stop them from the Runbook Designer or Orchestration console.

## See Also
[Monitoring Activities](Monitoring-Activities.md)


