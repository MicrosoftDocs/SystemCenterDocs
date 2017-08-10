---
description: Provides an overview of how you can work with integration modules.
manager:  carmonm
ms.topic:  article
author:  cfreemanwa
ms.author: raynew
ms.prod:  system-center-threshold
keywords:  
ms.date: 10/12/2016
title:  Working with Integration Modules
ms.technology:  service-management-automation
ms.assetid:  a99b8b42-665a-48eb-ab8e-5ebe8462c50a
---

# Working with integration modules

>Applies To: System Center 2016 - Service Management Automation

An [Integration Module](overview-powershell-workflows.md#GK_Modules) is a package that contains a [Windows PowerShell Module](http://go.microsoft.com/fwlink/?LinkID=325518). For information on writing a Windows PowerShell Module, see [Writing a Windows PowerShell Module](http://go.microsoft.com/fwlink/?LinkID=325523). An Integration Module can contain any of the valid Module Types specified in [Windows PowerShell Modules](http://go.microsoft.com/fwlink/?LinkID=325518). This includes Script Modules (.psm1), Binary Modules (.dll), and Manifest Modules (.psd1).
The Integration Module package is a compressed file with the same name as the module and a .zip extension. It contains a single folder also with the name of the module. The Windows PowerShell module and any supporting files, including a manifest file (.psd1) if the module has one, must be contained in this folder.

If the module should contain a [Connection](~/sma/manage-global-assets.md) type, it must also contain a file with the name <ModuleName\>-Automation.json that specifies the connection type properties. This is a json file with the following format.

```powershell
{
   "ConnectionFields": [
   {
      "IsEncrypted":  false,
      "IsOptional":  false,
      "Name":  "ComputerName",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  false,
      "IsOptional":  true,
      "Name":  "Username",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  true,
      "IsOptional":  false,
      "Name":  "Password",
   "TypeName":  "System.String"
   }],
   "ConnectionTypeName":  "DataProtectionManager",
   "IntegrationModuleName":  "DataProtectionManager"
}

```

The steps for creating and working with Automation runbooks are different depending on whether you using a management portal or Windows PowerShell. The basic steps for various common operations using both methods are provided in the following sections.

## Enumerating installed modules

### To Get a list of installed modules using the management portal

1. Select the **Automation** workspace.

2. If you are using Azure, then select an Automation account.

3. At the top of the window, click **Assets**.

4. Inspect the assets in the list with a Type of **Module**.

### To Get a list of installed modules in Service Management Automation using Windows PowerShell

The following sample commands retrieve all modules installed in Automation.

```powershell
$webServer = 'https://MyWebServer'
$port = 9090
Get-SmaModule "WebServiceEndpoint $webServer "Port $port
```

## Importing a module

A module is a compressed file with a .zip extension that contains a folder which includes one of the following file types:

- A module (psm1 file)
- A module manifest (psd1 file)

### To import a module using the management portal

1. Select the Automation workspace.

2. At the bottom of the window, click Import Module.

3. Click Browse for File.

4. Select the module file and click OK.

5. Click the checkmark button on the dialog box.


### To import a module in Service Management Automation using Windows PowerShell

The following sample commands show how to import a module.

```powershell
$webServer = 'https://MyWebServer'
$port = 9090
$modulePath = 'C:\Modules\MyModule.psm1'
Import-SmaModule "WebServiceEndpoint $webServer "Port $port "Path $modulePath
```

## Enumerating Activities in a Module

### To Get a list of activities in a module using the management portal

1. Select the Automation workspace.

2. If you are using Azure, then select an Automation account.

3. At the top of the window, click Assets.

4. Locate the module and select it.

5. Scroll to the bottom of the Module Details screen and inspect its activities.

6. Optionally, click the magnifying glass icon to filter for particular activities.

### To get a list of activities in a module in Service Management Automation using Windows PowerShell

The following sample commands show how to retrieve the activities in a particular module.

```powershell
$webServer = 'https://MyWebServer'
$port = 9090
$moduleName = 'MyModule'
$module = Get-SmaModule "WebServiceEndpoint $webServer "Port $port "Name $moduleName
$module.Activities
```

### To get a list of activities in all modules in Service Management Automation using Windows PowerShell

The following sample commands show how to retrieve the activities in all modules installed in Automation.

```powershell
$webServer = 'https://MyWebServer'
$port = 9090
$modules = Get-SmaModule "WebServiceEndpoint $webServer "Port $port
$modules | foreach {$_.Activities} | sort Name,ModuleName | ft Name,ModuleName,Description
```

## Next steps
To learn more about Service Management Automation read [Service Management Automation](service-management-automation.md).

To learn more about how to use runbooks in your environment read [Runbook Operations](manage/runbook-operations.md).
