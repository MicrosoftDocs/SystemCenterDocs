---
description:  Proivides guidance and instructions on how to schedule, track, and configure runbooks for Service Management Automation.
manager:  carmonm
ms.topic:  article
author:  cfreemanwa
ms.author: raynew
ms.prod:  system-center-threshold
keywords:  
ms.date: 03/31/2017
title:  Manage runbooks
ms.technology:  service-management-automation
---

# Manage runbooks for Service Management Automation

As an administrator of a Service Management Automation (SMA) installation, you will need to configure runbooks for execution. Configuring includes both initial setup of the runbook workers, as well as scheduling and tracking runbooks. There are two system runbooks that are included with SMA in addition to the runbooks you have authored. These are:

- DiscoverAllLocalModules: Runs immediately after you install a runbook worker. This runbook discovers all native modules on the Windows Server system where the runbook worker has been installed, and extracts activities and activity metadata for these modules so that their activities can be used when authoring runbooks in Windows Azure Pack. 

- SetAutomationModuleActivityMetadata: Runs immediately after you import a module into Service Management Automation. This runbook extracts activities and activity metadata from a newly imported module so that its activities can be used when authoring runbooks in Windows Azure Pack.

## Configuring runbook workers

When you start a runbook job in Service Management Automation, by default, it is picked by a runbook worker selected at random. However, sometimes you might want to run a runbook against a particular runbook worker for various reasons. RunbookWorker configuration property helps you achieve that. For more information on how runbooks are executed, see [Runbook Execution in Service Management Automation](runbook-automation.md).


### Designating a runbook worker through the PowerShell ISE Add-on.

- In the SMA ISE Add-on, under the **Configuration** tab,
sign in using your SMA account.
- On successful login, you can see your runbooks in the **Runbooks** tab.
- In the **Runbooks** tab, select one or more runbooks which you want to be executed against a particular runbook worker.
- Click on **configure** button in the bottom pane.
- In the **Configure Runbook properties** dialog, select a runbook worker from the drop-down menu. Click **Make changes**.


### Designating a runbook worker through the SMA PowerShell module

You can also set the runbook worker property using the following command to do the same via command line

```powershell
$webServer = 'https://MyServer'
$port = 9090
$runbookName = "Sample-TestRunbook"
$workerName = "Worker1"

Set-SmaRunbookConfiguration -WebServiceEndpoint $webServer -Port $port -Name $runbookName -RunbookWorker $workerName

```

You can see a list of all the runbook workers deployed using the following command.

```powershell
$webServer = 'https://MyServer'
$port = 9090

Get-SmaRunbookWorkerDeployment -WebServiceEndpoint $webServer -Port $port

```

> [!NOTE]
Currently, you can not use Windows Azure Pack portal to designate a runbook worker. Use either the SMA ISE Add-on or PowerShell cmdlets to do it.

## Scheduling runbooks

To schedule a runbook in Service Management Automation to start at a specified time, you link it to one or more schedules. A schedule can be configured to either run one time or recurring every specified number of days. A runbook can be linked to multiple schedules, and a schedule can have multiple runbooks linked to it.

### <a name="Create"></a>Creating a schedule
You can either create a new schedule with the Management Portal or with Windows PowerShell. You also have the option of creating a new schedule when you link a runbook to a schedule using the Management Portal.

#### To create a new schedule with the Management Portal

1.  In the Management Portal, select **Automation**.

2.  Select the **Assets** tab.

3.  At the bottom of the window, click **Add Setting**.

4.  Click **Add Schedule**.

5.  Type a **Name** and optionally a **Description** for the new schedule.

6.  Select whether the schedule will run **One Time** or **Daily**.

7.  Specify a **Start Time** and the other options depending on the type of schedule that you selected. The time zone of the start time will match the time zone of the local computer.

#### To create a new schedule with Windows PowerShell
You can use the [Set-SmaSchedule](http://aka.ms/runbookauthor/cmdlet/setsmaschedule) cmdlet to create a new schedule or modify an existing schedule in Automation. You must specify the start time for the schedule and whether it should run one time or daily.

The following sample Windows PowerShell commands create a new schedule called My Daily Schedule that starts on the current day and continues for one year every day at noon.

```powershell
$webServer = 'https://MyServer'
$port = 9090
$scheduleName = 'My Daily Schedule'
$startTime = (Get-Date).Date.AddHours(12)
$expiryTime = $startTime.AddYears(1)

Set-SmaSchedule "WebServiceEndpoint $webServer "Port $port "Name $scheduleName "ScheduleType OneTimeSchedule "StartTime $startTime "ExpiryTime $expiryTime "DayInterval 1
```

## <a name="Link"></a>Linking a schedule to a runbook
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
You can use the [Start-SmaRunbook](http://aka.ms/runbookauthor/startsmarunbook) with the **ScheduleName** parameter to link a schedule to a runbook. You can specify values for the runbook"s parameters with the **Parameters** parameter. See [Starting a Runbook](~/sma/manage-runbooks.md) for more information on specifying parameter values.

The following sample commands show how to link a schedule to a runbook.

```powershell
$webServer = 'https://MyServer'
$port = 9090
$runbookName = "Test-Runbook"
$scheduleName = "Sample-DailySchedule"

Start-SmaRunbook "WebServiceEndpoint $webServer "Port $port "Name $runbookName "ScheduleName $scheduleName "Parameters $params

```

## Tracking runbooks

When you start a runbook in Service Management Automation, a job is created. A job is a single execution instance of a runbook. A single runbook may have multiple jobs, each with their own set of values for the runbook"s parameters.

If the RunbookWorker property of the runbook is populated, then that Worker server will service the job. If the Worker server is not available, then the job will fail with an error. If the RunbookWorker property of the runbook is not populated, then SMA will randomly select an available Worker server to service the request.

The following diagram shows the lifecycle of a runbook job for PowerShell Workflow runbooks.

![Job Statuses - PowerShell Workflow](/system-center/sma/media/manage-runbooks1/sma-runbook-execution-workflow.png)

The following diagram shows the lifecycle of a runbook job for PowerShell script runbooks.

![Job Statuses - PowerShell Script](/system-center/sma/media/manage-runbooks1/sma-runbook-execution-script.png)

### <a name="jobstatuses"></a>Job statuses
The following table describes the different statuses that are possible for a job.

|Status|Description|
|----------|---------------|
|Completed|The job completed successfully.|
|Failed|The job ended with an exception.|
|Queued|The job is waiting for resources on an Automation worker to come available so that it can be started.|
|Starting|The job has been assigned to a worker, and the system is in the process of starting it.|
|Resuming|The system is in the process of resuming the job after it was suspended.|
|Running|The job is running.|
|Stopped|The job was stopped by the user before it was completed.|
|Stopping|The system is in the process of stopping the job.|
|Suspended|The job was suspended by the user, by the system, or by a command in the runbook. A job that is suspended can be started again and will resume from its last checkpoint or from the beginning of the runbook if it has no checkpoints.<br /><br />The runbook will only be suspended by the system in the case of an exception where there is a possibility of resuming. By default, [ErrorActionPreference](http://aka.ms/runbookauthor/preferencevariables) is set to **Continue** meaning that the job will keep running on an exception. If this preference variable is set to **Stop** then the job will suspend on an exception.|
|Suspending|The system is attempting to suspend the job at the request of the user. The runbook must reach its next checkpoint before it can be suspended. If it has already passed its last checkpoint, then it will complete before it can be suspended.|

### <a name="Portal"></a>Viewing job status using the Management Portal

The Automation Dashboard shows a summary of all of the runbooks in the Service Management Automation environment. The summary graph shows the number of total jobs for all runbooks that entered each status over a given number of days or hours. You can select the time range on the top right corner of the graph. The time axis of the chart will change according to the type of time range that you select. You can choose whether to display the line for a particular status by clicking on it at the top of screen.

You can use the following steps to display the Automation Dashboard.

1.  In the Management Portal, select **Automation**.

2.  Select the **Dashboard** tab.

### Runbook dashboard
The Runbook Dashboard shows a summary for a single runbook. The summary graph shows the number of total jobs for the runbook that entered each status over a given number of days or hours. You can select the time range on the top right corner of the graph. The time axis of the chart will change according to the type of time range that you select. You can choose whether to display the line for a particular status by clicking on it at the top of screen.

You can use the following steps to display the Runbook Dashboard.

1.  In the Management Portal, select **Automation**.

2.  Click the name of a runbook.

3.  Select the **Dashboard** tab.

### Job summary, history, and source
You can view a list of all of the jobs that have been created for a particular runbook and their most recent status. You can filter this list by job status and the range of dates for the last change to the job. Click on the name of a job to view its detailed information and its output. The detailed view of the job includes the values for the runbook parameters that were provided to that job.

The job history includes output, warning, and error messages with time stamps of when the record was created. For more information on records that are written to the job history, see [Runbook Output and Messages](overview-runbook-messages-output.md).

The source for a job is the source code of the workflow when the job was run. This may not be the same as the current version of the runbook if it was updated after the job was run.

You can use the following steps to view the jobs for a runbook.

1.  In the Management Portal, select **Automation**.

2.  Click the name of a runbook.

3.  Select the **Jobs** tab.

4.  Click on the **Job Created** column for a job to view its detail and output.

5.  Select the **History** tab to view the job history. Select a history record and click **View Details** at the bottom of the screen for a detailed view of the record.

6.  From the **History** tab, click **View Source** at the bottom of the screen to the source for the job.

### <a name="PowerShell"></a>Retrieving job status using Windows PowerShell
You can use the [Get-SmaJob](http://aka.ms/runbookauthor/cmdlet/getsmajob) to retrieve the jobs created for a runbook and the details of a particular job. If you start a runbook with Windows PowerShell using [Start-SmaRunbook](http://aka.ms/runbookauthor/cmdlet/startsmarunbook), then it will return the resulting job. Use [Get-SmaJobOutput](http://aka.ms/runbookauthor/cmdlet/getsmajoboutput) to get a job"s output.

The following sample commands retrieves the last job for a sample runbook and displays its status, the values provide for the runbook parameters, and the output from the job.

```powershell
$webServer = 'https://MyServer'
$port = 9090
$runbookName = "Test-Runbook"

$job = (Get-SmaJob "WebServiceEndpoint $webServer "Port $port "RunbookName $runbookName | sort LastModifiedDate "desc)[0]
$job.Status
$job.JobParameters
Get-SmaJobOutput "WebServiceEndpoint $webServer "Port $port -Id $job.Id "Stream Output
```

## Configure runbook settings

Each runbook in Service Management Automation has multiple settings. You can use these settings to help locate and manage runbooks. You also can change runbook logging by configuring these settings. Each of these settings is described below followed by procedures on how to modify them.

### <a name="Name"></a>Name and description
You cannot change the name of a runbook after it has been created. The **Description** is optional and can be up to 512 characters.

### <a name="Tags"></a>Tags
Tags allow you to assign distinct words and phrases to help identify a runbook. You can specify multiple tags for a runbook by separating them with commas.

### Logging
By default, Verbose and Progress records are not written to job history. You can change the settings for a particular runbook to log these records. For more information on these records, see [Runbook Output and Messages](overview-runbook-messages-output.md).

### Designated runbook worker
By default, a runbook job will be assigned to a random runbook worker to execute. You can change settings for a particular runbook to execute the runbook on a particular runbook worker. 

## Changing runbook settings with the Management Portal
You can change settings for a runbook in the Management Portal from the **Configure** page for the runbook.

1.  In the Management Portal, select **Automation**.

2.  Select the **Runbooks** tab.

3.  Click the name of a runbook.

4.  Select the **Configure** tab.

## Changing runbook settings with Windows PowerShell
You can use the [Set-SmaRunbookConfiguration](http://aka.ms/runbookauthor/cmdlet/setsmarunbookconfiguration) cmdlet to change all the settings for a runbook except for Tags. You can only change and add Tags for existing runbooks using the Management Portal. You can only set Tags for runbooks with PowerShell when you import a runbook using [Import-SmaRunbook](http://aka.ms/runbookauthor/cmdlet/importsmarunbook).

The following sample commands show how to set the properties for a runbook. This sample adds a description and specifies that verbose records should be logged.

```powershell
$webServer = 'https://MyServer'
$port = 9090
$runbookName = "Sample-TestRunbook"

Set-SmaRunbookConfiguration "WebServiceEndpoint $webServer "Port $port "Name $runbookName "Description "Sample runbook" "LogVerbose $true

```

## Next steps

- Read about managing global assets [Manage global assets](manage-global-assets.md).
- Learn about the role of SMA in a Windows Azure Pack implementation [SMA Whitepaper](https://gallery.technet.microsoft.com/Service-Management-fcd75828). 