---
title: Variables
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e7e41871-6acf-4531-970f-92e1cb86eefb
---
# Variables

>Applies To: Windows Azure Pack for Windows Server, System Center 2012 R2 Orchestrator

Automation variables are values that are available to all runbooks.  They can be created, modified, and retrieved from the management portal, Windows PowerShell, or from within a runbook. Automation variables are useful for the following scenarios:

-   Share a value between multiple runbooks.

-   Share a value between multiple jobs from the same runbook.

-   Manage a value from the management portal or from the Windows PowerShell command line that is used by runbooks.

Automation Variables are persisted so that they continue to be available even if the runbook fails.  This also allows a value to be set by one runbook that is then used by another, or is used by the same runbook the next time that it is run.

When a variable is created, you must specify its data type from the following list. This is so the management portal can display the appropriate control for the variable value. You can only assign a value of the correct type to a variable.

-   String

-   Integer

-   Boolean

-   Datetime

When a variable is created, you can specify that it be stored encrypted.  When a variable is encrypted, it is stored securely in the SMA database, and its value cannot be retrieved from the **Get-SmaVariable** cmdlet.  The only way that an encrypted value can be retrieved is from the **Get-AutomationVariable** activity in a runbook.  You can store multiple values of the defined type to a single variable by creating a hashtable.

## Windows PowerShell Cmdlets
The cmdlets in the following table are used to create and manage variables with Windows PowerShell in Service Management Automation.

|Cmdlets|Description|
|-----------|---------------|
|[Get-SmaVariable](http://go.microsoft.com/fwlink/?LinkID=306458)|Retrieves the value of an existing variable.|
|[Set-SmaVariable](http://go.microsoft.com/fwlink/?LinkID=306477)|Creates a new variable or sets the value for an existing variable.|

## Runbook Activities
The activities in the following table are used to access variables in a runbook.

|Activities|Description|
|--------------|---------------|
|Get-AutomationVariable|Retrieves the value of an existing variable.|
|Set-AutomationVariable|Sets the value for an existing variable.|

> [!NOTE]
> You should avoid using variables in the –Name parameter of Get-AutomationVariable since this can complicate discovering dependencies between runbooks and Automation variables.

## Creating a New Automation variable

### To create a new variable with the management portal

1.  Select the **Automation** workspace.

2.  At the top of the window, click **Assets**.

3.  At the bottom of the window, click **Add Setting**.

4.  Click **Add Variable**.

5.  In the **Type** dropdown, select a data type.

6.  Type a name for the variable in the **Name** box.

7.  Click the right arrow.

8.  Type in a value for the variable and specify whether to encrypt it.

9. Click the check mark to save the new variable.

### To create a new variable with Windows PowerShell in Service Management Automation
The [Set-SmaVariable](http://aka.ms/runbookauthor/cmdlet/setsmavariable) cmdlet both creates a new variable and sets the value for an existing variable.  The following sample commands show how to create a variable of type string.

```powershell
$web = 'https://MySMAServer'
$port = 9090

Set-SMAVariable –WebServiceEndpoint $web –Port $port –Name 'MyVariable' –Value 'My String'
```

## Using a variable in a runbook
Use the **Get-AutomationVariable** activity to use a variable in a runbook.

#### To use a variable in a runbook

-   The following sample code shows how to set and retrieve a variable in a runbook. In this sample, it is assumed that variables of type integer named NumberOfIterations and NumberOfRunnings and a variable of type string named SampleMessage have already been created.

    ```powershell
    $NumberOfIterations = Get-AutomationVariable -Name 'NumberOfIterations'
    $NumberOfRunnings = Get-AutomationVariable -Name 'NumberOfRunnings'
    $SampleMessage = Get-AutomationVariable -Name 'SampleMessage'
    Write-Output "Runbook has been run $NumberOfRunnings times."
    for ($i = 1; $i -le $NumberOfIterations; $i++) {
       Write-Output "$i`: $SampleMessage"
    }
    Set-AutomationVariable –Name NumberOfRunnings –Value (NumberOfRunngs += 1)
    ```

## See Also
[Service Management Automation](../Service-Management-Automation.md)
[Authoring Automation Runbooks](Authoring-Automation-Runbooks.md)
[Global Assets](Global-Assets.md)



