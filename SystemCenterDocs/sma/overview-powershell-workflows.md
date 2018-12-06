---
title: Windows PowerShell Workflow Concepts
description: Provides a brief overview of critical features of workflows that are common to Automation runbooks.
manager: carmon
ms.topic: article
author: rayne-wiselman
ms.author: raynew
ms.prod: system-center
ms.date: 05/08/2018
ms.technology: service-management-automation
---

# Windows PowerShell Workflow Concepts

One [type of runbook](manage/runbook-types-in-service-management-automation.md) for Service Management Automation is based on Windows PowerShell Workflows. This section provides a brief overview of critical features of workflows that are common to Automation runbooks. Complete details on workflows are available in [Getting Started with Windows PowerShell Workflow](https://go.microsoft.com/fwlink/?LinkID=324602).

The runbook structure is identical between runbooks for Service Management Automation and for [Microsoft Azure Automation](http://aka.ms/runbookauthor/azure) although the two will typically work with different resources.

## Windows PowerShell Workflows
A workflow is a sequence of programmed, connected steps that perform long-running tasks or require the coordination of multiple steps across multiple devices or managed nodes. The benefits of a workflow over a normal script include the ability to simultaneously perform an action against multiple devices and the ability to automatically recover from failures. A Windows PowerShell Workflow is a Windows PowerShell script that leverages Windows Workflow Foundation. While the workflow is written with Windows PowerShell syntax and launched by Windows PowerShell, it is processed by Windows Workflow Foundation.

### Basic Structure
A Windows PowerShell Workflow starts with the **Workflow** keyword followed by the body of the script enclosed in braces. The name of the workflow follows the **Workflow** keyword as shown in the following syntax. The name of the workflow matches the name of the Automation runbook.

```powershell
Workflow Test-Runbook
{
   <Commands>
}
```

To add parameters to the workflow, use the **Param** keyword as shown in the following syntax. The management Portal will prompt the user to provide values for these parameters when they start the runbook. This sample uses the optional Parameter attribute which specifies whether or not the parameter is mandatory.

```powershell
Workflow Test-Runbook
{
  Param
  (
   [Parameter(Mandatory=<$True | $False>]
   [Type]$<ParameterName>,

   [Parameter(Mandatory=<$True | $False>]
   [Type]$<ParameterName>
  )
  <Commands>
}
```

### Naming
The name of the workflow should conform to the Verb-Noun format that is standard with Windows PowerShell. You can refer to [Approved Verbs for Windows PowerShell Commands](https://go.microsoft.com/fwlink/?LinkID=324604) for a list of approved verbs to use. The name of the workflow must match the name of the Automation runbook. If the runbook is being imported, then the filename must match the workflow name and must end in .ps1.

### Limitations
For a complete list of limitations and syntax differences between Windows PowerShell Workflows and Windows PowerShell, see [Syntactic Differences Between Script Workflows and Scripts](https://technet.microsoft.com/library/jj574140.aspx).

## Activities
An activity is a specific task in a workflow. Just as a script is composed of one or more commands, a workflow is composed of one or more activities that are carried out in a sequence. Windows PowerShell Workflow automatically converts many of the Windows PowerShell cmdlets to activities when it runs a workflow. When you specify one of these cmdlets in your runbook, the corresponding activity is actually run by Windows Workflow Foundation. For those cmdlets without a corresponding activity, Windows PowerShell Workflow automatically runs the cmdlet within an [InlineScript](#bkmk_InlineScript) activity. There is a set of cmdlets that are excluded and cannot be used in a workflow unless you explicitly include them in an [InlineScript](#bkmk_InlineScript) block. For further details on these concepts, see [Using Activities in Script Workflows](https://go.microsoft.com/fwlink/?LinkID=324983).

Workflow activities share a set of common parameters to configure their operation. For details about the workflow common parameters, see [about_WorkflowCommonParameters](https://go.microsoft.com/fwlink/?LinkID=324606).

## Integration Modules
An *Integration Module* is a package that contains a [Windows PowerShell Module](https://go.microsoft.com/fwlink/?LinkID=325518) and can be imported into Automation. Windows PowerShell Modules contain cmdlets that can be used in Automation runbooks. Products and services such as Operations Manager and Azure have modules that include cmdlets specific to their operation.

Integration Modules that are imported into Automation are automatically available to all runbooks. Since Automation is based on Windows PowerShell 4.0, it supports auto loading of modules meaning that cmdlets from installed modules can be used without importing them into the script with [Import-Module](https://go.microsoft.com/fwlink/?LinkID=324984).

Any Windows PowerShell module can be imported into Automation as long as all of its dependencies can be located in a single folder. If the module depends on registry settings or files not in the default path, then it can be imported, but it will most likely not work because Automation will not be able to locate its dependencies. Modules with external dependencies can be used in a runbook by installing them on another host using and then accessing them with an [InlineScript](overview-powershell-workflows.md#bkmk_InlineScript) script block.

With Service Management Automation, you can use modules with external dependencies by installing them on each Worker server. While the cmdlets in these modules can be used in runbooks, they will not be discovered by Automation to support such features as the Insert Activity wizard. In order to use this feature, you can create a Portable module using the **New-SmaPortableModule** cmdlet. This cmdlet creates a module that includes a stub for each of its cmdlets and can be imported into Automation. When a runbook uses one of those cmdlets, the stub redirects the call to the actual cmdlet in the external module. That module must be installed on each Worker server or the call will fail.

## <a name="Parallel"></a>Parallel Execution
One advantage of Windows PowerShell Workflows is the ability to perform a set of commands in parallel instead of sequentially as with a typical script. This is particularly useful in runbooks since they may perform multiple actions that take a significant time to complete. For example, a runbook might provision a set of virtual machines. Rather than performing each provisioning process in sequence with one another, the actions could be performed simultaneously increasing overall efficiency. Only when all are complete would the runbook continue.

You can use the **Parallel** keyword to create a script block with multiple commands that will run concurrently. This uses the syntax shown below. In this case, Activity1 and Activity2 will start at the same time. Activity3 will start only after both Activity1 and Activity2 have completed.

```powershell
Parallel
{
  <Activity1>
  <Activity2>
}
<Activity3>
```

You can use the **ForEach -Parallel** construct to process commands for each item in a collection concurrently. The items in the collection are processed in parallel while the commands in the script block run sequentially. This uses the syntax shown below. In this case, Activity1 will start at the same time for all items in the collection. For each item, Activity2 will start after Activity1 is complete. Activity3 will start only after both Activity1 and Activity2 have completed for all items.

```powershell
ForEach -Parallel ($<item> in $<collection>)
{
  <Activity1>
  <Activity2>
}
<Activity3>
```

The **Sequence** keyword is used to run commands in sequence within a **Parallel** script block. The **Sequence** script block runs in parallel with other commands, but the commands within the block run sequentially. This uses the syntax shown below. In this case, Activity1, Activity2, and Activity3 will start at the same time. Activity4 will start only after Activity3 has completed. Activity5 will start after all other activities have completed

```powershell
Parallel
{
  <Activity1>
  <Activity2>

  Sequence
  {
   <Activity3>
   <Activity4>
  }
}
<Activity5>
```

## Checkpoints
A checkpoint is a snapshot of the current state of the workflow that includes the current value for variables and any output generated to that point. The last checkpoint to complete in a runbook is saved to the Automation database so that the workflow can resume even in the case of an outage. The checkpoint data is removed once the runbook job is complete.

You can set a checkpoint in a workflow with the **Checkpoint-Workflow** activity. When you include this activity in a runbook, a checkpoint is immediately taken. If the runbook is suspended by an error, when the job is resumed, it will resume from the point of the last checkpoint set.

In the following sample code, an error occurs after Activity2 causing the runbook to suspend. When the job is resumed, it starts by running Activity2 since this was just after the last checkpoint set.

```powershell
<Activity1>
Checkpoint-Workflow
<Activity2>
<Error>
<Activity3>
```

You should set checkpoints in a runbook after activities that may be prone to error and should not be repeated if the runbook is resumed. For example, your runbook may create a virtual machine. You could set a checkpoint both before and after the commands to create the virtual machine. If the creation fails, then the commands are repeated when the runbook is resumed. If the creation succeeds but the runbook later fails, then the virtual machine will not be created again when the runbook is resumed.

For more information about checkpoints, see [Adding Checkpoints to a Script Workflow](https://go.microsoft.com/fwlink/?LinkID=324993).

## Suspend a Runbook
You can force a runbook to suspend itself with the **Suspend-Workflow** activity. This activity will set a checkpoint and cause the workflow to immediately suspend. Suspending a workflow is useful for runbooks that may require a manual step to be performed before another set of activities are run.

For more information about suspending a workflow, see [Making a Workflow Suspend Itself](https://go.microsoft.com/fwlink/?LinkID=324997).

## InlineScript
The **InlineScript** activity runs a block of commands in a separate, non-workflow session and returns its output to the workflow. While commands in a workflow are sent to Windows Workflow Foundation for processing, commands in an InlineScript block are processed by Windows PowerShell. The activity uses the standard workflow common parameters including **PSComputerName** and **PSCredential** which allow you to specify that the code block be run on another computer or using alternate credentials.

InlineScript uses the syntax shown below.

```powershell
InlineScript
{
  <Script Block>
} <Common Parameters>
```

The most common use for **InlineScript** in a runbook is to run a block of code on another computer. This is required when cmdlets in your runbook are not installed in Automation or if the action only has permissions to be performed locally on the target computer. This is illustrated in the following diagram.

![Inline script diagram](/system-center/sma/media/overview-powershell-workflows/smaauth_inlinescript.png)

In order to run the code block on another computer, the **PSComputer** and **PSCredential** parameters are used with the **InlineScript** activity. A global resource such as a [Credential](~/sma/manage-global-assets.md) or [Connection](~/sma/manage-global-assets.md) is typically used in a runbook to provide values for these parameters. The following sample code runs a set of commands on a computer represented by a connection called MyConnection.

```powershell
$con = Get-AutomationConnection -Name 'MyConnection'
$securepassword = ConvertTo-SecureString -AsPlainText -String $con.Password -Force
$cred = New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $con.Username, $securepassword
InlineScript
{
  <Commands>
} "PSComputer $con.ComputerName "PSCredential $cred
```

While **InlineScript** activities may be critical in certain runbooks, they should only be used when necessary for the following reasons:

-   You cannot use checkpoints from within an **InlineScript** block. If a failure occurs within the block, it must be resumed from the beginning.

-   **InlineScript** affects scalability of the runbook since it holds the Windows PowerShell session for the entire length of the InlineScript block.

-   Activities such as **Get-AutomationVariable** and **Get-AutomationPSCredential** are not available in an InlineScript block.

If you do need to use an **InlineScript**, you should minimize its scope. For example, if your runbook iterates over a collection while applying the same operation to each item, the loop should occur outside of the **InlineScript**. This will provide the following advantages:

-   You can [checkpoint](#BK_Checkpoints) the workflow after each iteration. If the job is suspended or interrupted and resumed, the loop will be able to resume.

-   You can use **ForEach "Parallel** to handle collection items concurrently.

Keep the following recommendations in mind if you do use an **InlineScript** in your runbook:

-   You can pass values into the script though with the **$Using** scope modifier. For example, a variable called $abc that has been set outside of the InlineScript would become $using:abc inside an **InlineScript**.

-   To return output from an **InlineScript**, assign the output to a variable and output any data to be returned to the output stream. The following example assigns the string "hi" to a variable called $output.

    ```
    $output = InlineScript { Write-Output "hi" }
    ```

-   Avoid defining workflows within **InlineScript** scope. Even though some workflows may appear to operate correctly, this is not a tested scenario. As a result, you may encounter confusing error messages or unexpected behavior.

For further details on using **InlineScript**, see [Running Windows PowerShell Commands in a Workflow](https://go.microsoft.com/fwlink/?LinkID=324625) and [about_InlineScript](https://go.microsoft.com/fwlink/?LinkID=324624).

## Next steps

[Author automation runbooks](authoring-automation-runbooks.md)
