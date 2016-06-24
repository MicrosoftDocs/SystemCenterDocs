---
title: Publishing a Runbook
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2224465-5050-456e-99ec-d47772d33352
---
# Publishing a Runbook
Each runbook in Service Management Automation has a Draft and a Published version. Only the Published version is available to be run, and only the Draft version can be edited. The Published version is unaffected by any changes to the Draft version. When the Draft version should be made available, then you publish it which overwrites the Published version with the Draft version.

## To Publish a Runbook Using the management portal

1.  Select the **Automation** workspace.

2.  At the top of the screen, select **Runbooks**.

3.  Locate the runbook to edit and click on its name.

4.  At the top of the screen, click **Author**.

5.  Click **Draft**.

6.  At the bottom of the screen, click **Publish**.

7.  Click **Yes** to the verification message.

## To Publish a Runbook Using Windows PowerShell
You can use the Publish-SmaRunbook to publish a runbook with Windows PowerShell. The following sample commands show how to publish a runbook.

```powershell
$webServer = 'https://MyServer'
$port = 9090
$runbookPath = 'c:\runbooks\Sample-TestRunbook.ps1'
$runbookName = 'Test-Runbook'

Publish-SmaRunbook –WebServiceEndpoint $webServer –Port $port –Name $runbookName
```

## To Publish a Runbook Using Windows PowerShell ISE
Windows PowerShell Integrated Scripting Environment (ISE) is an application that allows you to run commands and write, test, and debug scripts.  The [SMA PowerShell ISE Add-on](https://www.powershellgallery.com/packages/AzureAutomationAuthoringToolkit/0.2.3.3) allows you to use this tool to write and test Automation runbooks.

1. Open Windows PowerShell ISE.

2. If the **SMA ISE add-on** is not displayed on the right side of the ISE, open the  **Add-ons** menu, and enable **SMA ISE add-on**.

3. Sign in to SMA on the **Configuration** tab.

4. Select the **Runbook** tab.  You should see a list of SMA runbooks.

5. Select the runbook and click **Publish Draft** to publish the latest draft version of the runbook.

## See Also
[Service Management Automation](../Service-Management-Automation.md)
[Authoring Automation Runbooks](Authoring-Automation-Runbooks.md)
[Creating or Importing a Runbook](Creating-or-Importing-a-Runbook.md)
[Editing a Runbook](Editing-a-Runbook.md)


