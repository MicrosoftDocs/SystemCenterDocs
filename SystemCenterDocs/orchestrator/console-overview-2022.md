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

The Navigation pane is always visible on all screens to allow quick navigation to other Runbooks and Folders, while remaining on the same screen.

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

When you select a Runbook on the Navigation tree or click on a Runbook link, the app navigates to the the Runbook details screen. The top panel lists out Runbook metadata (editing status, timestamps, etc). The **Run** button is also present that allows you to queue the Runbook for execution on the desired subset of Runbook Servers. The **Run** button is disabled for Runbooks that are not in **Published** state.

:::image type="run" source="media/console-overview-2022/run.png" alt-text="Screenshot showing run button.":::

Below this panel is a tabbed view:

- View, for the Runbook graphical image (see above).
- Jobs, for listing the active and completed jobs of the Runbook (see below).
- Instances, for listing active and completed instances of the Runbook across all its Jobs (see below).

:::image type="run screen" source="media/console-overview-2022/run-1.png" alt-text="Screenshot showing run screen.":::

:::image type="status check screen" source="media/console-overview-2022/run-2.png" alt-text="Screenshot showing status check screen.":::

The rows in the Jobs view are clickable just like the ones on the Dashboard screen. Jobs that are running can be stopped using the buttons on the right of the running row.

While this screen is active, you can choose a different runbook on the Navigation tree. Doing this will not change the selected tab, ie. you can quickly look at Jobs of different Runbooks by selecting the Jobs tab and navigating to the desired Runbooks in the Navigation tree.

## Jobs

When you select a Job (using the (i) button), the app navigates to this screen. The top panel shows the Job’s metadata (timestamps, parameters).

A table that shows the Instances of this Job follows the panel.

:::image type="job details" source="media/console-overview-2022/job-details.png" alt-text="Screenshot showing job details.":::

Most Jobs have a single Instance. If the Runbook has a Monitor/Event trigger activity, then each trigger starts a unique Job instance. The screenshot below shows a Job with more than one Instance.

:::image type="instances of jobs" source="media/console-overview-2022/instances-of-jobs.png" alt-text="Screenshot showing instances of jobs.":::

>[!NOTE]
>A Job can have at most one running Instance at any time. But, since a Runbook can have many concurrently running Jobs, a Runbook can have more than one running Instance.

The status of the Job is shown visually with the icons:

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
>- Note that the Job ID is same, and since the second instance is still running, the Job is also still running.
>- The navigation buttons will cross Job boundaries! Pay attention to the Job ID shown in the top panel.

Below the panel, you see the Runbook diagram. Each Runbook Activity can be clicked to show the Activity outputs and an icon denotes the status for each Activity. When you click on any Activity, an overlay is shown on the right that lists the Activity’s outputs.

Since an Activity may be executed more than once within an Instance (because of looping), each execution of the Activity has a unique **Sequence number**. The overlay lets you choose the **Sequence #** using the dropdown on the top.

:::image type="activity output overlay" source="media/console-overview-2022/activity-output-overlay.png" alt-text="Screenshot showing activity output overlay.":::

>[!NOTE]
>To ensure fast load time, only first 10 Activity outputs are loaded for the activity. The **Load more** button shows how many times this Activity was executed, and you can click it to load more outputs.

The Instance and Activity status follow the same format as Job Status.

## Executing Runbooks

Navigate to the Runbook screen of the desired Runbook and click on **Run** button. This opens an overlay form on the right where you are asked to:
- Set values to all input parameters (required)
- Choose the set of Runbook Servers on which this Job can be scheduled.
Only one of these servers will actually execute this Job. To execute a Runbook on many servers you will have to run those many number of Jobs and explicitly set the Server one-by-one.

:::image type="create job" source="media/console-overview-2022/create-job.png" alt-text="Screenshot showing create job.":::

>[!NOTE]
>The parameters must be filled in or else the form will not be considered valid.

When the form is submitted, a disappearing popup is shown on the top right to notify whether the job was successfully queued or not.

:::image type="job queue notification" source="media/console-overview-2022/job-queue-notification.png" alt-text="Screenshot showing job queue notification.":::

## Stop running Jobs

The stop button is shown on the Dashboard and the Job screen. A disappearing popup on the top right notifies whether the Job was stopped or not.

:::image type="job stop notification" source="media/console-overview-2022/job-stop-notification.png" alt-text="Screenshot showing job stop notification.":::

## FAQ

### The Console does not load, error “Uh oh! Trouble connecting to WebApi [status 0]” is shown

1. Please check the [browser’s developer console](/microsoft-edge/devtools-guide-chromium/overview) (Console Tab), look for CORS errors (“blocked by CORS policy”)

   :::image type="console tab" source="media/console-overview-2022/console-tab.png" alt-text="Screenshot showing console tab.":::

2. If there are no CORS errors, look at the Event Viewer logs (Application) on the Web API machine.

To fix CORS errors, you must ensure that the API’s web.config must have a suitable CORS configuration. The browser error shows what origin value it is expecting in the web.config. [Refer this document](/iis/extensions/cors-module/cors-module-configuration-reference) on how to configure CORS in web.config.

## Next steps

- To learn more about deploying runbooks see [Deploy runbooks](deploy-runbooks.md)
