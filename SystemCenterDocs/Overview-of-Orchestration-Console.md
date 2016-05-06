---
title: Overview of Orchestration Console
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9f2cd9f5-b177-4a9c-a7d8-9611c4d1e8aa
---
# Overview of Orchestration Console
The Orchestration console is comprised of a single webpage with multiple panes that are described in the following sections.

## Navigation pane
The navigation pane is the left pane in the Orchestration console where you can click the workspace that you want to use. Depending on the workspace you click, you can view specific data and use specific options. The following workspaces are available in the navigation pane.

## Runbooks workspace
The **Runbooks** workspace lets you start and stop runbooks. You can also view information such as the jobs and instances created for each runbook and their definition.

### Summary
The **Summary** tab is displayed for any folder or runbook selected in the **Runbooks** workspace. This tab displays summary information for the jobs and instances of the selected runbook or for all of the runbooks in the selected folder. The statistics that are displayed are updated every 10 minutes so that activity performed within that time might not be reflected in the numbers until they are updated.

Each column in the **Summary** displays the number of jobs and instances that finished with a particular status \(Succeeded, Warning, or Failed\) within the last hour, the last day, and the last week. For instances, the number of instances that are currently in progress are also displayed. For jobs, the number of jobs that have been created and that are currently queued are also displayed.

### Runbooks
The **Runbooks** tab is displayed when you select a folder in the **Runbooks** workspace. It lists the runbooks contained in the selected folder and specifies the status of any running jobs and instances from each. To select one of these runbooks and control their actions, click an option in the **Actions** pane. If you have a large number of runbooks, you can refine the list by specifying a filter.

### Jobs
The **Jobs** tab is displayed when you select a folder or runbook in the **Runbooks** workspace. This tab lists the jobs created for a given runbook and the completion status. For a folder, it lists the jobs created for all runbooks in the folder and their completion status. A job is a request for a runbook server to run a runbook and is created every time a runbook receives a request to run. If a runbook starts with a monitor, it creates a job that runs continuously until the runbook is stopped. In this case, the status of the job shows an hourglass that indicates it is currently running.

### Instances
The **Instances** tab is displayed when if you select a folder or runbook in the **Runbooks** workspace. For a runbook, this tab lists the instances that have been created for the runbook and their completion status. For a folder, it lists the instances that have been created for all runbooks in the folder and their completion status. An instance is a running copy of a runbook and is created each time that a runbook runs. If a runbook starts with a monitor, it creates an instance that continues to run until the monitor condition is met. In this case, the status for the instance shows an hourglass. When the monitor condition is met, the instance continues with the subsequent activities and then shows a completion status. The runbook then creates a new instance that also runs until the monitor condition is met.

## Runbook Servers workspace
The **Runbook Servers** workspace lets you view the status of current and completed jobs and instances for each runbook server.

### Jobs
The **Jobs** tab lists the jobs that have been run on the runbook server and their completion status. A job is a request for a runbook server to run a runbook and is created every time a runbook receives a request to run. If a runbook starts with a monitor, it creates a job that runs continuously until the runbook is stopped. In this case, the status of the job shows an hourglass, which means that it is currently running.

### Instances
The **Instances** tab lists the instances that have been created on the runbook server and their completion status. An instance is a running copy of a runbook and is created each time that a runbook runs. If a runbook starts with a monitor, it creates an instance that continues to run until the monitor condition is met. In this case, the status for the instance shows an hourglass. When the monitor condition is met, the instance continues with the subsequent activities, and then shows a completion status. The runbook then creates a new instance that also runs until the monitor condition is met.

## Events workspace
The **Events** workspace lets you view log events. By default, log events include all events for the management server and all runbook servers. To limit the events, click **Filter** and provide criteria to limit the events displayed. If an event is specific to a runbook server, it includes the name of the server in the **Source** box. In this case, you can select the event, and then click **View Runbook Server** in the **Actions** pane. Clicking **View Runbook Server** opens the **Jobs** tab in the **Runbook Servers** workspace for that runbook server.

## Starting and stopping runbooks
In addition to viewing the current status of a runbook, you can also start and stop a runbook from the Orchestration console. When you start a runbook, a job is created and waits for an available runbook server to process the runbook. If the first action in a runbook is a monitor, the job runs continuously, potentially producing multiple instances of a runbook, until the runbook or job is stopped. When a runbook server is available, the job provides an instance of the runbook to the runbook server to process. A running runbook has at least one job and one or more instances associated with it.

When you stop a runbook, the runbook, all jobs, and all instances associated with the runbook are stopped.

## Stopping jobs
A job is a request for a runbook to run. A job is created only when you request a runbook to run. If the first action in a runbook is a monitor, the job runs continuously until the runbook or job is stopped. An hourglass indicates the status of a running job. An instance is a running copy of a runbook.

You cannot start a job; you can only start a runbook.

When you view an instance, you can choose to stop the associated job. Stopping the job stops the instance, the job, any other associated instances, and the runbook.

## See Also
[Orchestration Console Browser Requirements](../Topic/Orchestration-Console-Browser-Requirements.md)
[How to Start the Orchestration Console](../Topic/How-to-Start-the-Orchestration-Console.md)
[How to Work With Runbooks in the Orchestration Console](../Topic/How-to-Work-With-Runbooks-in-the-Orchestration-Console.md)

