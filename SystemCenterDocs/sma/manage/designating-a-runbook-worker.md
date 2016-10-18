---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bwren
ms.prod:  system-center-threshold
keywords:  
ms.date: 10/12/2016
title:  Designating a runbook worker
ms.technology:  service-management-automation
ms.assetid:  
---

# Designating a runbook worker

When you start a runbook job in Service Management Automation, by default, it is picked by a runbook worker selected at random. However, sometimes you might want to run a runbook against a particular runbook worker for various reasons. RunbookWorker configuration property helps you achieve that. For more information on how runbooks are executed, see [Runbook Execution in Service Management Automation](../get-started/runbook-execution-in-service-management-automation.md).


## Designating a runbook worker through the PowerShell ISE Add-on.

- In the SMA ISE Add-on, under the **Configuration** tab,
sign in using your SMA account.
- On successful login, you can see your runbooks in the **Runbooks** tab.
- In the **Runbooks** tab, select one or more runbooks which you want to be executed against a particular runbook worker.
- Click on **configure** button in the bottom pane.
- In the **Configure Runbook properties** dialog, select a runbook worker from the drop-down menu. Click **Make changes**.


## Designating a runbook worker through the SMA PowerShell Module

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
