---
title: Overview of Orchestration Console
desc: Provides a summary of the administrative console for Orchestrator and basic functionality procedures. 
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.author: cfreeman
ms.date: 10/12/2016
author: cfreemanwa
manager: carmonm
---
# Overview of the Orchestration console for System Center 2016 - Orchestrator

> Applies To: System Center 2016 - Orchestrator

The Orchestration console is comprised of a single webpage made up of multiple panes and workspaces. This topic describes those panes and workspaces and includes procedures for accessing the console and managing runbooks.  

## Navigation pane  
The navigation pane is the left pane in the Orchestration console where you can click the workspace that you want to use. Depending on the workspace you click, you can view specific data and use specific options. The following workspaces are available in the navigation pane.  

### Runbooks workspace  
The **Runbooks** workspace lets you start and stop runbooks. You can also view information such as the jobs and instances created for each runbook and their definition.  

#### Summary  
The **Summary** tab is displayed for any folder or runbook selected in the **Runbooks** workspace. This tab displays summary information for the jobs and instances of the selected runbook or for all of the runbooks in the selected folder. The statistics that are displayed are updated every 10 minutes so that activity performed within that time might not be reflected in the numbers until they are updated.  

Each column in the **Summary** displays the number of jobs and instances that finished with a particular status \(Succeeded, Warning, or Failed\) within the last hour, the last day, and the last week. For instances, the number of instances that are currently in progress are also displayed. For jobs, the number of jobs that have been created and that are currently queued are also displayed.  

#### Runbooks  
The **Runbooks** tab is displayed when you select a folder in the **Runbooks** workspace. It lists the runbooks contained in the selected folder and specifies the status of any running jobs and instances from each. To select one of these runbooks and control their actions, click an option in the **Actions** pane. If you have a large number of runbooks, you can refine the list by specifying a filter.  

#### Jobs  
The **Jobs** tab is displayed when you select a folder or runbook in the **Runbooks** workspace. This tab lists the jobs created for a given runbook and the completion status. For a folder, it lists the jobs created for all runbooks in the folder and their completion status. A job is a request for a runbook server to run a runbook and is created every time a runbook receives a request to run. If a runbook starts with a monitor, it creates a job that runs continuously until the runbook is stopped. In this case, the status of the job shows an hourglass that indicates it is currently running.  

#### Instances  
The **Instances** tab is displayed when if you select a folder or runbook in the **Runbooks** workspace. For a runbook, this tab lists the instances that have been created for the runbook and their completion status. For a folder, it lists the instances that have been created for all runbooks in the folder and their completion status. An instance is a running copy of a runbook and is created each time that a runbook runs. If a runbook starts with a monitor, it creates an instance that continues to run until the monitor condition is met. In this case, the status for the instance shows an hourglass. When the monitor condition is met, the instance continues with the subsequent activities and then shows a completion status. The runbook then creates a new instance that also runs until the monitor condition is met.  

### Runbook Servers workspace  
The **Runbook Servers** workspace lets you view the status of current and completed jobs and instances for each runbook server.  

#### Jobs  
The **Jobs** tab lists the jobs that have been run on the runbook server and their completion status. A job is a request for a runbook server to run a runbook and is created every time a runbook receives a request to run. If a runbook starts with a monitor, it creates a job that runs continuously until the runbook is stopped. In this case, the status of the job shows an hourglass, which means that it is currently running.  

#### Instances  
The **Instances** tab lists the instances that have been created on the runbook server and their completion status. An instance is a running copy of a runbook and is created each time that a runbook runs. If a runbook starts with a monitor, it creates an instance that continues to run until the monitor condition is met. In this case, the status for the instance shows an hourglass. When the monitor condition is met, the instance continues with the subsequent activities, and then shows a completion status. The runbook then creates a new instance that also runs until the monitor condition is met.  

### Events workspace  
The **Events** workspace lets you view log events. By default, log events include all events for the management server and all runbook servers. To limit the events, click **Filter** and provide criteria to limit the events displayed. If an event is specific to a runbook server, it includes the name of the server in the **Source** box. In this case, you can select the event, and then click **View Runbook Server** in the **Actions** pane. Clicking **View Runbook Server** opens the **Jobs** tab in the **Runbook Servers** workspace for that runbook server.  

## To start the Orchestration console in a browser  

1.  Open your browser.  

2.  In the address bar, type **http:\/\/<computer name>:<port number>** where computer name is the name of the server where the web service is installed, and port is the port number selected during configuration of the web service. By default, the port is 82.  

## To start the Orchestration console in the Runbook Designer  

-  Click the **Orchestration Console** button on the toolbar.  

    > [!NOTE]  
    > If the URL has not been set for the Orchestration console, you will receive an error message. Use the following procedure to set the URL.  

## To set the Orchestration console URL in the Runbook Designer  

1.  Select **Options**, and then select **Orchestration Console**.  

2.  In the **URL** box, type **http:\/\/<computer name>:<port number>** where computer name is the name of the server where the web service is installed, and port is the port number selected during configuration of the web service. By default, the port is 82.  

3.  Click **Finish**. 

## Starting and stopping runbooks  
In addition to viewing the current status of a runbook, you can also start and stop a runbook from the Orchestration console. When you start a runbook, a job is created and waits for an available runbook server to process the runbook. If the first action in a runbook is a monitor, the job runs continuously, potentially producing multiple instances of a runbook, until the runbook or job is stopped. When a runbook server is available, the job provides an instance of the runbook to the runbook server to process. A running runbook has at least one job and one or more instances associated with it.  

When you stop a runbook, the runbook, all jobs, and all instances associated with the runbook are stopped.  

### To start a runbook

1.  Click **Runbooks** to open the **Runbooks** workspace.

2.  If the runbook is located in a folder, select the folder in the **Runbooks** pane.

3.  Click the **Runbooks** tab in the results pane.

4.  Select the runbook, and then in the **Actions** pane, click **Start Runbook**.

5.  If the runbook requires parameters, they are listed in the **Runbook Parameters** pane. Click the **Value** column for each runbook and type a value for the runbook to use.

6.  If you want to run the runbook on a server other than its default, click a server in the **Available Runbook Server(s)** pane, and then click the right arrow to add the server to the **Selected Runbook Server(s)** pane.

    > [!NOTE]
    > If you add multiple servers to the **Selected Runbook Server(s)** pane, the runbook runs only on the first server if it is available. The other servers are backup servers where the runbook runs only if the primary server is not available.

7.  Click **Start**.

### To stop a runbook

1.  Click **Runbooks** to open the **Runbooks** workspace.

2.  If the runbook is located in a folder, select the folder in the **Runbooks** pane.

3.  Click the **Runbooks** tab in the results pane.

4.  Select the runbook, and then in the **Actions** pane, click **Stop Runbook**.

5.  Click **OK** to the message to confirm that you want to stop the jobs.

6.  If the runbook was started successfully, you receive a confirmation message that the job was stopped. If the runbook has no running jobs, you receive a message that no job was running.

### To view the status of a runbook in the Orchestration console

1.  Click **Runbooks** to open the **Runbooks** workspace.

2.  If the runbook is located in a folder, select the folder in the **Runbooks** pane.

3.  Select the **Runbooks** tab in the results pane.

4.  Select the runbook.

5.  To view all jobs that the runbook created, in the **Actions** pane, select **View Jobs**.

6.  To view all instances that the runbook created, in the **Actions** pane, select **View Instances**.

## Stopping jobs  
A job is a request for a runbook to run. A job is created only when you request a runbook to run. If the first action in a runbook is a monitor, the job runs continuously until the runbook or job is stopped. An hourglass indicates the status of a running job. An instance is a running copy of a runbook.  

You cannot start a job; you can only start a runbook.  

When you view an instance, you can choose to stop the associated job. Stopping the job stops the instance, the job, any other associated instances, and the runbook.  
  
## Next steps

- To learn more about deploying runbooks see [Deploy runbooks](../deploy/deploy-runbooks.md)