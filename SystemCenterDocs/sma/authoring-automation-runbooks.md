---
description: Provides guidance and instructions for creating Service Management Automation runbooks
manager: carmonm
ms.topic: reference
author: rayne-wiselman
ms.author: raynew
ms.prod: system-center
keywords:
ms.date: 01/22/2018
title: Author Automation Runbooks
ms.technology: service-management-automation
---
# Author Service Management Automation runbooks

::: moniker range=">= sc-sma-1801 <= sc-sma-1807"

[!INCLUDE [eos-notes-service-management-automation.md](../includes/eos-notes-service-management-automation.md)]

::: moniker-end

Runbooks in Service Management Automation and Microsoft Azure Automation are Windows PowerShell workflows or PowerShell scripts. They provide the ability to automate administrative processes for managing and deploying cloud servers or any other function that a Windows PowerShell script can perform.

There is no difference in the runbooks between the two systems, and the same runbook can run on either with identical functionality. When the term *Automation* is used in this guide, it refers to both Service Management Automation and Microsoft Azure Automation.

The additional services provided by Automation for working with Windows PowerShell Workflows include the following:

-   Centralized storage and management of runbooks.

-   Scalable architecture for scheduling and running runbooks.

-   Global resources that are centrally managed and available to all runbooks.

-   User interface for authoring and testing runbooks.

-   Set of cmdlets for managing and starting runbooks.

## Create or import a runbook

You can add a runbook to Service Management Automation by either creating it in the management portal, or by importing it from a file.

### Create a runbook in the Management Portal

1.  In the Management Portal, click, **New**, **App Services**, **Automation**, **Runbook**, **Quick Create**.

2.  Enter the required information, and then click **Create**. The runbook name must start with a letter and can have letters, numbers, underscores, and dashes.

3.  If you want to edit the runbook now, then click **Edit Runbook**. Otherwise, click **OK**.

4.  Your new runbook will appear on the **Runbooks** tab.

### Import a runbook from a file

1.  In the Management portal, select **Automation** and then select an Automation Account.

2.  Click **Import**.

3.  Click **Browse for File** and locate the script file to import.

4.  If you want to edit the runbook now, then click **Edit Runbook**. Otherwise, click **OK**.

5.  Your new runbook will appear on the **Runbooks** tab for the Automation Account.

## Import a runbook from a script file with Windows PowerShell
You can use the [Import-SmaRunbook](https://aka.ms/runbookauthor/cmdlet/importsmarunbook) cmdlet to create a new runbook from a script file containing a workflow.

The following sample commands show how to import a script file into an existing runbook and then publish it.

```powershell
$webServer = 'https://MyServer'
$port = 9090
$runbookName = "Test-Runbook"
$scriptPath = "c:\runbooks\Test-Runbook.ps1"

Import-SmaRunbook "WebServiceEndpoint $webServer "Port $port "Path $scriptPath
Publish-SMARunbook "WebServiceEndpoint $webServer "Port $port "Name $runbookName

```
## Edit a runbook

Each runbook in Service Management Automation has two versions, Draft and Published. You edit the Draft version of the workflow and then publish it so it can be executed. The Published version cannot be edited.

### Edit a runbook with the Management Portal
The Management Portal includes an editor that you can use to view and edit runbooks. In addition to providing basic text editing capabilities, the editor provides the ability to automatically insert code for [Global Assets](#insert-a-global-asset-into-a-runbook), [Activities](#insert-an-activity-into-a-runbook), and [Runbooks](#insert-code-into-a-runbook).

1.  In the Management Portal, select **Automation**.

2.  Select the **Runbooks** tab.

3.  Click the name of the runbook you want to edit.

4.  Select the **Author** tab.

5.  Either click **Draft** at the top of the screen or the **Edit** button at the bottom of the screen.

6.  Perform the required editing.

7.  Click **Save** when your edits are complete.

8.  Click **Publish** if you want the latest draft version of the runbook to be published.

### Insert code into a Runbook

1.  Open the runbook in the Management Portal editor.

2.  At the bottom of the screen, click **Insert** and then **Runbook**.

3.  Select the runbook to insert from the center column and click the right arrow.

4.  If the runbook has parameters, they will be listed for your information.

5.  Click the check button.

6.  Code to run the selected runbook will be inserted into the current runbook.

7.  If the runbook requires parameters, provide an appropriate value in place of the data type surrounded by braces <>.

#### Insert a global asset into a runbook

1.  Open the runbook in the Management Portal editor.

2.  At the bottom of the screen, click **Insert** and then **Setting**.

3.  In the **Setting Action** column, select the type of code that you require

4.  Select from the available assets in the center column.

5.  Click the check button.

#### Insert an activity into a runbook

1.  Open the runbook in the Management Portal editor.

2.  At the bottom of the screen, click **Insert** and then **Activity**.

3.  In the **Integration Module** column, select the module that contains the activity.

4.  In the **Activity** pane, select an activity.

5.  In the **Description** column, note the description of the activity. Optionally, you can click **View detailed help** to launch help for the activity in the browser.

6.  Click the right arrow.

7.  If the activity has parameters, they will be listed for your information.

8.  Click the check button.

9. Code to run the activity will be inserted into the runbook.

10. If the activity requires parameters, provide an appropriate value in place of the data type surrounded by braces <>.

### Edit an Automation runbook with
PowerShell

To edit a runbook with Windows PowerShell, you edit the workflow using the editor of your choice and save it to a .ps1 file. You can use the [Get-SMARunbookDefinition](https://aka.ms/runbookauthor/cmdlet/getsmarunbookdefinition) cmdlet to retrieve the contents of the runbook and then [Edit-SMARunbook](https://aka.ms/runbookauthor/cmdlet/editsmarunbook) cmdlet to replace the existing draft workflow with the modified one.

### <a name="RetrieveContentsPowerShell"></a>To retrieve the contents of a runbook using Windows PowerShell
The following sample commands show how to retrieve the script for a runbook and save it to a script file. In this example, the Draft version is retrieved. It is also possible to retrieve the Published version of the runbook although this version cannot be changed.

```powershell
$webServer = 'https://MyServer'
$port = 9090
$runbookName = "Test-Runbook"
$scriptPath = "c:\runbooks\Test-Runbook.ps1"

$runbookDefinition = Get-SMARunbookDefinition "WebServiceEndpoint $webServer "Port $port -Name $runbookName -Type Draft
$runbookContent = $runbookDefinition.Content

Out-File -InputObject $runbookContent -FilePath $scriptPath
```

### <a name="ChangeContentsPowerShell"></a>To Change the contents of a runbook using Windows PowerShell
The following sample commands show how to replace the existing contents of a runbook with the contents of a script file containing a workflow.

```powershell
$webServer = 'https://MyServer'
$port = 9090
$runbookName = "Test-Runbook"
$scriptPath = "c:\runbooks\Test-Runbook.ps1"

Edit-SmaRunbook "WebServiceEndpoint $webServer "Port $port -Name $runbookName -Path $scriptPath -Overwrite
Publish-SmaRunbook "WebServiceEndpoint $webServer "Port $port "Name $runbookName "Path $scriptPath
```

## Edit an Automation runbook with PowerShell ISE
Windows PowerShell Integrated Scripting Environment (ISE) is an application that allows you to run commands and write, test, and debug scripts.  The [SMA PowerShell ISE Add-on](https://www.powershellgallery.com/packages/SMAAuthoringToolkit) allows you to use this tool to write and test Automation runbooks.

1. Open Windows PowerShell ISE.

2. If the **SMA ISE add-on** is not displayed on the right side of the ISE, open the  **Add-ons** menu, and enable **SMA ISE add-on**.

3. Sign in to SMA on the **Configuration** tab.

4. Select the **Runbook** tab.  You should see a list of SMA runbooks.

5. Select the runbook you want to edit and click **Download**.  This downloads a local copy of the runbook from SMA.

6. Click **Open**.  This creates a new tab with the runbook.

7. Make the necessary changes to the runbook.

8. Click **Upload Draft** to send the runbook to SMA.  This will overwrite the existing draft version of the runbook.

9.  Click **Publish Draft** if you want to publish the latest draft version of the runbook.

## Publish your runbook

After you have created your runbook you need to publish it to so the runbook worker can execute it. Each runbook in Service Management Automation has a Draft and a Published version. Only the Published version is available to be run, and only the Draft version can be edited. The Published version is unaffected by any changes to the Draft version. When you are ready to make the Draft version available, you publish it which overwrites the Published version with the Draft version.

### Publish a runbook using the management portal

1.  Select the **Automation** workspace.

2.  At the top of the screen, select **Runbooks**.

3.  Locate the runbook to edit and click on its name.

4.  At the top of the screen, click **Author**.

5.  Click **Draft**.

6.  At the bottom of the screen, click **Publish**.

7.  Click **Yes** to the verification message.

### Publish a runbook using PowerShell
You can use the Publish-SmaRunbook to publish a runbook with Windows PowerShell. The following sample commands show how to publish a runbook.

```powershell
$webServer = 'https://MyServer'
$port = 9090
$runbookPath = 'c:\runbooks\Sample-TestRunbook.ps1'
$runbookName = 'Test-Runbook'

Publish-SmaRunbook "WebServiceEndpoint $webServer "Port $port "Name $runbookName
```

### Publish a runbook using PowerShell ISE
Windows PowerShell Integrated Scripting Environment (ISE) is an application that allows you to run commands and write, test, and debug scripts.  The [SMA PowerShell ISE Add-on](https://www.powershellgallery.com/packages/SMAAuthoringToolkit) allows you to use this tool to write and test Automation runbooks.

1. Open Windows PowerShell ISE.

2. If the **SMA ISE add-on** is not displayed on the right side of the ISE, open the  **Add-ons** menu, and enable **SMA ISE add-on**.

3. Sign in to SMA on the **Configuration** tab.

4. Select the **Runbook** tab.  You should see a list of SMA runbooks.

5. Select the runbook and click **Publish Draft** to publish the latest draft version of the runbook.

## Test your runbook

You can test the Draft version of a runbook in Service Management Automation while leaving the published version of the runbook unchanged. This allows you to verify that the runbook is working correctly before replacing the published version.

When you test a runbook, the Draft runbook is executed and any actions that it performs are completed. No job history is created, but the [Output](overview-runbook-messages-output.md#output-stream) and [Warning and Error](overview-runbook-messages-output.md#warning-and-error-streams) streams are displayed in the Test Output Pane. Messages to the [Verbose Stream](overview-runbook-messages-output.md#verbose-stream) are displayed in the Output Pane only if the [$VerbosePreference variable](overview-runbook-messages-output.md#preference-variables) is set to **Continue**.

When you test a runbook, it still executes the workflow normally and performs any actions against resources in the environment. For this reason, you should only test runbooks against non-production resources.

### Test a runbook in Service Management Automation
To test a runbook, [open the Draft version of the runbook in the Management Portal](authoring-automation-runbooks.md). Click the **Test** button at the bottom of the screen to start the test.

You can stop or suspend the runbook while it is being tested with the buttons underneath the Output Pane. When you suspend the runbook, it completes the current activity before being suspended. Once the runbook is suspended, you can stop it or restart it.

### Test a runbook using PowerShell ISE
The [PowerShell ISE add-on](https://www.powershellgallery.com/packages/SMAAuthoringToolkit) provides cmdlets that emulate the standard activities such as Get-SMACredential and Set-SMAVariable, so you can test the runbook on the local computer just as you would any other script.   

Global assets and their values are downloaded from the automation group to use for local testing.  You can inspect or change these values on the **Assets** tab.  Encrypted values are displayed in orange, and their values are not downloaded.  If you want to use these assets in local testing, then you must set their value locally.

To test the runbook in SMA, click **Test Draft in SMA**.  A new window will be opened.  Click **Start New Job** to start the test.  The output will be displayed in the window.

## Automation runbook samples

The following runbooks ship with Service Management Automation as sample runbooks to illustrate techniques and best practices. They are available to be used in the Automation extension in Windows Azure Pack for Windows Server.

|Runbook name|Description|
|----------------|---------------|
|Sample-Deleting-VMCloud-Subscription|Demonstrates a useful scenario for triggering a runbook when a user deletes a VM Clouds subscription.|
|Sample-Managing-Azure|Shows how to connect to a Windows Azure subscription and perform basic operations using the Windows Azure PowerShell module.|
|Sample-Managing-ConfigurationManager|Demonstrates the capability of Service Management Automation to connect into Configuration Manager.|
|Sample-Managing-DataProtectionManager|Demonstrates how to connect to a Data Protection Manager (DPM) server and view information about the disks found on the DPM server.|
|Sample-Managing-MySQLServers|Demonstrates how to retrieve a security token which will be used to then retrieve a list of host servers.|
|Sample-Managing-OperationsManager|Demonstrates the capability of Service Management Automation to connect to System Center Operations Manager.|
|Sample-Managing-Orchestrator|Shows how to connect to System Center Orchestrator and start an Orchestrator runbook to leverage your existing infrastructure.|
|Sample-Managing-Plans|Demonstrates how to create a new plan and add the SQL Server service with a defined quota to the new plan.|
|Sample-Managing-ServiceBusClouds|Demonstrates how to connect to a Service Bus Cloud server and view information about the created namespaces.|
|Sample-Managing-SQLServers|Demonstrates how create a new server group and add a SQL hosting server.|
|Sample-Managing-UserAccounts|Demonstrates how to create a User in Windows Azure Pack for Windows Server, which will be created in Windows Azure Pack, and appear in the management portal for administrators Users extension. However, this user should also be integrated into the authentication provider (for example, AuthSite) for accessing the management portal for tenants, which is not included in this sample.|
|Sample-Managing-VirtualMachineManager|Demonstrates how to connect to a Virtual Machine Manager (VMM) server and view information about the VMM server license.|
|Sample-Managing-VMClouds|Demonstrates how to access information about a Service Provider Foundation server's database connection and information about the VMM server objects managed by Service Provider Foundation.|
|Sample-Managing-WebSiteCloud|Demonstrates how to connect to a Web Site Clouds controller server and view information about the Web Site Clouds deployed servers.|
|Sample-Modify-VMCloud-Subscription|Demonstrates a useful scenario for triggering a runbook when tenant or administrator suspends or activates a VM Clouds subscription.|
|Sample-Using-Activities|Demonstrates the capability of Service Management Automation to use activities|
|Sample-Using-Checkpoints|Demonstrates the capability to use checkpoints in Service Management Automation.|
|Sample-Using-Connections|Demonstrates the capability of Service Management Automation to use connections to connect into remote systems.|
|Sample-Using-Credentials|Demonstrates the capability of Service Management Automation to use credentials, and outputs the user who the Service Management Automation runbook is running as. Then, it connects to the server 'ServerName' and outputs the user specified by 'SampleCredential' who is accessing the server.|
|Sample-Using-Modules|Demonstrates importing modules in runbooks, and outputs the number of already imported modules on the server 'ServerName'. Then, it imports the module specified by 'ModulePath' and outputs the new module count and information corresponding to the newly imported module.|
|Sample-Using-RunbookParameters|Demonstrates how to use input parameters for runbooks and also specify whether parameters are required, provide default parameter values, and use parameter values later in the workflow.|
|Sample-Using-Runbooks|Demonstrates how to call a runbook from within another runbook.|
|Sample-Using-SuspendWorkflow|Demonstrates how to force a runbook to suspend. This could be useful if a manual step is required before a runbook should continue, such as receiving sign-off approval from a specific person. Once the manual step is completed, the suspended runbook would be resumed manually to continue the runbook.|
|Sample-Using-Variables|Demonstrates the capability of Service Management Automation to use variables.|
|Sample-Using-VMCloud-Automation|Demonstrates a useful scenario for triggering a runbook at the start of a Service Provider Foundation event.|

## Next steps

- [Read about](service-management-automation.md) how to call one runbook from another runbook.
- [Read about](manage-integration-modules.md)
