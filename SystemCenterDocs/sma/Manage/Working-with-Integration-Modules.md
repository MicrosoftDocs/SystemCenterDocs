---
description:  
manager:  cfreemanwa
ms.topic:  article
author:  bwren
ms.prod:  system-center-threshold
keywords:  
ms.date:  2016-06-28
title:  Working with Integration Modules
ms.technology:  service-management-automation
ms.assetid:  a99b8b42-665a-48eb-ab8e-5ebe8462c50a
---

# Working with Integration Modules

>Applies To: 

The steps for creating and working with Automation runbooks are different depending on whether you using a management portal or Windows PowerShell. The basic steps for various common operations using both methods are provided in the following sections.

## Enumerating Installed Modules

### To Get a List of Installed Modules using the management portal

1. Select the **Automation** workspace.

2. If you are using Azure, then select an Automation account.

3. At the top of the window, click **Assets**.

4. Inspect the assets in the list with a Type of **Module**.

### To Get a List of Installed Modules in Service Management Automation using Windows PowerShell

The following sample commands retrieve all modules installed in Automation. 

```powershell
$webServer = 'https://MyWebServer'
$port = 9090
Get-SmaModule "WebServiceEndpoint $webServer "Port $port
```

## Importing a Module

A module is a compressed file with a .zip extension that contains a folder which includes one of the following file types:

- A module (psm1 file)
- A module manifest (psd1 file)

### To Import a Module using management portal

1. Select the Automation workspace.

2. At the bottom of the window, click Import Module.

3. Click Browse for File.

4. Select the module file and click OK.

5. Click the checkmark button on the dialog box.


### To Import a Module in Service Management Automation using Windows PowerShell

The following sample commands show how to import a module.

```powershell
$webServer = 'https://MyWebServer'
$port = 9090
$modulePath = 'C:\Modules\MyModule.psm1'
Import-SmaModule "WebServiceEndpoint $webServer "Port $port "Path $modulePath
```

## Enumerating Activities in a Module

### To Get a List of Activities in a Module using management portal

1. Select the Automation workspace.

2. If you are using Azure, then select an Automation account.

3. At the top of the window, click Assets.

4. Locate the module and select it.

5. Scroll to the bottom of the Module Details screen and inspect its activities.

6. Optionally, click the magnifying glass icon to filter for particular activities.

### To Get a List of Activities in a Module in Service Management Automation using Windows PowerShell

The following sample commands show how to retrieve the activities in a particular module.

```powershell
$webServer = 'https://MyWebServer'
$port = 9090
$moduleName = 'MyModule'
$module = Get-SmaModule "WebServiceEndpoint $webServer "Port $port "Name $moduleName
$module.Activities
```

### To Get a List of Activities in All Modules in Service Management Automation using Windows PowerShell

The following sample commands show how to retrieve the activities in all modules installed in Automation. 

```powershell
$webServer = 'https://MyWebServer'
$port = 9090
$modules = Get-SmaModule "WebServiceEndpoint $webServer "Port $port
$modules | foreach {$_.Activities} | sort Name,ModuleName | ft Name,ModuleName,Description
```

## See Also
[Service Management Automation](../Service-Management-Automation.md)
[Runbook Operations](Runbook-Operations.md)
[Building an Integration Module](Building-an-Integration-Module.md)


