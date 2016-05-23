---
title: Starting a Runbook
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4190285b-64f7-44a9-95f4-f8ed816b7724
---
# Starting a Runbook
You can start a runbook in [!INCLUDE[sma_1](../../Token/sma_1_md.md)] using one of the following three methods.

-   [Management Portal](Starting-a-Runbook.md#Portal)

-   [PowerShell](Starting-a-Runbook.md#PowerShell)

-   [From another runbook](Child-Runbooks-in-../Service-Management-Automation.md)

The first two methods are documented below. Calling a runbook from another runbook is documented in [Child Runbooks](Child-Runbooks-in-../Service-Management-Automation.md).

## <a name="Portal"></a>To start a runbook from the Windows Azure Pack Management Portal

1.  In the Management Portal, select **Automation** in the left pane.

2.  Select the **Runbooks** tab.

3.  Select a runbook, and then click **Start**.

4.  If the runbook has parameters, you will be prompted to provide values with a text box for each parameter. Boolean and datetime parameters have special selectors instead of the standard text box. See [Runbook Parameters](Starting-a-Runbook.md#Parameters) below for further details on parameters.

5.  Either select **View Job** next to the **Starting runbook** message or select the **Jobs** tab for the runbook to view the job’s status.

## <a name="PowerShell"></a>To start a runbook with Windows PowerShell
You can use the [Start\-SmaRunbook](http://aka.ms/runbookauthor/cmdlet/startsmarunbook) to start a runbook with Windows PowerShell. The following sample code starts a runbook called Test\-Runbook.

```powershell
$webServer = 'https://MyServer'
$port = 9090
$runbookName = "Test-Runbook"
Start-SmaRunbook –WebServiceEndpoint $webServer –Port $port –Name $runbookName
```

Start\-SmaRunbook returns a job object that you can use to track its status once the runbook is started. You can then use this job object with [Get\-SmaJob](http://aka.ms/runbookauthor/cmdlet/getsmajob) to determine the status of the job and [Get\-SmaJobOutput](http://aka.ms/runbookauthor/cmdlet/getsmajoboutput) to get its output. The following sample code starts a runbook called Test\-Runbook, waits until it has completed, and then displays its output.

```powershell
$webServer = 'https://MyServer'
$port = 9090
$runbookName = "Test-Runbook"

$job = Start-SmaRunbook –WebServiceEndpoint $webServer –Port $port –Name $runbookName

$doLoop = $true
While ($doLoop) {
   $job = Get-SmaJob –WebServiceEndpoint $webServer –Port $port -Id $job.Id
   $status = $job.Status
   $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped") 
}

Get-SmaJobOutput –WebServiceEndpoint $webServer –Port $port -Id $job.Id –Stream Output
```

If the runbook requires parameters, then you must provide them as a [hashtable](http://aka.ms/runbookauthor/hashtables) where the key of the hashtable matches the parameter name and the value is the parameter value. The following example shows how to start a runbook with two string parameters named FirstName and LastName, an integer named RepeatCount, and a boolean parameter named Show. For additional information on parameters, see [Runbook Parameters](Starting-a-Runbook.md#Parameters) below.

```powershell
$webServer = 'https://MyServer'
$port = 9090
$runbookName = "Test-Runbook"

$params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
Start-SmaRunbook –WebServiceEndpoint $webServer –Port $port –Name $runbookName –Parameters $params
```
## To specify the worker server for a runbook.
Each runbook has a property called **RunbookWorker** that is empty by default.  If this property is populated, then that Worker server will service the job. If the Worker server is not available, then the job will fail with an error. If the **RunbookWorker** property of the runbook is not populated, then SMA will randomly select an available Worker server to service the request.

You can currently only set the **RunbookWorker** property using the Set-SmaRunbookConfiguration cmdlet in PowerShell.  The following example specifies that a test runbook always run on a worker server called *srv01*. 

```powershell
$webServer = 'https://MyServer'
$port = 9090
$runbookName = "Test-Runbook"
$workerServer = "srv01"
 
Set-SmaRunbookConfiguration –WebServiceEndpoint $webServer –Port $port –Name $runbookName -RunbookWorker $workerServer
```

To reset the runbook to use any available Worker server, set the **RunbookWorker** property to **$null**.

## <a name="Parameters"></a>Runbook Parameters
Parameters are values that a runbook requires when it is started. For example, a runbook that creates a new virtual machine would presumably have a parameter for you to specify the computer name. If a parameter is mandatory, then you must provide a value for it when you start the runbook. If a parameter is not mandatory, then can provide a value but are not required to.

When you start a runbook using the Management Portal or Windows PowerShell, the instruction is sent through the Automation web service. This service does not support parameters with complex data types. If you need to provide a value for a complex parameter, then you must call it inline from another runbook as described in [Child Runbooks](Child-Runbooks-in-../Service-Management-Automation.md).

The Automation web service will provide special functionality for parameters using certain data types as described in the following sections.

### <a name="NamedValues"></a>Named Values
If the parameter is data type \[object\], then you can use the following JSON format to send it a list of named values: *{"Name1":Value1, "Name2":Value2, "Name3":Value3}*. These values must be simple types. The runbook will receive the parameter as a [PSCustomObject](http://aka.ms/runbookauthor/pscustomobject) with properties that correspond to each named value.

Consider the following test runbook that accepts a parameter called *user*.

```powershell
Workflow Test-Parameters
{
   param ( 
      [Parameter(Mandatory=$true)][object]$user
   )
    if ($user.Show) {
        foreach ($i in 1..$user.RepeatCount) {
            $user.FirstName
            $user.LastName
        }
    } 
}
```

The following text could be used for the user parameter.

```powershell
{"FirstName":"Joe","LastName":"Smith","RepeatCount":2,"Show":true}
```

This results in the following output.

```powershell
Joe
Smith
Joe
Smith

```

### <a name="Arrays"></a>Arrays
If the parameter is an array such as \[array\] or \[string\[\]\], then you can use the following JSON format to send it a list of values: *\[Value1,Value2,Value3\]*. These values must be simple types.

Consider the following test runbook that accepts a parameter called *user*.

```powershell
Workflow Test-Parameters
{
   param ( 
      [Parameter(Mandatory=$true)][array]$user
   )
    if ($user[3]) {
        foreach ($i in 1..$user[2]) {
            $ user[0]
            $ user[1]
        }
    } 
}
```

The following text could be used for the user parameter.

```powershell
["Joe","Smith",2,true]
```

This results in the following output.

```powershell
Joe
Smith
Joe
Smith

```

### <a name="Credentials"></a>Credentials
If the parameter is data type \[PSCredential\], then you can provide the name of a [!INCLUDE[sma_1](../../Token/sma_1_md.md)] credential asset. The runbook will retrieve the [credential asset](http://aka.ms/runbookauthor/assets/credentials) with the name that you specify.

Consider the following test runbook that accepts a parameter called *credential*.

```powershell
Workflow Test-Parameters
{
   param ( 
      [Parameter(Mandatory=$true)][PSCredential]$credential
   )
   $credential.UserName
}
```

The following text could be used for the user parameter assuming that there was a credential asset called *"MyCredential"*.

```powershell
MyCredential
```

Assuming the username in the credential was *jsmith*, this results in the following output.

```powershell
jsmith
```

## See Also
[Service Management Automation](../Service-Management-Automation.md)
[Runbook Operations](Runbook-Operations.md)
[Child Runbooks](Child-Runbooks-in-../Service-Management-Automation.md)


