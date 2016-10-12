---
title: Runbook Properties
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3bd4992a-badc-4d36-9e64-52e2a167f9e8
ms.author: cfreeman
ms.date: 2016-10-12
author: cfreemanwa
manager: cfreeman
---
# Runbook Properties

> Applies To: System Center 2016 - Orchestrator

A runbook is essentially a series of activities that are using data, performing tasks, and publishing data for use by other activities in the runbook. Each runbook has a collection of configurable properties. These properties let you customize the behavior of a runbook.  

### To view the properties of a runbook  

1.  In the Runbook Designer, in the **Connections** pane, click the **Runbooks** folder.  

2.  If the runbook is stored in a folder, select the appropriate folder under **Runbooks**.  

3.  In the **Runbook Designer** Design workspace, Right-click the tab of a runbook to select **Properties**.  

4.  To close the **Runbook Properties** dialog box, click **Finish**.  

A summary of the runbook properties and how to configure them follows.  

## General  
On the **General** tab of the **Runbook Properties** dialog box, you can customize a name and description for the runbook. You can also associate a schedule with the runbook. After you assigned a schedule to the runbook, the runbook only runs on the dates and times that you specified in the schedule.  

#### To create a schedule  

1.  In the Runbook Designer, in the **Connections** pane, expand the **Global Settings** folder.  

2.  Right-click the **Schedules** folder to select **New** to select**Schedule**.  

3.  On the **General** tab of the **New Schedule** dialog box, in the **Name** box, enter a name for the schedule.  

4.  On the **Details** tab of the **New Schedule** dialog box, select the date and time to start the runbook.  

    ###### To configure the schedule for specific days of the week  

    1.  On the **Details** tab of the **New Schedule** dialog box, click **Days of the week**, and then select the days on which you want to start the runbook.  

    2.  Under **Occurrence**, select the week of the month to start the runbook.  

        For example, if you want to start the runbook every Monday, under **Days of the week**, select **Monday**, and under **Occurrence**, select **First**, **Second**, **Third**, **Fourth**, and **Last**.  

    ###### To configure the schedule for specific days in the month  

    1.  On the **Details** tab of the **New Schedule** dialog box, click **Days of the month**.  

    2.  In the **Days of the month** box, enter the date or dates on which you want to start the runbook.  

        Separate multiple dates with a comma.  

        For example, if you want to start the runbook on the first and 15th of every month, enter **1, 15** in the **Days of the month** box.  

    ###### To configure the schedule for specific hours  

    1.  On the **Details** tab of the **New Schedule** dialog box, select **Hours**.  

    2.  In the **Schedule Hours** dialog box, select the hours on which you want to start the runbook.  

        You can both allow and deny the start of a runbook during any period. For example, if you want to start a runbook only outside business hours, select the hours of 9 A.M. to 5 P.M. for Monday, Tuesday, Wednesday, Thursday, and Friday, and then click **Denied**.  

5.  On the **Exceptions** tab of the **New Schedule** dialog box, add any date exceptions for the runbook, and then click **OK**.  

6.  Click **Finish**.  

> [IMPORTANT]  
> The scheduled date and time to start a runbook is based on the system clock of the runbook server. This enables schedules to function in virtual machine environments and to continue to run even when the system clock adjusts for daylight savings time.  

#### To associate a schedule with a runbook  

1.  In the **Runbook Properties** dialog box, on the **General** tab, click the ellipsis **\(...\)** button to browse for a **Schedule**.  

2.  Select a schedule, click **OK**, and then click **Finish**.  

## Runbook Servers  
This tab displays the list of runbook servers assigned to run this runbook. If the list is empty, the runbook uses the setting defined in the **Runbook Servers** folder found in the **Connections** pane of the Runbook Designer. If the runbook server that uses the Primary role is available, the runbook runs on it. If the primary runbook server is not available, each runbook server that uses a Standby role is checked until one is found that can run the runbook.  

You can override the default behavior and assign a primary and any number of standby runbook servers to a runbook. It is useful to assign a specific runbook server to a runbook if the runbook requires access to a specialized resource, such as a backup device.  

#### To assign primary and standby runbook servers to a runbook  

1.  In the **Runbook Properties** dialog box, on the **Runbook Servers** tab, select **Override default Runbook Server roles** to configure primary and standby runbook servers.  

2.  Click **Add**.  

3.  Select a runbook server, and then click **OK**.  

    The first runbook server that you added becomes the primary runbook server.  

4.  To add more runbook servers, click **Add**, and select another runbook server.  

    All additional runbook servers are added as standby runbook servers.  

5.  When you are finished adding runbook servers, click **Finish**.  

## <a name="BKMK_Logging"></a>Logging  
This feature controls what data is logged to the orchestration database. If stored in the orchestration database, this data is visible in views such as the **Log** pane in the Runbook Designer and in the Orchestration console. This information does not affect the availability of Published Data in a running runbook.  

Published Data includes data specific to each activity.  

Common Published Data is a set of data items that are common to all activities. These items are as follows:  

-   Activity Name  

-   Activity Type  

-   Activity ID  

-   Activity End Time Year, Month, Day, Weekday, Hours, Minutes, Seconds  

-   Activity Duration  

-   Previous Activity  

-   Previous Activity Name  

> [CAUTION]  
> When you turn on logging, the size of the orchestration database increases.  

## Event Notifications  
You can enable event notification for the runbook. Notifications appear in views such as the **Log** pane in the Runbook Designer and in the Orchestration console.  

If you want to be notified when a runbook runs for more than a specified length of time, enter a value in the **seconds** box.  

If you want to be notified if the runbook does not run, click the **Runbook fails to run** option.  

For more information about Event Notifications, see [Orchestrator Logs](../get-started/orchestrator-logs.md).  

## Job Concurrency  
The job concurrency setting lets you set the maximum number of simultaneous jobs, so that you can carry out multiple requests for the same runbook at the same time. This setting applies to the individual runbook. A runbook server can run 50 runbooks at the same time. If you select a job concurrency setting over 50, your environment requires more runbook servers or the requests to start a runbook will queue.  

The following limitations apply:  

-   You cannot run simultaneous requests for runbooks that start with Monitoring activities. If you try to change the maximum number of simultaneous requests for these runbooks, the Runbook Designer resets the **Maximum number of simultaneous jobs** value to 1 and displays an error message.  

-   A runbook server runs simultaneous requests for runbooks up to the maximum processing limit. To change the maximum processing limit, see [How to Configure Runbook Throttling](../manage/how-to-configure-runbook-throttling.md).  

-   Do not create simultaneous requests for runbooks that contain Modify Counter activities. When you run different copies of the same runbook at the same time that modify \(set, reset, increment, or decrement\), a Counter can cause the Counter value to become unreliable. You can read the value of Counters in runbooks that run at the same time.  

-   Do not run simultaneous requests for runbooks that interact with a non\-Microsoft product, such as a ticketing or system\-monitoring tool, unless you have a good understanding of how the tool handles parallel processing. If the non\-Microsoft application cannot handle parallel processing, or if you do not know, leave the maximum number of simultaneous requests at a value of 1.  

-   Plan the use of multiple requests carefully. Before you change the maximum number of simultaneous runbook requests, consider the tasks performed by the runbook. Verify that each runbook instance can finish successfully. For example, if your runbook creates a folder, copies files into it, and then deletes the folder when it is finished, one instance of the runbook might delete the folder before other instances are finished with it. In this case, you should keep the maximum number of simultaneous requests for this runbook a value of 1 to avoid conflicts.  

## Returned Data  
Returned Data defines the data that a runbook returns when it finishes.&nbsp; Each Returned Data definition can contain either a single or multiple parameter values. To populate the data definitions, end the workflow with a Return Data activity that contains the return values.  

You access the Returned Data values through Published Data in one of several ways.  

-   Invoke the runbook from another runbook by using the Invoke Runbook activity. The parent runbook can access the child runbook's Returned Data as Published Data from the Invoke Runbook activity.  

-   View the Published Data from the Runbook Designer or Orchestration console.  

-   Use the Orchestrator web service to return the Published Data programmatically.  

To define the Returned Data for a runbook to return, use **Add**, **Edit**, and **Remove** to create each parameter.  

## See Also  

[Orchestrator Logs](../get-started/orchestrator-logs.md)  
