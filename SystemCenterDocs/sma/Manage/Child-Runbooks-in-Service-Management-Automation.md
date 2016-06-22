---
title: Child Runbooks in Service Management Automation
ms.custom: na
ms.prod: system-center-2012-r2
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4ccce671-6f5e-405c-a007-05f2e43f7124
---
# Child Runbooks in Service Management Automation
It is a best practice in Service Management Automation to write reusable, modular runbooks with a discrete function that can be used by other runbooks. A parent runbook will often call one or more child runbooks to perform required functionality. There are two ways to call a child runbook, and each has distinct differences that you should understand so that you can determine which will be best for your different scenarios.

## <a name="InlineExecution"></a>Invoking a Child Runbook Using Inline Execution
To invoke a runbook inline from another runbook, you use the name of the runbook and provide values for its parameters exactly like you would use an activity or cmdlet.  All runbooks in the same Service Management Automation environment are available to all others to be used in this manner. The parent runbook will wait for the child runbook to complete before moving to the next line, and any output is returned directly to the parent.

When you invoke a runbook inline, it runs in the same job as the parent runbook. There will be no indication in the job history of the child runbook that it ran. Any exceptions and any stream output from the child runbook will be associated with the parent. This results in fewer jobs and makes them easier to track and to troubleshoot since any exceptions thrown by the child runbook and any of its stream output are associated with the parent runbook’s job.

When a runbook is published, any child runbooks that it calls must already have a published version. This is because Automation builds an association with any child runbooks when a runbook is compiled. If they aren’t, the parent runbook will appear to publish properly, it but will generate an exception when it’s started. If this happens, you can republish the parent runbook in order to properly reference the child runbooks. You do not need to republish the parent runbook if any of the child runbooks are changed because the association will have already been created.

The parameters of a child runbook called inline can be any data type including complex objects, and there is no [JSON serialization](Starting-a-Runbook.md#Parameters) as there is when you start the runbook using the Management Portal or with the [Start\-SmaRunbook](http://aka.ms/runbookauthor/cmdlet/startsmarunbook) cmdlet.

### Runbook types

A runbook can only use another runbook of the same [type](Runbook-Types-in-Service-Management-Automation.md) as a child runbook using inline execution.  This means that a [PowerShell Workflow runbook](Runbook-Types-in-Service-Management-Automation.md)  cannot use a [PowerShell runbook](Runbook-Types-in-Service-Management-Automation.md) as a child using inline execution, and a PowerShell runbook cannot use a PowerShell Workflow runbook.

When you call a PowerShell Workflow child runbook using inline execution, you just use the name of the runbook.  When you call a PowerShell child runbook, you must preceded its name with *.\\* to specify that the script is located in the local directory. 

### Example

The following example invokes a test child runbook that accepts three parameters, a complex object, an integer, and a boolean. The output of the child runbook is assigned to a variable.  In this case, the child runbook is a PowerShell Workflow runbook

```powershell
$vm = Get-VM –Name "MyVM" –ComputerName "MyServer"
$output = Test-ChildRunbook –VM $vm –RepeatCount 2 –Restart $true
```

Following is the same example using a PowerShell script runbook as the child.
```powershell
$vm = Get-VM –Name "MyVM" –ComputerName "MyServer"
$output = .\Test-ChildRunbook.ps1 –VM $vm –RepeatCount 2 –Restart $true
```

## <a name="cmdlet"></a>Starting a Child Runbook Using Cmdlet
You can use the [Start\-SMARunbook](http://aka.ms/runbookauthor/cmdlet/startsmarunbook) cmdlet to start a runbook as described in [To start a runbook with Windows PowerShell](assetId:///6ff9b0b3-d210-4463-96a1-cbab272eac4c#PowerShell). When you start a child runbook from a cmdlet, the parent runbook will move to the next line as soon as the job is created for the child runbook. If you need to retrieve any output from the runbook, then you need to access the job using [Get\-SMAJobOutput](http://aka.ms/runbookauthor/getsmajoboutput).

The job from a child runbook started with a cmdlet will run in a separate job from the parent runbook. This results in more jobs than invoking the workflow inline, increasing overhead on the worker server, and making them more difficult to track. The parent can start multiple child runbooks though without waiting for each to complete. For that same kind of parallel execution calling the child runbooks inline, the parent runbook would need to use the [parallel keyword](http://aka.ms/runbookauthor/parallel).

Parameters for a child runbook started with a cmdlet are provided as a hashtable as described in [Runbook Parameters](Starting-a-Runbook.md#Parameters). Only simple data types can be used, although you can provide the name of a credential asset as described in [Credentials](Starting-a-Runbook.md#Credentials). If the runbook has a parameter with a complex data type, then it must be called inline.

The following example starts a child runbook with parameters and then waits for it to complete. Once completed, its output is collected from the job by the parent runbook.

```powershell
$webServer = 'https://MyServer'
$port = 9090
$runbookName = "Test-Runbook"
$params = @{"VMName"="MyVM";"RepeatCount"=2;"Restart"=$true} 

$job = Start-SmaRunbook –WebServiceEndpoint $webServer –Port $port –Name $runbookName –Parameters $params

$doLoop = $true
While ($doLoop) {
   $job = Get-SmaJob –WebServiceEndpoint $webServer –Port $port -Id $job.Id
   $status = $job.Status
   $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped") 
}

Get-SmaJobOutput –WebServiceEndpoint $webServer –Port $port -Id $job.Id –Stream Output
```

## Comparison of Methods for Calling a Child Runbook
The following table summarizes the differences between the two methods for calling a runbook from another runbook.

||Inline|Cmdlet|
|-|----------|----------|
|Job|Child runbooks run in the same job as the parent.|A separate job is created for the child runbook.|
|Execution|Parent runbook waits for the child runbook to complete before continuing.|Parent runbook continues immediately after child runbook is started.|
|Output|Parent runbook can directly get output from child runbook.|Parent runbook must retrieve output from child runbook job.|
|Parameters|Values for the child runbook parameters are specified separately and can use any data type.|Values for the child runbook parameters must be combined into a single hashtable and can only include simple, array, and object data types that leverage JSON serialization.|
|Publishing|Child runbook must be published before parent runbook is published.|Child runbook must be published any time before parent runbook is started.|

## See Also
[To start a runbook with Windows PowerShell](Starting-a-Runbook.md#PowerShell)
[Authoring Automation Runbooks](Authoring-Automation-Runbooks.md)
[Automation Runbooks](Automation-Runbooks.md)
[Runbook types](Runbook-Types-in-Service-Management-Automation.md)


