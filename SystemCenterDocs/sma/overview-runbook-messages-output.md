---
description: Provides an overview of how you can use different output stream in your runbooks.
ms.topic: article
author: jyothisuri
ms.author: jsuri
ms.service: system-center
keywords:
ms.date: 02/26/2025
title: Runbook Output and Messages
ms.subservice: service-management-automation
ms.custom: UpdateFrequency2, engagement-fy24
---

# Runbook output and messages

Most automation runbooks will have some form of output such as an error message to the user or a complex object intended to be consumed by another workflow. Windows PowerShell provides [multiple streams](/archive/blogs/) to send output from a workflow. Service Management Automation works with each of these streams differently, and you should follow best practices for how to use each when you're creating a runbook.

The following table provides a brief description of each of the streams and their behavior in the Management Portal both when running a published runbook and when [testing a runbook](./authoring-automation-runbooks.md). Further details on each stream are provided in the subsequent sections.

|Stream|Description|Published|Test|
|----------|---------------|-------------|--------|
|Output|Objects intended to be consumed by other runbooks.|Written to the job history.|Displayed in the Test Output Pane.|
|Warning|Warning message intended for the user.|Written to the job history.|Displayed in the Test Output Pane.|
|Error|Error message intended for the user. Unlike an exception, the runbook continues after an error message by default.|Written to the job history.|Displayed in the Test Output Pane.|
|Verbose|Messages providing general or troubleshooting information.|Written to job history only if verbose logging is turned on for the runbook.|Displayed in the Test Output pane only if [$VerbosePreference](overview-runbook-messages-output.md#preference-variables) is set to **Continue** in the runbook.|
|Progress|Records automatically generated before and after each activity in the runbook. The runbook shouldn't attempt to create its own progress records since they're intended for an interactive user.|Written to job history only if progress logging is turned on for the runbook.|Not displayed in the Test Output Pane.|
|Debug|Messages intended for an interactive user. Shouldn't be used in runbooks.|Not written to job history.|Not written to Test Output Pane.|

## Output stream

The Output stream is intended for output of objects created by a workflow when it runs correctly. In Automation, this stream is primarily used for objects intended to be consumed by [parent runbooks that call the current runbook](~/sma/link-runbooks.md). When you [call a runbook inline](~/sma/link-runbooks.md#invoke-a-child-runbook-using-inline-execution) from a parent runbook, it returns data from the output stream to the parent. You should only use the output stream to communicate general information back to the user if you know the runbook will never be called by another runbook. As a best practice, however, you should typically use the [Verbose Stream](overview-runbook-messages-output.md#message-streams) to communicate general information to the user.

You can write data to the output stream using [Write-Output](/powershell/module/microsoft.powershell.utility/write-output) or by putting the object on its own line in the runbook.

```powershell
#The following lines both write an object to the output stream.
Write-Output -InputObject $object
$object
```

### Output from a function

When you write to the output stream in a function that is included in your runbook, the output is passed back to the runbook. If the runbook assigns that output to a variable, then it isn't written to the output stream. Writing to any other streams from within the function will write to the corresponding stream for the runbook.

Consider the following sample runbook.

```powershell
Workflow Test-Runbook
{
   Write-Verbose "Verbose outside of function"
   Write-Output "Output outside of function"
   $functionOutput = Test-Function

   Function Test-Function
   {
      Write-Verbose "Verbose inside of function"
      Write-Output "Output inside of function"
   }
}
```

The output stream for the runbook job would be:

```powershell
Output outside of function
```

The verbose stream for the runbook job would be:

```powershell
Verbose outside of function
Verbose inside of function
```

The $functionOutput variable would have the value:

```powershell
Output inside of function
```

### Declare output data type

A workflow can specify the data type of its output using the [OutputType attribute](/powershell/module/microsoft.powershell.core/about/about_functions_outputtypeattribute). This attribute has no effect during runtime, but it provides an indication to the runbook author at design time of the expected output of the runbook. As the toolset for runbooks continues to evolve, the importance of declaring output data types at design time will increase in importance. As a result, it's a best practice to include this declaration in any runbooks that you create.

The following sample runbook outputs a string object and includes a declaration of its output type. If your runbook outputs an array of a certain type, then you should still specify the type as opposed to an array of the type.

```powershell
Workflow Test-Runbook
{
   [OutputType([string])]

   $output = "This is some string output."
   Write-Output $output
}
```

## Message streams

Unlike the output stream, message streams are intended to communicate information to the user. There are multiple message streams for different kinds of information, and each is handled differently by Automation.

Select the required tab to know more about these message streams:

# [Warning and Error streams](#tab/WarningError)

The Warning and Error streams are intended to log problems that occur in a runbook. They're written to the job history when a runbook is executed and are included in the Test Output Pane in the Management Portal when a runbook is tested. By default, the runbook will continue executing after a warning or error. You can specify that the runbook should be suspended on a warning or error by setting a [preference variable](overview-runbook-messages-output.md#preference-variables) in the runbook before creating the message. For example, to cause a runbook to suspend on an error as it would an exception, set $ErrorActionPreference to **Stop**.

Create a warning or error message using the [Write-Warning](/powershell/module/microsoft.powershell.utility/write-warning) or [Write-Error](/powershell/module/microsoft.powershell.utility/write-error) cmdlet. Activities may also write to these streams.

```powershell
#The following lines create a warning message and then an error message that will suspend the runbook.

$ErrorActionPreference = "Stop"
Write-Warning -Message "This is a warning message."
Write-Error -Message "This is an error message that will stop the runbook because of the preference variable."
```

# [Verbose stream](#tab/Verbose)

The Verbose message stream is for general information about the runbook operation. Since the [Debug Stream](overview-runbook-messages-output.md#message-streams) isn't available in a runbook, verbose messages should be used for troubleshooting information. By default, verbose messages from published runbooks won't be stored in the job history. To store verbose messages, configure published runbooks to **Log Verbose Records** on the **Configure** tab of the runbook in the Management Portal. In most cases, you should keep the default setting of not logging verbose records for a runbook for performance reasons. Turn on this option only to troubleshoot or debug a runbook.

The $VerbosePreference variable defaults to a value of **SilentlyContinue**. You don't need to change this variable in a published runbook for verbose messages to be stored. If this value is explicitly set to **SilentlyContinue** in a published runbook though, then verbose messages won't be stored even if the runbook is configured to log verbose records.

When [testing a runbook](./authoring-automation-runbooks.md), verbose messages aren't displayed even if the runbook is configured to log verbose records. To display verbose messages while testing a runbook, you must set the $VerbosePreference variable to **Continue**. With that variable set, verbose messages will be displayed in the Test Output Pane of the Management Portal.

Create a verbose message using the [Write-Verbose](/powershell/module/microsoft.powershell.utility/write-verbose) cmdlet.

```powershell
#The following line creates a verbose message.

Write-Verbose -Message "This is a verbose message."
```

# [Debug stream](#tab/Debug)

The Debug stream is intended for use with an interactive user and shouldn't be used in runbooks.

---

## Progress records

If you configure a runbook to log progress records (on the **Configure** tab of the runbook in the Management Portal), then a record will be written to the job history before and after each activity is run. In most cases, you should keep the default setting of not logging progress records for a runbook in order to maximize performance. Turn on this option only to troubleshoot or debug a runbook. When testing a runbook, progress messages aren't displayed even if the runbook is configured to log progress records.

The [Write-Progress](/powershell/module/microsoft.powershell.utility/write-progress) cmdlet isn't valid in a runbook since it is intended for use with an interactive user.

## Preference variables

Windows PowerShell uses [preference variables](/powershell/module/microsoft.powershell.core/about/about_preference_variables) to determine how to respond to data sent to different output streams. You can set these variables in a runbook to control how it will respond to data sent into different streams.

The following table lists the preference variables that can be used in runbooks with their valid and default values.

> [!NOTE]
> This table only includes the values that are valid in a runbook. Additional values are valid for the preference variables when used in Windows PowerShell outside of Service Management Automation.

|Variable|Default Value|Valid Values|
|------------|-----------------|----------------|
|WarningPreference|Continue|Stop<br />Continue<\br><br />\SilentlyContinue|
|ErrorActionPreference|Continue|Stop<br />Continue<br />SilentlyContinue|
|VerbosePreference|SilentlyContinue|Stop<br />Continue<br />SilentlyContinue|

The following table lists the behavior for the preference variable values that are valid in runbooks.

|Value|Behavior|
|---------|------------|
|Continue|Logs the message and continues executing the runbook.|
|SilentlyContinue|Continues executing the runbook without logging the message. This has the effect of ignoring the message.|
|Stop|Logs the message and suspends the runbook.|

## <a name="RetrieveOutput"></a>Retrieving Runbook Output and Messages

### Management portal

You can view the details of a runbook job in the Management Portal from the **Jobs** tab of a runbook. The **Summary** of the job will display the input parameters and the [Output Stream](overview-runbook-messages-output.md#output-stream) in addition to general information about the job and any exceptions if they occurred. The **History** will include messages from the Output Stream and [Warning and Error Streams](overview-runbook-messages-output.md#message-streams) in addition to the [Verbose Stream](overview-runbook-messages-output.md#message-streams) and [Progress Records](overview-runbook-messages-output.md#progress-records) if the runbook is configured to log verbose and progress records.

### Windows PowerShell

In Windows PowerShell, you can retrieve output and messages from a runbook using the [Get-SmaJobOutput](/previous-versions/system-center/powershell/system-center-2012-r2/dn502570(v=sc.20)) cmdlet. This cmdlet requires the ID of the job and has a parameter called **Stream** where you specify which stream to return. You can specify **Any** to return all streams for the job.

The following example starts a sample runbook and then waits for it to complete. Once completed, its output stream is collected from the job.

```powershell
$webServer = 'https://MyServer'
$port = 9090
$runbookName = "Test-Runbook"
$job = Start-SmaRunbook -WebServiceEndpoint $webServer -Port $port -Name $runbookName

$doLoop = $true
While ($doLoop) {
   $job = Get-SmaJob -WebServiceEndpoint $webServer -Port $port -Id $job.Id
   $status = $job.Status
   $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped")
}

Get-SmaJobOutput -WebServiceEndpoint $webServer -Port $port -Id $job.Id -Stream Output
```

## Next steps

[Author automation runbooks](authoring-automation-runbooks.md).
