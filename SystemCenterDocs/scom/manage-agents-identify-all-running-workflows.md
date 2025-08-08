---
title: View All Rules and Monitors Running on an Agent-Managed Computer
description: This article describes how to view what workflows are running on an agent-managed computer in Operations Manager.
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.custom: UpdateFrequency2, engagement-fy24
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
ms.assetid: 5ec7aa58-3789-4589-a051-63fdd6f2dec1
---

# View all rules and monitors running on an agent-managed computer



Administrators for System Center Operations Manager sometimes want to know which rules and monitors are running on a computer. This is simple to do with the **Show Running Rules and Monitors for this Health Service** task.  

## View all rules and monitors running on a computer  

1. Open the Operations console and select **Monitoring**.  

2. For an agent-managed computer, navigate to the Operations Manager\Agent Details\Agent Health State view. For a management server, navigate to Operations Manager\Management Server\Management Servers State view.  

3. Select the agent you want to see rules and monitors for.  

4. In the **Tasks** pane, select the task **Show Running Rules and Monitors for this Health Service**.  

5. The **Run Task - Show Running Rules and Monitors for this Health Service** dialog appears. Select **Run**.  

6. The Task Status dialog appears. When the task is completed, you can select **Copy Text** or **Copy HTML** and paste the task output in the appropriate tool for further review.  

## Next steps

- If you've an agent-managed computer generating an alert that doesn't immediately help you understand what the cause behind it was, review [Identifying the Computer Experiencing a Problem](identifying-the-computer-experiencing-a-problem.md) for further recommendations.
