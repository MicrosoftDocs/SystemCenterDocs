---
title: Scheduling a Runbook
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e7929b96-7057-4b18-bcd6-9d4a9f8566da
---
# Scheduling a Runbook
To schedule a runbook in [!INCLUDE[sma_1](../Token/sma_1_md.md)] to start at a specified time, you link it to one or more schedules. A schedule can be configured to either run one time or recurring every specified number of days. A runbook can be linked to multiple schedules, and a schedule can have multiple runbooks linked to it.

## <a name="Create"></a>Creating a Schedule
You can either create a new schedule with the Management Portal or with Windows PowerShell. You also have the option of creating a new schedule when you link a runbook to a schedule using the Management Portal.

### To create a new Schedule with the Management Portal

1.  In the Management Portal, select **Automation**.

2.  Select the **Assets** tab.

3.  At the bottom of the window, click **Add Setting**.

4.  Click **Add Schedule**.

5.  Type a **Name** and optionally a **Description** for the new schedule.

6.  Select whether the schedule will run **One Time** or **Daily**.

7.  Specify a **Start Time** and the other options depending on the type of schedule that you selected. The time zone of the start time will match the time zone of the local computer.

### To create a new Schedule with Windows PowerShell
You can use the [Set\-SmaSchedule](http://aka.ms/runbookauthor/cmdlet/setsmaschedule) cmdlet to create a new schedule or modify an existing schedule in [!INCLUDE[sma_2](../Token/sma_2_md.md)]. You must specify the start time for the schedule and whether it should run one time or daily.

The following sample Windows PowerShell commands create a new schedule called My Daily Schedule that starts on the current day and continues for one year every day at noon.

```powershell
$webServer = 'https://MyServer'
$port = 9090
$scheduleName = 'My Daily Schedule'
$startTime = (Get-Date).Date.AddHours(12)
$expiryTime = $startTime.AddYears(1)

Set-SmaSchedule –WebServiceEndpoint $webServer –Port $port –Name $scheduleName –ScheduleType OneTimeSchedule –StartTime $startTime –ExpiryTime $expiryTime –DayInterval 1
```

## <a name="Link"></a>Linking a Schedule to a Runbook
A runbook can be linked to multiple schedules, and a schedule can have multiple runbooks linked to it. If a runbook has parameters, then you can provide values for them that are used when the runbook is started. You must provide values for any mandatory parameters.

### To link a schedule to a runbook with the Management Portal

1.  In the Management Portal, select **Automation**.

2.  Select the **Runbooks** tab.

3.  Click on the name of the runbook to schedule.

4.  Click the **Schedule** tab.

5.  If the runbook is currently linked to a schedule,.

6.  Click **Link** at the bottom of the window. Then either click **Link to a New Schedule** and follow the dialog box to create a new schedule, or click **Link to an Existing Schedule** and select a schedule that has already been created.

7.  If the runbook has parameters, you will be prompted for their values.

### To link a schedule to a runbook with Windows PowerShell
You can use the [Start\-SmaRunbook](http://aka.ms/runbookauthor/startsmarunbook) with the **ScheduleName** parameter to link a schedule to a runbook. You can specify values for the runbook’s parameters with the **Parameters** parameter. See [Starting a Runbook](../Topic/Starting-a-Runbook.md) for more information on specifying parameter values.

The following sample commands show how to link a schedule to a runbook.

```powershell
$webServer = 'https://MyServer'
$port = 9090
$runbookName = "Test-Runbook"
$scheduleName = "Sample-DailySchedule"

Start-SmaRunbook –WebServiceEndpoint $webServer –Port $port –Name $runbookName –ScheduleName $scheduleName –Parameters $params

```

## See Also
[Service Management Automation](Service-Management-Automation.md)
[Runbook Operations](Runbook-Operations.md)
[Starting a Runbook](Starting-a-Runbook.md)

