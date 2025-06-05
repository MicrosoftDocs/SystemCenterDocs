---
title: Build and test runbooks in System Center - Orchestrator
description: This article provides guidance and detailed procedures for creating and testing runbooks in System Center - Orchestrator.
ms.service: system-center
ms.subservice: orchestrator
ms.topic: article
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.custom: engagement-fy23, engagement-fy23
---
# Build and test runbooks

The **Runbook Designer** is the tool that you use to create, manage, and run runbooks. You can also run runbooks and view their status in the [Orchestration Console](console-overview.md).  

To build a runbook, you drag activities onto the workspace. Activities are the building blocks of runbooks. In general, individual activities perform three actions:

- Access published data  

- Perform some action  

- Publish new data

For more information about the types of activities, see [Control runbook activities](control-runbook-activities.md).

## Runbook Designer Panes

The Runbook Designer interface is organized into the following four panes.  

|Pane|Description|  
|--------|---------------|  
|**Connections**|The folder structure where you can organize workflows in the Orchestrator system and edit permissions on folders. Also provides access to **Runbook Servers** and **Global Settings**.|  
|**Runbook Designer workspace**|The workspace where you build Orchestrator runbooks. The runbooks in the folder selection in the **Connections** pane are listed as tabs across the top of the workspace. When you select a tab in a runbook, it's displayed in the Runbook Designer workspace.|  
|**Activities**|Contains all the activities available (either standard activities or activities available from integration packs) for use in runbooks. You drag activities from the **Activities** pane into the Design workspace, and then link them together to form runbooks.|  
|**Log**|Logs showing the activity and history for the current runbook. For more information, see [Orchestrator Logs](orchestrator-logs.md).|  

## Trace logs location

Following are the Trace logs locations:

- %ProgramData%Microsoft System Center 2012\Orchestrator\**\Logs\*.log
- %Common Files%\Microsoft System Center 2012\Orchestrator\Management Server\Components\Logs\*.log

## Sort activities by activity name and category name

Orchestrator lets you sort activities alphabetically by activity name or by category name. By default, activities are sorted by category, such as Runbook Control, Email, File Management, Monitoring, Notification, Scheduling, System, Text File Management, and Tools.  

Use the following steps to sort activities by their activity name and category name.  

### Sort activities alphabetically by activity name  

- In the **Activities** pane, right-click a category name to select **All Activities**.  

    The activities are sorted alphabetically by activity name.  

### Sort activities alphabetically by category name  

- In the **Activities** pane, right-click a category name to select **Default**.  

    The activities are sorted alphabetically by category name.  

## Change icons  

You can change the default size of each activity icon from small to large by right-clicking an activity name and selecting **Small** or **Large**.

## Start a runbook in the Designer

Follow these steps to start a runbook in the Designer:

1. In the **Connections** pane, select the **Runbooks** folder to see the available runbooks.  

2. In the Design workspace, select a runbook tab.  

3. If the runbook is Checked Out, select the **Check In** button.  

4. In the Design workspace, right-click the runbook tab and select **Run**.  

5. In the **Start Runbook** dialog, go to **Available Runbook Server\(s\)** box and select the applicable server.  

6. Select the Arrow button so that the server name is now in the **Selected Runbook Servers\(s\)** box.  

7. Select **Start**.  

## Stop a job from the Runbook Designer

Follow these steps to stop a job from the Runbook Designer:  

1. Select the **Monitor Runbook** tab.  

2. On the toolbar, select **Stop**.

## Test your runbook

After you build a runbook, you can test it before it's run in production. To test, you use the **Runbook Tester** which you start in the **Runbook Designer**. The **Runbook Tester** lets you run the runbook to view the Published Data from each activity. You can run through the entire runbook, step through each activity one at a time, or set breakpoints at certain activities.

> [!IMPORTANT]  
> Runbook Tester actually performs each activity within the workflow. The steps are not performed in a simulated or virtualized environment. All the connections referenced in the runbook are live and fully functional. So any activities that modify or destroy data in connected systems cause that data to be modified or destroyed. For example, if you use the **Query Database** activity to **DROP TABLE ImportantTable**, it actually deletes the **ImportantTable** from the instance of Microsoft SQL Server. 
 
> [!IMPORTANT]  
> Note that the account used to start the runbook must have permission on the local computer to run successfully. These permission requirements also apply when testing the runbook with the Runbook Tester. To successfully test your runbook, start the Runbook Designer **as Administrator**. By association, the Runbook Tester runs **as Administrator** and uses the higher-level security token.

### Test a runbook

Follow these steps to test a runbook:

1. In the **Runbook Designer**, open the runbook, and on the menu bar, select **Runbook Tester**.  

2. If prompted, select **Yes** to check out the runbook.  

3. To run through the runbook from beginning to end without stopping, select **Run to Breakpoint**.  

    If you want to step through it one activity at a time, select **Step**.  

4. View the **Log** pane to see the completion status of each activity. To view the details and Published Data from an activity, select the activity and select **Show Details**.  

### Set a breakpoint  

Follow these steps to set a breakpoint:

1. Select the activity on which to set the breakpoint.  

2. Select **Toggle Breakpoint**.  

3. Select **Run to Breakpoint**.  

    Each activity up to the breakpoint runs. The runbook pauses before running the activity with the breakpoint.  

4. To continue through to the end of the runbook, select **Run to Breakpoint** again, or to step through it one activity at a time, select **Step**.

## Next steps

- To get step-by-step instructions for building and testing a sample runbook, see [Creating and testing a sample runbook](creating-and-testing-a-sample-runbook.md).
- To review guidance and best practices for designing runbook, see [Designing a runbook](designing-a-runbook.md).
