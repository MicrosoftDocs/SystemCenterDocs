---
ms.assetid: b35a0bd5-12b2-4c55-9c47-7eb2a36eccb1
title: Running Tasks in Operations Manager
description: This article describes how to run a task from the Operations console to help investigate and resolve issues detected.  
author: mgoedtel
ms.author: magoedte
manager: cfreemanwa
ms.date: 11/15/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Running tasks in Operations Manager

>Applies To: System Center 2016 - Operations Manager

In the System Center 2016 - Operations Manager Operations console, the **Tasks** pane provides links to tasks. A task is a user-initiated action from the Operations console that is run on an Operations Manager agent or on the computer where the Operations console is launched from. The tasks that are available depend on the management packs that are installed. For example, Operations Manager comes with a core set of functionality that provides the ping task. When you install the SQL Server management pack, it adds SQL-specific tasks, such as a task to start or stop the SQL Server agent.  
  
> [!NOTE]  
> If the **Tasks** pane is not displayed, click **Tasks** on the toolbar to display it.  
  
Click an alert or object to see tasks for that alert or object. Click a task to run the task.  
  
![Example of tasks](../media/om2016-tasks-pane.png)  
  
In the example above, if you click the task **Display Local Users**, you see a **Run Task** dialog box:  
  
![Example of a run tasks dialog box](../media/om2016-task-run-properties.png)  
  
Tasks use the default action account, unless you specify other credentials in this dialog box. Tasks can also be configured by a management pack author to use a specific Run As profile.  
  
Generally, you should accept the defaults and click **Run**. You will then see a **Task Status** window:  
  
![Example of a task status window](../media/om2016-task-results.png)  
  
In this instance, the task completed successfully. **Task Output** provides you with the results of the task, in this case it will return all of the user accounts defined on the server.
  
## Next steps

- To stop monitoring of a computer, group of computers or monitored object temporarily during planned maintenance using a schedule, or to stop monitoring while troubleshooting an issue, see [How to Suspend Monitoring Temporarily by Using Maintenance Mode](How-to-Suspend-Monitoring-Temporarily-by-Using-Maintenance-Mode.md). 

- Groups help categorize, classify or arrange one or more monitored objects to manage targeting of visualized data, overrides, reports, and more.  To learn how to create groups and common uses for groups, see [Creating and Managing Groups](Creating-and-Managing-Groups.md).    

- Operations Manager extends the PowerShell command-line environment and task-based scripting technology to automate most Operations Manager administrative tasks.  See [Using Operations Manager Shell](Using-Operations-Manager-Shell.md).  
  
