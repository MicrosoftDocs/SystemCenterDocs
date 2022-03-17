---
title: Overview of Orchestration console 2022
description: The Orchestration console is a Single Page App that helps you monitor and execute your Orchestrator deployment.
ms.date: 03/21/2022
ms.prod: system-center
ms.technology: orchestrator
ms.topic: reference
author: jyothisuri
ms.author: jsuri
manager: carmonm
MonikerRange: 'sc-orch-2022'
---

# Overview of Orchestration console 2022

The Orchestrator console is a single page App that helps you monitor and execute your Orchestrator deployment. This article details the supported features in the Orchestrator 2022 console.

:::image type="console" source="media/console-overview-2022/console.png" alt-text="Screenshot showing Orchestrator console.":::

## Navigation pane

The Navigation pane on the left shows the **Runbook** and **Folders** tree, similar to the one shown on the **Runbook Designer**. Unlike the console in earlier versions, you cannot click the *Folders*, but can click the *Runbooks* and view specific data and use specific options.

The Navigation pane is always visible on all screens to allow quick navigation to other runbooks and folders, while remaining on the same screen.

To the right of the navigation pane, you can see the chosen screen. The Dashboard screen is shown by default.

>[!NOTE]
>Currently, auto-refresh is not supported for any of the screens. Reload the page manually.


## Dashboard

The Dashboard shows **Active jobs** on the top followed by a table of all **Completed jobs (history)**. The **Completed jobs (history)** pane is collapsed by default, allowing focus on the active jobs.

:::image type="active and completed jobs" source="media/console-overview-2022/active-and-completed-jobs.png" alt-text="Screenshot showing active and completed jobs.":::

Each row in both the panels corresponds to a unique job. A job may have one or more runbook instances. Each row shows:
- **Job ID**: Link to the Runbook
- **Timestamps**: The number of successful and failed instances is shown in one of the columns for all rows.
- **Action buttons**: Stop job or View Job details

You can click and expand each of the job rows and view the instances of the job.

## Runbooks

When you select a runbook on the navigation tree or click a runbook link, the app navigates to the the Runbook details screen. The top panel lists out runbook metadata (editing status, timestamps, etc). The **Run** button available on the screen allows you to queue the runbook for execution on the desired subset of runbook servers. The **Run** button is disabled for runbooks that are not in **Published** state.

:::image type="run" source="media/console-overview-2022/run.png" alt-text="Screenshot showing run button.":::

Below this panel is a tabbed view:

- View, for the Runbook graphical image (see above).
- Jobs, for listing the active and completed jobs of the runbook (see below).
- Instances, for listing active and completed instances of the runbook across all its Jobs (see below).

:::image type="run screen" source="media/console-overview-2022/run-1.png" alt-text="Screenshot showing run screen.":::

:::image type="status check screen" source="media/console-overview-2022/run-2.png" alt-text="Screenshot showing status check screen.":::

You can click the rows in the Jobs view just like the ones on the Dashboard screen. Jobs that are running can be stopped using the buttons on the right of the running row.

While this screen is active, you can choose a different runbook on the Navigation tree. This will not change the selected tab, you can quickly look at Jobs of different runbooks by selecting the jobs tab and navigating to the desired runbooks in the Navigation tree.

## Jobs

When you select a job (using the (i) button), the app navigates to this screen. The top panel shows the job’s metadata (timestamps, parameters).

A table that shows the Instances of this job follows the panel.

:::image type="job details" source="media/console-overview-2022/job-details.png" alt-text="Screenshot showing job details.":::

Most jobs have a single Instance. If the runbook has a Monitor/Event trigger activity, then each trigger starts a unique job instance. The screenshot below shows a Job with more than one Instance.

:::image type="instances of jobs" source="media/console-overview-2022/instances-of-jobs.png" alt-text="Screenshot showing instances of jobs.":::

>[!NOTE]
>A Job can have at most one running Instance at any time. But, since a Runbook can have many concurrently running Jobs, a Runbook can have more than one running Instance.

The status of the job is shown visually with the icons:

- **Three dots**: Job is queued
- **Hourglass**: Job is running
- **Circle with slash**: Job was cancelled
- **Tick**: Job completed successfully
- **Red exclamation**: Job completed but failed
- **Warning**: Job completed with warning(s)

## Instances

When you select an Instance (using the (i) button), the app navigates to this screen. The top panel shows the Instance’s metadata (Job ID, timestamps, parameters, server which executes this instance).

:::image type="instance-screen" source="media/console-overview-2022/instance-screen.png" alt-text="Screenshot showing instance screen.":::

The top panel also has three navigation buttons:

- **Previous**: View Instance that ran before this one.
- **Next**: View Instance that ran after this one.
- **Latest**: View most current instance

:::image type="runbook instance details" source="media/console-overview-2022/runbook-instance-details.png" alt-text="Screenshot showing runbook instance details.":::

:::image type="runbook details" source="media/console-overview-2022/runbook-instance-details-1.png" alt-text="Screenshot showing runbook details.":::

>[!NOTE]
>- Note that the job ID is same, and since the second instance is still running, the job is also still running.
>- The navigation buttons will cross Job boundaries! Pay attention to the Job ID shown in the top panel.

Below the panel, you see the runbook diagram. You can click each runbook activity  to view activity outputs. A separate icon denotes the status for each activity. When you click any activity, an overlay is shown on the right that lists the activity’s outputs.

Since an activity may be executed more than once within an instance (because of looping), each execution of the Activity has a unique **Sequence number**. The overlay lets you choose the **Sequence #** using the dropdown on the top.

:::image type="activity output overlay" source="media/console-overview-2022/activity-output-overlay.png" alt-text="Screenshot showing activity output overlay.":::

>[!NOTE]
>To ensure fast load time, only first 10 activity outputs are loaded for the activity. The **Load more** button shows how many times this activity was executed, and you can click it to load more outputs.

The **Instance** and **Activity status** follow the same format as **Job Status**.

## Execute runbooks

Navigate to the Runbook screen of the desired Runbook and click **Run** . An overlay form opens to the right where you are asked to:
- Set values to all input parameters (required)
- Choose the set of Runbook servers on which this Job can be scheduled.

Only one of these servers will actually execute this Job. To execute a Runbook on many servers you will have to run those many number of Jobs and explicitly set the servers one-by-one.

:::image type="create job" source="media/console-overview-2022/create-job.png" alt-text="Screenshot showing create job.":::

>[!NOTE]
> Enter the parameters in the form, else the form will not be considered.

When the form is submitted, a disappearing popup is shown on the top right to notify whether the job was successfully queued or not.

:::image type="job queue notification" source="media/console-overview-2022/job-queue-notification.png" alt-text="Screenshot showing job queue notification.":::

## Stop running Jobs

The **Stop** button is shown on the Dashboard and the Job screen. disappearing popup on the top right notifies whether the Job is stopped or not.

:::image type="job stop notification" source="media/console-overview-2022/job-stop-notification.png" alt-text="Screenshot showing job stop notification.":::

## FAQ

### The Console does not load, error “Uh oh! Trouble connecting to WebApi [status 0]” appears

1. Check the [browser’s developer console](/microsoft-edge/devtools-guide-chromium/overview) (Console tab), look for CORS errors (*blocked by CORS policy*)

   :::image type="console tab" source="media/console-overview-2022/console-tab.png" alt-text="Screenshot showing console tab.":::

2. If there are no CORS errors, look at the **Event Viewer** logs (Application) on the Web API computer.

To fix CORS errors, you must ensure that the API’s *web.config* file must have a suitable CORS configuration. The browser error shows the origin value it is expecting in the *web.config*. [See this document](/iis/extensions/cors-module/cors-module-configuration-reference) for details about how to configure CORS in *web.config* .

## Next steps

- To learn more about deploying runbooks see [Deploy runbooks](deploy-runbooks.md)
