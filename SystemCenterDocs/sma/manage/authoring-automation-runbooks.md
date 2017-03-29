---
description: Provides guidance and instructions for creating Service Management Automation runbooks
manager:  carmonm
ms.topic:  article
author:  cfreemanwa
ms.author: cfreeman
ms.prod:  system-center-threshold
keywords:  
ms.date:  03/29/2017
title:  Authoring Automation Runbooks
ms.technology:  service-management-automation
ms.assetid:  a8b7e82f-e3fc-4286-8570-8d5ded944b27
---
# Authoring Sevice Management Automation Runbooks

>Applies To: Windows Azure Pack for Windows Server, System Center 2016 - Service Management Automation

Runbooks in Service Management Automation and Microsoft Azure Automation are Windows PowerShell workflows or PowerShell scripts. They provide the ability to automate administrative processes for managing and deploying cloud servers or any other function that a Windows PowerShell script can perform.

There is no difference in the runbooks between the two systems, and the same runbook can run on either with identical functionality. When the term *Automation* is used in this guide, it refers to both Service Management Automation and Microsoft Azure Automation.

The additional services provided by Automation for working with Windows PowerShell Workflows include the following:

-   Centralized storage and management of runbooks.

-   Scalable architecture for scheduling and running runbooks.

-   Global resources that are centrally managed and available to all runbooks.

-   User interface for authoring and testing runbooks.

-   Set of cmdlets for managing and starting runbooks.

## Creating or importing a runbook

You can add a runbook to Service Management Automation by either creating it in the management portal, or by importing it from a file.

### To create a runbook in the Management Portal:

1.  In the Management Portal, click, **New**, **App Services**, **Automation**, **Runbook**, **Quick Create**.

2.  Enter the required information, and then click **Create**. The runbook name must start with a letter and can have letters, numbers, underscores, and dashes.

3.  If you want to edit the runbook now, then click **Edit Runbook**. Otherwise, click **OK**.

4.  Your new runbook will appear on the **Runbooks** tab.

### To import a runbook from a file:

.  In the Management portal, select **Automation** and then select an Automation Account.

2.  Click **Import**.

3.  Click **Browse for File** and locate the script file to import.

4.  If you want to edit the runbook now, then click **Edit Runbook**. Otherwise, click **OK**.

5.  Your new runbook will appear on the **Runbooks** tab for the Automation Account.

### To import a runbook from a script file with Windows PowerShell
You can use the [Import-SmaRunbook](http://aka.ms/runbookauthor/cmdlet/importsmarunbook) cmdlet to create a new runbook from a script file containing a workflow. To modify the draft version of an existing runbook with the contents of a script file, see [To Change the Contents of a Runbook Using Windows PowerShell](Editing-a-Runbook.md#ChangeContentsPowerShell).

The following sample commands show how to import a script file into an existing runbook and then publish it.

```powershell
$webServer = 'https://MyServer'
$port = 9090
$runbookName = "Test-Runbook"
$scriptPath = "c:\runbooks\Test-Runbook.ps1"

Import-SmaRunbook "WebServiceEndpoint $webServer "Port $port "Path $scriptPath
Publish-SMARunbook "WebServiceEndpoint $webServer "Port $port "Name $runbookName

```
## Editing a Runbook

Each runbook in Service Management Automation has two versions, Draft and Published. You edit the Draft version of the workflow and then publish it so it can be executed. The Published version cannot be edited.

### To Edit a Runbook with the Management Portal
The Management Portal includes an editor that you can use to view and edit runbooks. In addition to providing basic text editing capabilities, the editor provides the ability to automatically insert code for [Global Assets](#InsertGlobalSetting), [Activities](#InsertActivity), and [Runbooks](#InsertRunbook).

1.  In the Management Portal, select **Automation**.

2.  Select the **Runbooks** tab.

3.  Click the name of the runbook you want to edit.

4.  Select the **Author** tab.

5.  Either click **Draft** at the top of the screen or the **Edit** button at the bottom of the screen.

6.  Perform the required editing.

7.  Click **Save** when your edits are complete.

8.  Click **Publish** if you want the latest draft version of the runbook to be published.

### To Insert Code for a Runbook into a Runbook

1.  Open the runbook in the Management Portal editor.

2.  At the bottom of the screen, click **Insert** and then **Runbook**.

3.  Select the runbook to insert from the center column and click the right arrow.

4.  If the runbook has parameters, they will be listed for your information.

5.  Click the check button.

6.  Code to run the selected runbook will be inserted into the current runbook.

7.  If the runbook requires parameters, provide an appropriate value in place of the data type surrounded by braces <>.

#### <a name="InsertGlobalSetting"></a>To Insert a Global Asset into a Runbook

1.  Open the runbook in the Management Portal editor.

2.  At the bottom of the screen, click **Insert** and then **Setting**.

3.  In the **Setting Action** column, select the type of code that you require

4.  Select from the available assets in the center column.

5.  Click the check button.

#### <a name="InsertActivity"></a>To Insert an Activity into a Runbook

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

### To Edit an Automation Runbook Using Windows PowerShell
To edit a runbook with Windows PowerShell, you edit the workflow using the editor of your choice and save it to a .ps1 file. You can use the [Get-SMARunbookDefinition](http://aka.ms/runbookauthor/cmdlet/getsmarunbookdefinition) cmdlet to retrieve the contents of the runbook and then [Edit-SMARunbook](http://aka.ms/runbookauthor/cmdlet/editsmarunbook) cmdlet to replace the existing draft workflow with the modified one.

To create a new runbook from the contents of a script file, see [To import a runbook from a script file with Windows PowerShell](Creating-or-Importing-a-Runbook.md#to-import-a-runbook-from-a-script-file-with-windows-powershell).

### <a name="RetrieveContentsPowerShell"></a>To Retrieve the Contents of a Runbook Using Windows PowerShell
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

### <a name="ChangeContentsPowerShell"></a>To Change the Contents of a Runbook Using Windows PowerShell
The following sample commands show how to replace the existing contents of a runbook with the contents of a script file containing a workflow.

```powershell
$webServer = 'https://MyServer'
$port = 9090
$runbookName = "Test-Runbook"
$scriptPath = "c:\runbooks\Test-Runbook.ps1"

Edit-SmaRunbook "WebServiceEndpoint $webServer "Port $port -Name $runbookName -Path $scriptPath -Overwrite
Publish-SmaRunbook "WebServiceEndpoint $webServer "Port $port "Name $runbookName "Path $scriptPath
```

## <a name="ISE"></a>To Edit an Automation Runbook Using Windows PowerShell ISE
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

## Next steps

- Read about how to call one runbook from another runbook [Child Runbooks](../Service-Management-Automation.md).

- Read about how to build an integration module with activities that can be used by a runbook [Building an Integration Module](Building-an-Integration-Module.md).
