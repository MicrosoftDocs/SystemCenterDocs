---
title: Runbook Types in Service Management Automation
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 757a0f53-b84a-404b-85fb-bfe1c065c599
---
# Runbook Types in Service Management Automation
Service Management Automation (SMA) supports two types of runbooks that are  briefly described in the following table.  The sections below provide further information about each type including considerations on when to use each.


| Type |  Description |
|:---|:---|
| PowerShell Workflow | Text runbook based on Windows PowerShell Workflow. |
| PowerShell | Text runbook based on Windows PowerShell script. |


## PowerShell Workflow runbooks

PowerShell Workflow runbooks are based on Windows PowerShell Workflow.  You directly edit the code of the runbook using the editor in the Management Portal.  You can also use any offline text editor and [import the runbook](Creating-or-Importing-a-Runbook.md) into SMA.

### Advantages

- Implement all complex logic with PowerShell Workflow code.
- Use [checkpoints](Windows-PowerShell-Workflow-Concepts.md#BK_Checkpoints) to resume runbook in case of error.
- Use [parallel processing](Windows-PowerShell-Workflow-Concepts.md#Parallel) to perform multiple actions in parallel.
- Can include other PowerShell Workflow runbooks as child runbooks to create high level workflows.


### Limitations

- Author must be familiar with PowerShell Workflow.
- Runbook must deal with the additional complexity of PowerShell Workflow such as deserialized objects.
- Runbook takes longer to start than PowerShell runbooks since it needs to be compiled before running.
- PowerShell runbooks can only be included as child runbooks by using the Start-SMARunbook cmdlet which creates a new job.


## PowerShell runbooks

PowerShell runbooks are based on Windows PowerShell.  You directly edit the code of the runbook using the editor in the Management Portal.  You can also use any offline text editor and [import the runbook](Creating-or-Importing-a-Runbook.md) into SMA.

### Advantages

- Implement all complex logic with PowerShell code without the additional complexities of PowerShell Workflow. 
- Runbook starts faster than PowerShell Workflow runbooks since it doesn't need to be compiled before running.

### Limitations

- Must be familiar with PowerShell scripting.
- Can't use [parallel processing](Windows-PowerShell-Workflow-Concepts.md#Parallel) to perform multiple actions in parallel.
- Can't use [checkpoints](Windows-PowerShell-Workflow-Concepts.md#BK_Checkpoints)  to resume runbook in case of error.
- PowerShell Workflow runbooks can only be included as child runbooks by using the Start-SMARunbook cmdlet which creates a new job.

### Known Issues
Following are current known issues with PowerShell runbooks.

- PowerShell runbooks cannot cannot retrieve an unencrypted [variable asset](Variables.md) with a null value.
- PowerShell runbooks cannot retrieve a [variable asset](Variables.md) with *~* in the name.
- Get-Process in a loop in a PowerShell runbook may crash after about 80 iterations. 
- A PowerShell runbook may fail if it attempts to write a very large amount of data to the output stream at once.   You can typically work around this issue by outputting just the information you need when working with large objects.  For example, instead of outputting something like *Get-Process*, you can output just the required fields with *Get-Process | Select ProcessName, CPU*.

## Considerations

You should take into account the following additional considerations when determining which type to use for a particular runbook.

- You can't convert runbooks from one type to another.
- There are limitations using runbooks of different types as a child runbook.  See [Child runbooks in Service Management Automation](Child-Runbooks-in-Service-Management-Automation.md) for more information.



