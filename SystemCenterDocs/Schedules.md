---
title: Schedules
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0092bd39-187d-42ea-b126-02ef516e21e4
---
# Schedules
[!INCLUDE[sma_2](./Token/sma_2_md.md)] Schedules are used to schedule runbooks to run automatically.  This could be either a single date and time for the runbook to run once.  Or it could be a recurring schedule to start the runbook multiple times.  Schedules are typically not accessed from runbooks.

## Windows PowerShell Cmdlets
The cmdlets in the following table are used to create and manage variables with Windows PowerShell in [!INCLUDE[sma_1](./Token/sma_1_md.md)].

|Cmdlets|Description|
|-----------|---------------|
|[Get\-SmaSchedule](http://go.microsoft.com/fwlink/?LinkID=306457)|Retrieves a schedule.|
|[Set\-SmaSchedule](http://go.microsoft.com/fwlink/?LinkID=306476)|Creates a new schedule or sets the properties for an existing schedule.|

## Creating a new Schedule

### To create a new schedule with the management portal

1.  Select the **Automation** workspace.

2.  At the top of the window, click **Assets**.

3.  At the bottom of the window, click **Add Setting**.

4.  Click **Add Schedule**.

5.  Type a name for the variable in the **Name** box.

6.  Click the right arrow.

7.  Select **One Time** or **Daily**.

8.  Select a **Start Time**.

9. For a Daily schedule, perform the following steps:

    1.  If the schedule should not run indefinitely, select **Schedule Expires On** and specify an expiration date and time.

    2.  In the **Recur Every** box, select the number of days the schedule should recur.

10. Click the check mark to save the variable.

### To create a new schedule with Windows PowerShell in Service Management Automation
The[Set\-SmaSchedule](http://aka.ms/runbookauthor/cmdlet/setsmaschedule) cmdlet both creates a new schedule and sets the value for an existing schedule.  The following sample Windows PowerShell commands create a new schedule called My Daily Schedule that starts on the current day and fires every day at noon for one year:

```powershell
$web = 'https://MySMAServer'
$port = 9090
$scheduleName = 'My Daily Schedule'
$startTime = (Get-Date).Date.AddHours(12)
$expiryTime = $startTime.AddYears(1)
Set-SmaSchedule –WebServiceEndpoint $web –Port $port –Name $scheduleName –ScheduleType OneTimeSchedule –StartTime $startTime –ExpiryTime $expiryTime –DayInterval 1
```

## See Also
[Service Management Automation](Service-Management-Automation.md)
[Authoring Automation Runbooks](Authoring-Automation-Runbooks.md)
[Global Assets](Global-Assets.md)
[Scheduling a Runbook](Scheduling-a-Runbook.md)


