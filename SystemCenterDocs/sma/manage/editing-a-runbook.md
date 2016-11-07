---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bwren
ms.author: bwren
ms.prod:  system-center-threshold
keywords:  
ms.date:  10/12/2016
title:  Editing a Runbook
ms.technology:  service-management-automation
ms.assetid:  a6daafc4-bc8d-4cd5-bd14-5f5b55da90a2
---

# Editing a Runbook

>Applies To: Windows Azure Pack for Windows Server, System Center 2016 - Service Management Automation

Each runbook in Service Management Automation has two versions, Draft and Published. You edit the Draft version of the workflow and then publish it so it can be executed. The Published version cannot be edited.

## <a name="Portal"></a>To Edit a Runbook with the Management Portal
The Management Portal includes an editor that you can use to view and edit runbooks. In addition to providing basic text editing capabilities, the editor provides the ability to automatically insert code for [Global Assets](#InsertGlobalSetting), [Activities](#InsertActivity), and [Runbooks](#InsertRunbook).

1.  In the Management Portal, select **Automation**.

2.  Select the **Runbooks** tab.

3.  Click the name of the runbook you want to edit.

4.  Select the **Author** tab.

5.  Either click **Draft** at the top of the screen or the **Edit** button at the bottom of the screen.

6.  Perform the required editing.

7.  Click **Save** when your edits are complete.

8.  Click **Publish** if you want the latest draft version of the runbook to be published.

### <a name="InsertingCode"></a>Inserting Code into a Runbook
The Automation editor includes a feature to insert code for Activities, Settings and Runbooks into a runbook. Rather than typing in the code yourself, you can select from a list of available assets and have the appropriate code inserted into the runbook.

#### <a name="InsertRunbook"></a>To Insert Code for a Runbook into a Runbook

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

## <a name="PowerShell"></a>To Edit an Automation Runbook Using Windows PowerShell
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

## See Also
[Creating or Importing a Runbook](Creating-or-Importing-a-Runbook.md)

[Service Management Automation](../Service-Management-Automation.md)

[Authoring Automation Runbooks](Authoring-Automation-Runbooks.md)
