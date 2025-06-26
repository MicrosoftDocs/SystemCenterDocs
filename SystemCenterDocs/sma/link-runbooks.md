---
description: Provides an overview of how you can call one or more child runbooks.
ms.topic: concept-article
author: jyothisuri
ms.author: jsuri
ms.service: system-center
ms.date: 11/01/2024
title: Child runbooks in Service Management Automation
ms.subservice: service-management-automation
ms.custom: UpdateFrequency2, engagement-fy24
---

# Child runbooks in Service Management Automation

It's a best practice in Service Management Automation (SMA) to write reusable, modular runbooks with a discrete function that can be used by other runbooks. A parent runbook will often call one or more child runbooks to perform the required functionality. There are two ways to call a child runbook, and each has distinct differences that you should understand so that you can determine which will be the best for your different scenarios.

## Invoke a child runbook using inline execution

To invoke a runbook inline from another runbook, you use the name of the runbook and provide values for its parameters exactly like you would use an activity or cmdlet.  All runbooks in the same SMA environment are available to all others to be used in this manner. The parent runbook will wait for the child runbook to complete before moving to the next line, and any output is returned directly to the parent.

When you invoke a runbook inline, it runs in the same job as the parent runbook. There will be no indication in the job history of the child runbook that it ran. Any exceptions and any stream output from the child runbook will be associated with the parent. This results in fewer jobs and makes them easier to track and to troubleshoot since any exceptions thrown by the child runbook and any stream outputs that are associated with the parent runbook job.

When a runbook is published, any child runbooks that it calls must already have a published version. This is because Automation builds an association with any child runbooks when a runbook is compiled. If they aren't, the parent runbook will appear to publish properly, but it will generate an exception when it's started. If this happens, you can republish the parent runbook in order to properly reference the child runbooks. You don't need to republish the parent runbook if any of the child runbooks are changed because the association will have already been created.

The parameters of a child runbook called inline can be any data type, including complex objects, and there's no [JSON serialization](manage-runbooks.md) as there's when you start the runbook using the Management Portal or with the [Start-SmaRunbook](/previous-versions/system-center/powershell/system-center-2012-r2/dn502564(v=sc.20)) cmdlet.

### Runbook types

A runbook can only use another runbook of the same [type](./authoring-automation-runbooks.md) as a child runbook using inline execution. This means that a [PowerShell Workflow runbook](./authoring-automation-runbooks.md) can't use a [PowerShell runbook](./authoring-automation-runbooks.md) as a child using inline execution, and a PowerShell runbook can't use a PowerShell Workflow runbook.

When you call a PowerShell Workflow child runbook using inline execution, you just use the name of the runbook. When you call a PowerShell child runbook, you must precede its name with *.\\* to specify that the script is located in the local directory.

### Example

The following example invokes a test child runbook that accepts three parameters, a complex object, an integer, and a boolean. The output of the child runbook is assigned to a variable. In this case, the child runbook is a PowerShell Workflow runbook.

```powershell
$vm = Get-VM -Name "MyVM" -ComputerName "MyServer"
$output = Test-ChildRunbook -VM $vm -RepeatCount 2 -Restart $true
```

Following is the same example using a PowerShell script runbook as the child.

```powershell
$vm = Get-VM -Name "MyVM" -ComputerName "MyServer"
$output = .\Test-ChildRunbook.ps1 -VM $vm -RepeatCount 2 -Restart $true
```

## Start a child runbook using cmdlets

You can use the [Start-SMARunbook](/previous-versions/system-center/powershell/system-center-2012-r2/dn502564(v=sc.20)) cmdlet [to start a runbook with Windows PowerShell](manage-runbooks.md). When you start a child runbook from a cmdlet, the parent runbook will move to the next line as soon as the job is created for the child runbook. If you need to retrieve any output from the runbook, then you need to access the job using [Get-SMAJobOutput](https://aka.ms/runbookauthor/getsmajoboutput).

The job from a child runbook started with a cmdlet will run in a separate job from the parent runbook. This results in more jobs than invoking the workflow inline, increasing overhead on the worker server and making them more difficult to track. The parent can start multiple child runbooks though without waiting for each to complete. For that same kind of parallel execution calling the child runbooks inline, the parent runbook would need to use the [parallel keyword](./overview-powershell-workflows.md).

Parameters for a child runbook started with a cmdlet are provided as a hashtable as described in [Runbook Parameters](manage-runbooks.md). Only simple data types can be used, although you can provide the name of a credential asset as described in [Credentials](manage-runbooks.md). If the runbook has a parameter with a complex data type, then it must be called inline.

The following example starts a child runbook with parameters and then waits for it to complete. Once completed, its output is collected from the job by the parent runbook.

```powershell
$webServer = 'https://MyServer'
$port = 9090
$runbookName = "Test-Runbook"
$params = @{"VMName"="MyVM";"RepeatCount"=2;"Restart"=$true}

$job = Start-SmaRunbook -WebServiceEndpoint $webServer -Port $port -Name $runbookName -Parameters $params

$doLoop = $true
While ($doLoop) {
   $job = Get-SmaJob -WebServiceEndpoint $webServer -Port $port -Id $job.Id
   $status = $job.Status
   $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped")
}

Get-SmaJobOutput -WebServiceEndpoint $webServer -Port $port -Id $job.Id -Stream Output
```

## Compare methods for calling a child runbook

The following table summarizes the differences between the two methods for calling a runbook from another runbook.

||Inline|Cmdlet|
|-|----------|----------|
|**Job**|Child runbooks run in the same job as the parent.|A separate job is created for the child runbook.|
|**Execution**|Parent runbook waits for the child runbook to complete before continuing.|Parent runbook continues immediately after child runbook is started.|
|**Output**|Parent runbook can directly get output from child runbook.|Parent runbook must retrieve output from child runbook job.|
|**Parameters**|Values for the child runbook parameters are specified separately and can use any data type.|Values for the child runbook parameters must be combined into a single hashtable and can only include simple, array, and object data types that use JSON serialization.|
|**Publishing**|Child runbook must be published before parent runbook is published.|Child runbook must be published anytime before a parent runbook is started.|

## Next steps

- Learn about [automation runbooks](./manage-runbooks.md).
