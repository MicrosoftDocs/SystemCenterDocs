---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bwren
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  Testing a Runbook
ms.technology:  service-management-automation
ms.assetid:  c75fe03c-3709-4c85-b593-fb1a2920f80e
---

# Testing a Runbook

>Applies To: Windows Azure Pack for Windows Server

You can test the Draft version of a runbook in Service Management Automation while leaving the published version of the runbook unchanged. This allows you to verify that the runbook is working correctly before replacing the published version.

When you test a runbook, the Draft runbook is executed and any actions that it performs are completed. No job history is created, but the [Output](Runbook-Output-and-Messages.md#Output) and [Warning and Error](Runbook-Output-and-Messages.md#WarningError) streams are displayed in the Test Output Pane. Messages to the [Verbose Stream](Runbook-Output-and-Messages.md#Verbose) are displayed in the Output Pane only if the [$VerbosePreference variable](Runbook-Output-and-Messages.md#PreferenceVariables) is set to **Continue**.

When a runbook is tested, it still executes the workflow normally and performs any actions against resources in the environment. For this reason, you should only test runbooks against non-production resources.

## To Test a Runbook in Service Management Automation
To test a runbook, [open the Draft version of the runbook in the Management Portal](Editing-a-Runbook.md#Portal). Click the **Test** button at the bottom of the screen to start the test.

You can stop or suspend the runbook while it is being tested with the buttons underneath the Output Pane. When you suspend the runbook, it completes the current activity before being suspended. Once the runbook is suspended, you can stop it or restart it.

## To Test a Runbook Using Windows PowerShell ISE
The [PowerShell ISE add-on](https://www.powershellgallery.com/packages/SMAAuthoringToolkit) provides cmdlets that emulate the standard activities such as Get-SMACredential and Set-SMAVariable, so you can test the runbook on the local computer just as you would any other script.   

Global assets and their values are downloaded from the automation group to use for local testing.  You can inspect or change these values on the **Assets** tab.  Encrypted values are displayed in orange, and their values are not downloaded.  If you want to use these assets in local testing, then you must set their value locally.

To test the runbook in SMA, click **Test Draft in SMA**.  A new window will be opened.  Click **Start New Job** to start the test.  The output will be displayed in the window.  


## See Also
[Service Management Automation](../Service-Management-Automation.md)
[Authoring Automation Runbooks](Authoring-Automation-Runbooks.md)
[Editing a Runbook](Editing-a-Runbook.md)
