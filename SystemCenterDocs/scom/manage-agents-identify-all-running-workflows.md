---
title: How to View All Rules and Monitors Running on an Agent-Managed Computer
description: This article describes how to view what workflows are running on an agent-managed computer in Operations Manager.
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 12/13/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
ms.assetid: 5ec7aa58-3789-4589-a051-63fdd6f2dec1
---

# How to view all rules and monitors running on an agent-managed computer

Administrators for System Center 2016 - Operations Manager sometimes want to know which rules and monitors are running on a computer. This is simple to do with the **Show Running Rules and Monitors for this Health Service** task.  
  
## To view all rules and monitors running on a computer  
  
1.  Open the Operations console and click **Monitoring**.  
  
2.  For an agent-managed computer, navigate to the Operations Manager\Agent Details\Agent Health State view.  For a management server, navigate to Operations Manager\Management Server\Management Servers State view.  
  
3.  Click the agent you want to see rules and monitors for.  
  
4.  In the **Tasks** pane, select the task **Show Running Rules and Monitors for this Health Service**.  
  
5.  The **Run Task - Show Running Rules and Monitors for this Health Service** dialog box appears. Click **Run**.  
  
6.  The Task Status dialog box appears. When the task is completed, you can click **Copy Text** or **Copy HTML** and paste the task output in the appropriate tool for further review.  
  

## Next steps

- If you have an agent-managed computer generating an alert that doesn't immediately help you understand what the cause behind it was, review [Identifying the Computer Experiencing a Problem](identifying-the-computer-experiencing-a-problem.md) for further recommendations.    
