---
description: Provides details on how you can automate operations in your Windows Azure Pack environment with Service Management Automation
manager: carmonm
ms.topic: article
author: rayne-wiselman
ms.author: raynew
ms.prod: system-center-threshold
ms.date: 05/08/2018
title: Automate Windows Azure Pack operations with runbooks
ms.technology: service-management-automation
---

# Automate Windows Azure Pack operations with Service Management Automation

You can use Service Management Automation (SMA) runbooks to automate routine operations in your Windows Azure Pack for Window Server environment. There are two distinct types of SMA runbooks:

| Type |  Description |
|:---|:---|
| PowerShell Workflow | Text runbook based on Windows PowerShell Workflow. |
| PowerShell | Text runbook based on Windows PowerShell script. |

## PowerShell workflow runbooks

PowerShell Workflow runbooks are based on Windows PowerShell Workflow.  You directly edit the code of the runbook using the editor in the Management Portal.  You can also use any offline text editor and [import the runbook](authoring-automation-runbooks.md) into SMA.

### Advantages

- Implement all complex logic with PowerShell Workflow code.
- Use [checkpoints](overview-powershell-workflows.md#checkpoints) to resume runbook in case of error.
- Use [parallel processing](overview-powershell-workflows.md) to perform multiple actions in parallel.
- Can include other PowerShell Workflow runbooks as child runbooks to create high-level workflows.


### Limitations

- You must be familiar with PowerShell Workflow.
- Runbook must deal with the additional complexity of PowerShell Workflow such as deserialized objects.
- Runbook takes longer to start than PowerShell runbooks since it needs to be compiled before running.
- PowerShell runbooks can only be included as child runbooks by using the Start-SMARunbook cmdlet which creates a new job.


## PowerShell runbooks

PowerShell runbooks are based on Windows PowerShell.  You directly edit the code of the runbook using the editor in the Management Portal.  You can also use any offline text editor and [import the runbook](authoring-automation-runbooks.md) into SMA.

### Advantages

- Implement all complex logic with PowerShell code without the additional complexities of PowerShell Workflow.
- Runbook starts faster than PowerShell Workflow runbooks since it doesn't need to be compiled before running.
### Limitations

- You must be familiar with PowerShell scripting.
- You can't use [parallel processing](overview-powershell-workflows.md) to perform multiple actions in parallel.
- You can't use [checkpoints](overview-powershell-workflows.md#checkpoints)  to resume runbooks when an error occurs.
- PowerShell Workflow runbooks can only be included as child runbooks by using the Start-SMARunbook cmdlet, which creates a new job.

## How SMA executes runbooks

Requests to start a runbook are performed by the SMA web service using either the Service Management Portal, or the [Start-SmaRunbook](http://aka.ms/runbookauthor/startsmarunbook) Windows PowerShell cmdlet. The web service writes this request to the Automation database where it is retrieved by one of the Automation Worker servers.

If the RunbookWorker property of the runbook is populated, then that Worker server will service the job.  If the Worker server is not available, then the job fails with an error.  If the RunbookWorker property of the runbook is not populated, then SMA randomly selects an available Worker server to service the request.

The Worker server creates a job that runs on the Worker server that services the request and remotely accesses any computers or other resources that it will work with. This requires the cmdlets in the runbook to be able to remotely access these resources. Alternatively, the runbook can include an [InlineScript](overview-powershell-workflows.md#inlinescript) command in order to use PowerShell Remoting to run commands locally on a target computer. This concept is illustrated in the following diagram.

![Runbook execution diagram](./media/runbook-automation/smaauth_runbookconcept.png)

If a job is suspended or interrupted, it may be resumed on a different Worker server. Because of this, you should be careful about using local resources that are not accessible to all Worker servers such as a file on a local computer. You should leverage [Global Assets](manage-global-assets.md) such as [Variables](manage-global-assets.md) as much as possible for sharing information between [checkpoints](overview-powershell-workflows.md#checkpoints).

## Permissions
In order for a runbook to perform its required actions, it must have permissions to access the resources that it works with. Runbooks in SMA always run in the context of the service account of the Automation Runbook Service. If this account does not have required permissions, then you can use either a [Credentials](manage-global-assets.md) or a [Connection](manage-global-assets.md) global resource in your runbook to run required commands using credentials with the required permissions. These credentials can either be used with a cmdlet that accepts credentials through a parameter or with [InlineScript](overview-powershell-workflows.md#inlinescript) to run a block of code using alternate credentials.

## Next steps
- Read more about [authoring automation runbooks](authoring-automation-runbooks.md).
- Read more about [Windows PowerShell workflow concepts](overview-powershell-workflows.md).
