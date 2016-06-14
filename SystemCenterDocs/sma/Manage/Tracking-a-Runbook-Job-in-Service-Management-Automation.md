---
title: Tracking a Runbook Job in Service Management Automation
ms.custom: na
ms.prod: system-center-2012-r2
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 24cd18c8-4aea-4f22-971b-756d9fa45a8e
---
# Tracking a Runbook Job in Service Management Automation
When you start a runbook in [!INCLUDE[sma_1](../../includes/sma_1_md.md)], a job is created. A job is a single execution instance of a runbook. A single runbook may have multiple jobs, each with their own set of values for the runbook’s parameters. 

If the RunbookWorker property of the runbook is populated, then that Worker server will service the job. If the Worker server is not available, then the job will fail with an error. If the RunbookWorker property of the runbook is not populated, then SMA will randomly select an available Worker server to service the request.

The following diagram shows the lifecycle of a runbook job for PowerShell Workflow runbooks.

![Job Statuses - PowerShell WorkflowImage/sma-runbook-execution-workflow.png)

The following diagram shows the lifecycle of a runbook job for PowerShell script runbooks.

![Job Statuses - PowerShell ScriptImage/sma-runbook-execution-script.png)

## <a name="jobstatuses"></a>Job Statuses
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

## <a name="Portal"></a>Viewing Job Status using the Management Portal

### Automation Dashboard
The Automation Dashboard shows a summary of all of the runbooks in the [!INCLUDE[sma_1](../../includes/sma_1_md.md)] environment. The summary graph shows the number of total jobs for all runbooks that entered each status over a given number of days or hours. You can select the time range on the top right corner of the graph. The time axis of the chart will change according to the type of time range that you select. You can choose whether to display the line for a particular status by clicking on it at the top of screen.

You can use the following steps to display the Automation Dashboard.

1.  In the Management Portal, select **Automation**.

2.  Select the **Dashboard** tab.

### Runbook Dashboard
The Runbook Dashboard shows a summary for a single runbook. The summary graph shows the number of total jobs for the runbook that entered each status over a given number of days or hours. You can select the time range on the top right corner of the graph. The time axis of the chart will change according to the type of time range that you select. You can choose whether to display the line for a particular status by clicking on it at the top of screen.

You can use the following steps to display the Runbook Dashboard.

1.  In the Management Portal, select **Automation**.

2.  Click the name of a runbook.

3.  Select the **Dashboard** tab.

### Job Summary, History, and Source
You can view a list of all of the jobs that have been created for a particular runbook and their most recent status. You can filter this list by job status and the range of dates for the last change to the job. Click on the name of a job to view its detailed information and its output. The detailed view of the job includes the values for the runbook parameters that were provided to that job.

The job history includes output, warning, and error messages with time stamps of when the record was created. For more information on records that are written to the job history, see [Runbook Output and Messages](Runbook-Output-and-Messages.md).

The source for a job is the source code of the workflow when the job was run. This may not be the same as the current version of the runbook if it was updated after the job was run.

You can use the following steps to view the jobs for a runbook.

1.  In the Management Portal, select **Automation**.

2.  Click the name of a runbook.

3.  Select the **Jobs** tab.

4.  Click on the **Job Created** column for a job to view its detail and output.

5.  Select the **History** tab to view the job history. Select a history record and click **View Details** at the bottom of the screen for a detailed view of the record.

6.  From the **History** tab, click **View Source** at the bottom of the screen to the source for the job.

## <a name="PowerShell"></a>Retrieving Job Status using Windows PowerShell
You can use the [Get\-SmaJob](http://aka.ms/runbookauthor/cmdlet/getsmajob) to retrieve the jobs created for a runbook and the details of a particular job. If you start a runbook with Windows PowerShell using [Start\-SmaRunbook](http://aka.ms/runbookauthor/cmdlet/startsmarunbook), then it will return the resulting job. Use [Get\-SmaJobOutput](http://aka.ms/runbookauthor/cmdlet/getsmajoboutput) to get a job’s output.

The following sample commands retrieves the last job for a sample runbook and displays its status, the values provide for the runbook parameters, and the output from the job.

```powershell
$webServer = 'https://MyServer'
$port = 9090
$runbookName = "Test-Runbook"

$job = (Get-SmaJob –WebServiceEndpoint $webServer –Port $port –RunbookName $runbookName | sort LastModifiedDate –desc)[0]
$job.Status
$job.JobParameters
Get-SmaJobOutput –WebServiceEndpoint $webServer –Port $port -Id $job.Id –Stream Output
```

## See Also
[Service Management Automation](../Service-Management-Automation.md)
[Runbook Operations](Runbook-Operations.md)
[Starting a Runbook](Starting-a-Runbook.md)


