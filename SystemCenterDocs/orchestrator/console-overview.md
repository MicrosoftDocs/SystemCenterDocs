---
title: Overview of Orchestration Console
description: This article provides a summary of the administrative console for Orchestrator and basic functionality procedures.
ms.prod: system-center
ms.reviewer: na
ms.suite: na
ms.technology: orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.author: jsuri
ms.date: 07/05/2023
author: jyothisuri
manager: mkluck
---
# Overview of the Orchestration console

::: moniker range=">= sc-orch-1801 <= sc-orch-1807"

[!INCLUDE [eos-notes-orchestrator.md](../includes/eos-notes-orchestrator.md)]

::: moniker-end

::: moniker range="sc-orch-2022"

The Orchestrator console is a Single Page App that helps you monitor and execute your Orchestrator deployment. This article details the supported features in the Orchestrator 2022 console.

:::image type="content" source="./media/console-overview-2022/dashboard-inline.png" alt-text="Screenshot showing the dashboard." lightbox="./media/console-overview-2022/dashboard-expanded.png":::

## Navigation pane

The Navigation pane on the left shows the **Runbook** and **Folders** tree, like the one shown on the **Runbook Designer**. Unlike the console in earlier versions, you can't select the *Folders*, but you select the *Runbooks* and view their jobs and execute them.

The Navigation pane is always visible on all the screens to allow quick navigation to other runbooks and folders while remaining on the same screen.

To the right of the navigation pane, you can see the chosen screen. The Dashboard screen is shown by default.

>[!NOTE]
>Currently, auto-refresh isn't supported for any of the screens. Reload the page manually.


## Dashboard

The Dashboard shows **Active jobs** on the top followed by a table of all the **Completed jobs (history)**. The **Completed jobs (history)** pane is collapsed by default, allowing focus on the active jobs.

:::image type="content" source="./media/console-overview-2022/dashboard-history-inline.png" alt-text="Screenshot showing the dashboard history." lightbox="./media/console-overview-2022/dashboard-history-expanded.png":::

Each row in both the panels corresponds to a unique job. A job may have one or more runbook instances. Each row shows:
- **Job ID**: Link to the Runbook
- **Timestamps**: The number of successful and failed instances is shown in one of the columns for all rows.
- **Action buttons**: Stop job or View Job details

You can select and expand each of the job rows and view the instances of the job.

## Runbooks

When you select a runbook on the navigation tree or select a runbook link, the app navigates to the Runbook screen. The top panel lists out runbook metadata (editing status, timestamps, and so on). The **Run** button available on the screen allows you to queue the runbook for execution on the desired subset of runbook servers. The **Run** button is disabled for runbooks that aren't in **Published** state.

:::image type="content" source="./media/console-overview-2022/runbook-view-inline.png" alt-text="Screenshot showing runbook view." lightbox="./media/console-overview-2022/runbook-view-expanded.png":::

Below this panel is a tabbed view:

- **View**: For the Runbook graphical image.
- **Jobs**: For the list of active and completed jobs of the runbook (see below).
- **Instances**: For the list of active and completed instances of the runbook across all its Jobs (see below).

You can select the rows in the Jobs view just like the ones on the Dashboard screen. Jobs that are running can be stopped using the buttons on the right of the running row.

:::image type="content" source="./media/console-overview-2022/runbook-jobs-2-inline.png" alt-text="Screenshot showing runbook jobs." lightbox="./media/console-overview-2022/runbook-jobs-2-expanded.png":::

:::image type="content" source="./media/console-overview-2022/runbook-instances-inline.png" alt-text="Screenshot showing runbook instances." lightbox="./media/console-overview-2022/runbook-instances-expanded.png":::

While this screen is active, you can choose a different runbook on the Navigation tree. This won't change the selected tab. You can quickly look at Jobs of different runbooks by selecting the jobs tab and navigating to the desired runbooks in the Navigation tree.

## Jobs

When you select a job (using the (i) button), the app navigates to this screen. The top panel shows the job’s metadata (timestamps, parameters).

A table that shows the Instances of this job follows the panel.

:::image type="job details" source="./media/console-overview-2022/job-details-inline.png" alt-text="Screenshot showing job details." lightbox="./media/console-overview-2022/job-details-expanded.png":::

Most jobs have a single Instance. If the runbook has a Monitor/Event trigger activity, then each trigger starts a unique job instance. The screenshot below shows a Job with more than one Instance.

:::image type="instances of jobs" source="./media/console-overview-2022/instances-of-jobs-inline.png" alt-text="Screenshot showing instances of jobs." lightbox="./media/console-overview-2022/instances-of-jobs-expanded.png":::

>[!NOTE]
>A Job can have at most one running Instance at any time. But since a Runbook can have many concurrently running Jobs, a Runbook can have more than one running Instance.

The status of the job is shown visually with the icons:

- **Three dots**: Job is queued
- **Hourglass**: Job is running
- **Circle with slash**: Job was canceled
- **Tick**: Job completed successfully
- **Red exclamation**: Job completed but failed
- **Warning**: Job completed with warning(s)

## Instances

When you select an Instance (using the (i) button), the app navigates to this screen. The top panel shows the Instance's metadata (Job ID, timestamps, parameters, server that executes this instance).

:::image type="content" source="./media/console-overview-2022/instance-inline.png" alt-text="Screenshot showing instance." lightbox="./media/console-overview-2022/instance-expanded.png":::

The top panel also has three navigation buttons:

- **Previous**: View Instance that ran before this one.
- **Next**: View Instance that ran after this one.
- **Latest**: View most current instance

:::image type="runbook instance details" source="./media/console-overview-2022/runbook-instance-details-inline.png" alt-text="Screenshot showing runbook instance details." lightbox="./media/console-overview-2022/runbook-instance-details-expanded.png":::

:::image type="runbook details" source="./media/console-overview-2022/runbook-instance-details-1-inline.png" alt-text="Screenshot showing runbook details." lightbox="./media/console-overview-2022/runbook-instance-details-1-expanded.png":::

>[!NOTE]
> The job ID is the same, and since the second instance is still running, the job is also still running.

Below the panel, you see the runbook diagram. You can select each runbook activity to view activity outputs. An icon dedicated for each activity denotes the status of that activity. When you select any activity, an overlay is shown on the right that lists the activity’s outputs.

Since an activity may be executed more than once within an instance (because of looping), each execution of the Activity has a unique **Sequence number**. The overlay lets you choose the **Sequence #** using the dropdown on the top.

:::image type="content" source="./media/console-overview-2022/instance-detail-inline.png" alt-text="Screenshot showing instance detail." lightbox="./media/console-overview-2022/instance-detail-expanded.png":::

>[!NOTE]
>To ensure fast load time, only the first 10 activity outputs are loaded for the activity. The **Load more** button shows how many times this activity was executed, and you can select it to load more outputs.

The **Instance** and **Activity status** follow the same format as **Job Status**.

## Execute runbooks

Navigate to the Runbook screen of the desired Runbook and select **Run**. An overlay form opens to the right where you're asked to:
- Set values to all input parameters (required)
- Choose the set of Runbook servers on which this Job can be scheduled.

:::image type="content" source="./media/console-overview-2022/parameterized-run-inline.png" alt-text="Screenshot showing parameterized run." lightbox="./media/console-overview-2022/parameterized-run-expanded.png":::

Only one of these servers will actually execute this Job. To execute a Runbook on many servers, you'll have to run those many number of Jobs and explicitly set the servers one by one.

>[!NOTE]
> Enter the parameters in the form, else the form won't be considered.

When the form is submitted, a disappearing popup is shown on the top right to notify whether the job was successfully queued or not.

:::image type="job queue notification" source="./media/console-overview-2022/job-queue-notification.png" alt-text="Screenshot showing job queue notification.":::

## Stop running Jobs

The **Stop** button is shown on the Dashboard and the Job screen. Disappearing popup on the top right notifies whether the Job is stopped or not.

:::image type="job stop notification" source="./media/console-overview-2022/job-stop-notification.png" alt-text="Screenshot showing job stop notification.":::


## FAQs

### The Console doesn't load; error “Uh oh! Trouble connecting to WebApi [status 0]” appears

1. Check the [browser’s developer console](/microsoft-edge/devtools-guide-chromium/overview) (Console tab), look for CORS errors (*blocked by CORS policy*).

    :::image type="content" source="./media/console-overview-2022/error-console-inline.png" alt-text="Screenshot showing error console." lightbox="./media/console-overview-2022/error-console-expanded.png":::


2. If there are no CORS errors, check the **Event Viewer** logs (Application) on the Web API computer.

To fix CORS errors, you must ensure that the API’s `web.config` file must have a suitable CORS configuration. The browser error shows the origin value it is expecting in the Web API's `web.config`. Although domain names are case-insensitive, IIS CORS uses case-sensitive comparison test. Ensure that the `origin` value is in lowercase in the IIS CORS config.

> [!TIP] 
> A typical Web API IIS CORS config:
> ```xml
> <add allowCredentials="true" maxAge="7200" origin="http://{domain}[:{port}]">
>   <allowMethods>
>     <add method="GET"/>
>     <add method="PUT"/>
>     <add method="POST"/>
>     <add method="PATCH"/>
>     <add method="DELETE"/>
>   </allowMethods>
>   <allowHeaders allowAllRequestedHeaders="true"/>
> </add>
> ```

For details on how to configure CORS in `web.config`, see this article on [CORS Module Configuration](/iis/extensions/cors-module/cors-module-configuration-reference).

### How do I update the Web API URL?

The Console loads *{install_dir}\assets\configuration.json* to find the API URL. You can edit it using a plain text editor. Ensure that there's no trailing / at the end of the URL.

::: moniker-end

::: moniker range="<=sc-orch-2019"

The Orchestration console is a single webpage made up of multiple panes and workspaces. This article describes those panes and workspaces and includes procedures for accessing the console and managing runbooks.  

## Navigation pane  
The navigation pane is the left pane in the Orchestration console where you can select the workspace that you want to use. Depending on the workspace you select, you can view specific data and use specific options. The following workspaces are available in the navigation pane.  

### Runbooks workspace  
The **Runbooks** workspace lets you start and stop runbooks. You can also view information such as the jobs and instances created for each runbook and their definition.  

#### Summary  
The **Summary** tab is displayed for any folder or runbook selected in the **Runbooks** workspace. This tab displays summary information for the jobs and instances of the selected runbook or for all the runbooks in the selected folder. The statistics that are displayed are updated every 10 minutes, so the activity performed within that time might not be reflected in the numbers until they're updated.  

Each column in the **Summary** displays the number of jobs and instances that finished with a particular status \(Succeeded, Warning, or Failed\) within the last hour, the last day, and the last week. For instances, the number of instances that are currently in progress are also displayed. For jobs, the number of jobs that have been created and that are currently queued are also displayed.  

#### Runbooks  
The **Runbooks** tab is displayed when you select a folder in the **Runbooks** workspace. It lists the runbooks contained in the selected folder and specifies the status of any running jobs and instances from each. To select one of these runbooks and control their actions, select an option in the **Actions** pane. If you have a large number of runbooks, you can refine the list by specifying a filter.  

#### Jobs  
The **Jobs** tab is displayed when you select a folder or runbook in the **Runbooks** workspace. This tab lists the jobs created for a given runbook and the completion status. For a folder, it lists the jobs created for all runbooks in the folder and their completion status. A job is a request for a runbook server to run a runbook and is created every time a runbook receives a request to run. If a runbook starts with a monitor, it creates a job that runs continuously until the runbook is stopped. In this case, the status of the job shows an hourglass that indicates it's currently running.  

#### Instances  
The **Instances** tab is displayed if you select a folder or runbook in the **Runbooks** workspace. For a runbook, this tab lists the instances that have been created for the runbook and their completion status. For a folder, it lists the instances that have been created for all runbooks in the folder and their completion status. An instance is a running copy of a runbook and is created each time that runbook runs. If a runbook starts with a monitor, it creates an instance that continues to run until the monitor condition is met. In this case, the status for the instance shows an hourglass. When the monitor condition is met, the instance continues with the subsequent activities and then shows a completion status. The runbook then creates a new instance that also runs until the monitor condition is met.  

### Runbook Servers workspace  
The **Runbook Servers** workspace lets you view the status of current and completed jobs and instances for each runbook server.  

#### Jobs  
The **Jobs** tab lists the jobs that have been run on the runbook server and their completion status. A job is a request for a runbook server to run a runbook and is created every time a runbook receives a request to run. If a runbook starts with a monitor, it creates a job that runs continuously until the runbook is stopped. In this case, the status of the job shows an hourglass, which means that it's currently running.  

#### Instances  
The **Instances** tab lists the instances that have been created on the runbook server and their completion status. An instance is a running copy of a runbook and is created each time that runbook runs. If a runbook starts with a monitor, it creates an instance that continues to run until the monitor condition is met. In this case, the status for the instance shows an hourglass. When the monitor condition is met, the instance continues with the subsequent activities, and then shows a completion status. The runbook then creates a new instance that also runs until the monitor condition is met.  

### Events workspace  
The **Events** workspace lets you view log events. By default, log events include all events for the management server and all runbook servers. To limit the events, select **Filter** and provide criteria to limit the events displayed. If an event is specific to a runbook server, it includes the name of the server in the **Source** box. In this case, you can select the event, and then select **View Runbook Server** in the **Actions** pane. Selecting **View Runbook Server** opens the **Jobs** tab in the **Runbook Servers** workspace for that runbook server.  

## Start the Orchestration console in a browser  

1.  Open your browser.  

2.  In the address bar, enter `http://computer name/:port number` where computer name is the name of the server where the web service is installed and port is the port number selected during configuration of the web service. By default, the port is 82.  

## Start the Orchestration console in the Runbook Designer  

Select the **Orchestration Console** button on the toolbar.  

> [!NOTE]  
> If the URL hasn't been set for the Orchestration console, you'll receive an error message. Use the following procedure to set the URL.  

## Set the Orchestration console URL in the Runbook Designer  

1.  Select **Options**, and then select **Orchestration Console**.  

2.  In the **URL** box, enter `http://computer name:port number` where computer name is the name of the server where the web service is installed and port is the port number selected during configuration of the web service. By default, the port is 82.  

3.  Select **Finish**.

## Start and stop runbooks  

In addition to viewing the current status of a runbook, you can also start and stop a runbook from the Orchestration console. When you start a runbook, a job is created and waits for an available runbook server to process the runbook. If the first action in a runbook is a monitor, the job runs continuously, potentially producing multiple instances of a runbook, until the runbook or job is stopped. When a runbook server is available, the job provides an instance of the runbook to the runbook server to process. A running runbook has at least one job and one or more instances associated with it.  

When you stop a runbook, the runbook, all the jobs, and the all instances associated with the runbook are stopped.  

Select the required tab for steps to start, stop, or view the status of a runbook:

# [Start a runbook](#tab/Start)

Follow these steps to start a runbook:

1.  Select **Runbooks** to open the **Runbooks** workspace.

2.  If the runbook is located in a folder, select the folder in the **Runbooks** pane.

3.  Select the **Runbooks** tab in the results pane.

4.  Select the runbook, and then in the **Actions** pane, select **Start Runbook**.

5.  If the runbook requires parameters, they're listed in the **Runbook Parameters** pane. Select the **Value** column for each runbook and enter a value for the runbook to use.

6.  If you want to run the runbook on a server other than its default, select a server in the **Available Runbook Server(s)** pane, and then select the right arrow to add the server to the **Selected Runbook Server(s)** pane.

    > [!NOTE]
    > If you add multiple servers to the **Selected Runbook Server(s)** pane, the runbook runs only on the first server if it's available. The other servers are backup servers where the runbook runs only if the primary server isn't available.

7.  Select **Start**.

# [Stop a runbook](#tab/Stop)

Follow these steps to stop a runbook:

1.  Select **Runbooks** to open the **Runbooks** workspace.

2.  If the runbook is located in a folder, select the folder in the **Runbooks** pane.

3.  Select the **Runbooks** tab in the results pane.

4.  Select the runbook, and then in the **Actions** pane, select **Stop Runbook**.

5.  Select **OK** to the message to confirm that you want to stop the jobs.

6.  If the runbook was started successfully, you receive a confirmation message that the job was stopped. If the runbook has no running jobs, you receive a message that no job was running.

# [View the status of a runbook](#tab/ViewStatus)

Follow these steps to view the status of a runbook in the Orchestration console:

1.  Select **Runbooks** to open the **Runbooks** workspace.

2.  If the runbook is located in a folder, select the folder in the **Runbooks** pane.

3.  Select the **Runbooks** tab in the results pane.

4.  Select the runbook.

5.  To view all the jobs that the runbook created, in the **Actions** pane, select **View Jobs**.

6.  To view all the instances that the runbook created, in the **Actions** pane, select **View Instances**.

---

## Stop jobs

A job is a request for a runbook to run. A job is created only when you request a runbook to run. If the first action in a runbook is a monitor, the job runs continuously until the runbook or job is stopped. An hourglass indicates the status of a running job. An instance is a running copy of a runbook.  

You can't start a job; you can only start a runbook.  

When you view an instance, you can choose to stop the associated job. Stopping the job stops the instance, the job, any other associated instances, and the runbook.  

::: moniker-end

## Next steps

To learn more about deploying runbooks see [Deploy runbooks](deploy-runbooks.md).
