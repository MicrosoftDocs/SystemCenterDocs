---
title: Schedules_1
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c7dd39d-d3f7-492a-af19-a45b1b2d235a
---
# Schedules_1
[!INCLUDE[orchlong](Token/orchlong_md.md)] uses schedules to define the times when runbooks can run. For example, there are times when it is inappropriate to run some runbooks, such as backing up a runbook on a main server during regular business hours. You can create a schedule that runs according to a complex interval, such as the first and third Mondays and Thursdays of every month, except when these days fall on a holiday.

Schedules use the system clock of the Runbook server that runs the runbook. This enables schedules to function in virtual machine environments, and to continue running even when the system clock is adjusted because of the move to or from daylight savings time.

Runbooks that start before a prohibited time run until finished, even if they are still processing when the prohibited time arrives. They will not be interrupted after processing has started.

> [!IMPORTANT]
> The access permissions for schedules can be modified, but the runbook server does not enforce these permissions.

> [!NOTE]
> If a runbook is scheduled to start during an hour that is skipped when the system clock is adjusted forward by one hour, that starting time is skipped, and the runbook starts at the next scheduled time. If a runbook is scheduled to start during an hour that occurs two times because the system clock is adjusted backward by one hour, the runbook starts two times.

> [!NOTE]
> [!INCLUDE[orchshort](Token/orchshort_md.md)] does not support moving multiple schedules with multiple\-selection. To move more than one schedule to another folder, you must move each schedule individually.

## Conditional Links
In addition to assigning a schedule to a runbook, you can use a [Check Schedule](Check-Schedule.md) activity to use a schedule for conditional logic in a runbook. This activity checks a particular schedule and returns a published data item with a value of true or false specifying whether the current time is within the schedule. This published data item can be used by a link to determine whether to run a particular activity or to continue to the workflow.

## <a name="BKMK_CreateSchedule"></a>Creating a schedule and assigning the schedule to a runbook
Use the following procedures to create a schedule, to assign the schedule to a runbook, or remove a schedule from a runbook.

#### To create a schedule

1.  In the **Connections** pane, right\-click the **Schedules** folder or a subfolder of the **Schedules** folder, point to **New**, and then click **Schedule** to open the **New Schedule** dialog box.

2.  On the **General** tab, in the **Name** box, type a name for the schedule.

3.  In the **Description** box, type a description that describes or explains the purpose of the schedule.

4.  Click the **Details** tab. Select the days that this schedule allows runbooks to run:

    **Days of week**:  Select this option and select the days of the week when this schedule allows runbooks to run.

    **Occurrence**: Select the weeks of the month when the schedule allows runbooks to run.

    **Days of month**: Select this option and select the days of the month when this schedule allows runbooks to run. Specify the days of the month by entering the number of the day. You can use hyphens to describe ranges and commas to separate entries. For example, typing **1,3** includes the first and third day of the month. Typing **1\-21** includes the first through to the twenty\-first day of the month. You can combine both to create complex descriptions of the days of the month. Type **all** to specify all days of the month. Type **last** to specify the last day of the month.

    You cannot use **all** and **last** as part of a range of days. Additionally, if you typed a range of 5\-31, this range works correctly for all months, including those with 28, 29, 30, and 31 days.

5.  Click **Hours** to open the **Schedule Hours** dialog box.

6.  Click and drag to select a group of hours in a week. The text at the bottom of the dialog box shows the time period that you selected. Then select one of the following:

    **Permit** \(blue\): assigns the time period that you selected as a time when runbooks are allowed to run.

    **Denied** \(white\): assign the time period that you selected as a time when runbooks are not allowed to run.

7.  Click **OK**.

8.  Click the **Exceptions** tab. The list displays all the days that are exceptions to the rules defined in the **Details** tab.

9. Click **Add** to open the **Date** dialog box.

10. Specify the date and select **Allow** or **Disallow** to allow or not allow the runbook to run on that day, and then click **OK**. The entry appears in the list.

11. To modify an Exception entry, select it, and then click **Modify**. To remove the Exception entry, select it, and then click **Remove**.

12. To modify a schedule, double\-click the **Schedule**.

13. To remove a schedule, right\-click the **Schedule**, and then select **Delete**.

14. Click **Finish**.

#### To assign a schedule to a runbook

1.  Right\-click the runbook tab, and then click **Properties** to open the **Runbook Properties** dialog box.

2.  On the **General** tab, click the ellipsis **\(...\)** button to open the **Select a Schedule** dialog box.

3.  Select the schedule that you want to apply to the runbook, and then click **OK**.

4.  Click **Finish**.

    Every time the runbook is started, it checks the schedule to verify that it is allowed to run. If it is not allowed to run, it stops and does not restart until the next time it is started.

#### To remove a schedule from a runbook

1.  Right\-click the runbook tab, and then click **Properties** to open the **Runbook Properties** dialog box.

2.  On the **General** tab, click the ellipsis **\(...\)** button to open the **Select a Schedule** dialog box.

3.  Do not select a schedule. Click **OK**.

4.  Click **Finish**. The schedule is removed from the runbook.

## See Also
[Published Data](Published-Data.md)
[Check Schedule](Check-Schedule.md)


