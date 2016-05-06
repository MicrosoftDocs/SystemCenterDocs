---
title: Runbook Tester
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ce993ecb-d4e2-41dd-91f6-1051507e28dd
---
# Runbook Tester
**Runbook Tester** lets you test runbooks in a debugging environment. You can run an entire runbook, step through it one activity at a time, or add breakpoints to stop the simulation at any activity you select. You start Runbook Tester from the toolbar above the central Design workspace in the **Runbook Designer**. When you click the Runbook Tester button, the Runbook Tester starts and loads the current runbook. The button is only enabled if the runbook is not currently running. You must stop the runbook before you can test it.

> [!IMPORTANT]
> Runbook Tester actually performs each activity within the workflow. The steps are not performed in a simulated or virtualized environment. All the connections referenced in the runbook are live and fully functional, so any activities that modify or destroy data in connected systems cause that data to be modified or destroyed. For example, if you use the **Query Database** activity to **DROP TABLE ImportantTable**, it actually deletes the **ImportantTable** from the instance of Microsoft SQL Server.

> [!IMPORTANT]
> Note that the account used to start the runbook must have permission on the local computer to run successfully. These permission requirements also apply when testing the runbook with the Runbook Tester. To successfully test your runbook, start the Runbook Designer **as Administrator**. By association, the Runbook Tester runs **as Administrator** and uses the higher\-level security token.

## Runbook Tester panes
The Runbook Tester interface is organized into the following four panes.

|Pane|Description|
|--------|---------------|
|**Run Time Properties**|Displays run\-time information, including resolved published data items, variables, and computer groups, about the activity that is currently being processed by Runbook Tester. Information appears in this pane when the runbook runs with breakpoints or in step\-through mode.|
|**Design Time Properties**|Displays design\-time information about each activity in the runbook when the runbook runs without breakpoints and is not run in step\-through mode. To view the design\-time properties of an activity, click an activity in the runbook. **Note:** You cannot edit the information that appears in the **Design Time Properties** pane.|
|**Workspace**|Displays the active runbook. You can select each activity to view its information in the **Design Time Properties** pane or to set a breakpoint on it.|
|**Log**|Displays information about each activity in the runbook as it runs. You can click the **Show Details** link to show the configuration details and published data from the activity.|
|**Resource Browser**|Displays the counters, variables, computers groups, and schedules that the runbook in the workspace uses.|

## See Also
[Tools](../Topic/Tools.md)

