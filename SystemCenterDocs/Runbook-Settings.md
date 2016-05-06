---
title: Runbook Settings
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 55d44d60-9ddf-45d5-b0db-b67e3941e134
---
# Runbook Settings
Each runbook in [!INCLUDE[sma_1](./Token/sma_1_md.md)] has multiple settings that help it to be identified and to change its logging behavior. Each of these settings is described below followed by procedures on how to modify them.

## Settings

### <a name="Name"></a>Name and Description
You cannot change the name of a runbook after it has been created. The **Description** is optional and can be up to 512 characters.

### <a name="Tags"></a>Tags
Tags allow you to assign distinct words and phrases to help identify a runbook. You can specify multiple tags for a runbook by separating them with commas.

### Logging
By default, Verbose and Progress records are not written to job history. You can change the settings for a particular runbook to log these records. For more information on these records, see [Runbook Output and Messages](./Runbook-Output-and-Messages.md).

## Changing Runbook Settings

### Changing Runbook Settings with the Management Portal
You can change settings for a runbook in the Management Portal from the **Configure** page for the runbook.

1.  In the Management Portal, select **Automation**.

2.  Select the **Runbooks** tab.

3.  Click the name of a runbook.

4.  Select the **Configure** tab.

### Changing Runbook Settings with Windows PowerShell
You can use the [Set\-SmaRunbookConfiguration](http://aka.ms/runbookauthor/cmdlet/setsmarunbookconfiguration) cmdlet to change all the settings for a runbook except for Tags. You can only change and add Tags for existing runbooks using the Management Portal. You can only set Tags for runbooks with PowerShell when you import a runbook using [Import\-SmaRunbook](http://aka.ms/runbookauthor/cmdlet/importsmarunbook).

The following sample commands show how to set the properties for a runbook. This sample adds a description and specifies that verbose records should be logged.

```powershell
$webServer = 'https://MyServer'
$port = 9090
$runbookName = "Sample-TestRunbook"

Set-SmaRunbookConfiguration –WebServiceEndpoint $webServer –Port $port –Name $runbookName –Description "Sample runbook" –LogVerbose $true

```

## See Also
[Service Management Automation](./Service-Management-Automation.md)
[Runbook Operations \(old\) \[SMA\]](assetId:///230817bd-e503-4beb-9ec3-8c1f028e9b48)
[How to purge the Service Management Automation database](./How-to-purge-the-Service-Management-Automation-database.md)


