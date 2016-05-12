---
title: Creating or Importing a Runbook
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d14db796-a3e5-4b1d-a098-e734ceae2e0e
---
# Creating or Importing a Runbook
You can add a runbook to [!INCLUDE[sma_1](Token/sma_1_md.md)] by either [creating one in the Management Portal](Creating-or-Importing-a-Runbook.md#CreateRunbook) or [importing an existing runbook from a file](Creating-or-Importing-a-Runbook.md#ImportRunbook). This topic provides procedures for each of these methods.

## <a name="CreateRunbook"></a>Creating a new Automation Runbook
You can create a new runbook in [!INCLUDE[sma_1](Token/sma_1_md.md)] using the Management Portal, Windows PowerShell ISE add-on, or Windows PowerShell. Once the runbook has been created, you can edit it using information in the [Runbook Authoring Guide](http://aka.ms/runbookauthor).

### <a name="CreatePortal"></a>To create a new Automation runbook with the Management Portal

1.  In the Management Portal, click, **New**, **App Services**, **Automation**, **Runbook**, **Quick Create**.

2.  Enter the required information, and then click **Create**. The runbook name must start with a letter and can have letters, numbers, underscores, and dashes.

3.  If you want to edit the runbook now, then click **Edit Runbook**. Otherwise, click **OK**.

4.  Your new runbook will appear on the **Runbooks** tab.

### <a name="ISE"></a>To create a new Automation runbook with Windows PowerShell ISE
Windows PowerShell Integrated Scripting Environment (ISE) is an application that allows you to run commands and write, test, and debug scripts.  The [SMA PowerShell ISE Add-on](https://www.powershellgallery.com/packages/AzureAutomationAuthoringToolkit/0.2.3.3) allows you to use this tool to write and test Automation runbooks.

1. Open Windows PowerShell ISE.

2. If the **SMA ISE add-on** is not displayed on the right side of the ISE, open the  **Add-ons** menu, and enable **SMA ISE add-on**.

3. Sign in to SMA on the **Configuration** tab.

4. Select the **Runbook** tab.  

5. Click **Create New**.

6. Provide a name for the runbook and then select whether it should be a **Script** or **Workflow** runbook.

7. [Edit](Editing-a-Runbook.md#ISE) and [publish](Publishing-a-Runbook.md) the runbook.

### <a name="CreatePowerShell"></a>To create a new Automation runbook with Windows PowerShell
You can create a new runbook with Windows PowerShell by importing a script file. This is described below in [To import a runbook from a script file with Windows PowerShell](Creating-or-Importing-a-Runbook.md#ImportPowerShell).

## <a name="ImportRunbook"></a>Importing a Runbook into Service Management Automation
You can import a script file into [!INCLUDE[sma_1](Token/sma_1_md.md)] using either the Management Portal or Windows PowerShell. The file must contain a single workflow, and the name of the workflow must match the name of the script file. This name will be used for the new runbook.

### <a name="ImportPortal"></a>To import a runbook from a script file with the Management portal
You can use the following procedure to import a script file into [!INCLUDE[sma_1](Token/sma_1_md.md)].

1.  In the Management portal, select **Automation** and then select an Automation Account.

2.  Click **Import**.

3.  Click **Browse for File** and locate the script file to import.

4.  If you want to edit the runbook now, then click **Edit Runbook**. Otherwise, click **OK**.

5.  Your new runbook will appear on the **Runbooks** tab for the Automation Account.

### <a name="ImportPowerShell"></a>To import a runbook from a script file with Windows PowerShell
You can use the [Import\-SmaRunbook](http://aka.ms/runbookauthor/cmdlet/importsmarunbook) cmdlet to create a new runbook from a script file containing a workflow. To modify the draft version of an existing runbook with the contents of a script file, see [To Change the Contents of a Runbook Using Windows PowerShell](Editing-a-Runbook.md#ChangeContentsPowerShell).

The following sample commands show how to import a script file into an existing runbook and then publish it.

```powershell
$webServer = 'https://MyServer'
$port = 9090
$runbookName = "Test-Runbook"
$scriptPath = "c:\runbooks\Test-Runbook.ps1"

Import-SmaRunbook –WebServiceEndpoint $webServer –Port $port –Path $scriptPath 
Publish-SMARunbook –WebServiceEndpoint $webServer –Port $port –Name $runbookName

```

## See Also
[Service Management Automation](Service-Management-Automation.md)
[Runbook Authoring](Authoring-Automation-Runbooks.md)
[Editing a Runbook](Editing-a-Runbook.md)


