---
description: Provides an overview of how you can work with integration modules.
manager: carmonm
ms.topic: article
author: rayne-wiselman
ms.author: raynew
ms.prod: system-center
ms.date: 05/08/2018
title: Work with Integration Modules
ms.technology: service-management-automation
---

# Work with integration modules

An [Integration Module](overview-powershell-workflows.md#integration-modules) is a package that contains a [Windows PowerShell Module](https://go.microsoft.com/fwlink/?LinkID=325518). For information on writing a Windows PowerShell Module, see [Writing a Windows PowerShell Module](https://go.microsoft.com/fwlink/?LinkID=325523). An Integration Module can contain any of the valid Module Types specified in [Windows PowerShell Modules](https://go.microsoft.com/fwlink/?LinkID=325518). This includes Script Modules (.psm1), Binary Modules (.dll), and Manifest Modules (.psd1).
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

## Enumerate installed modules

### Get a list of installed modules in the management portal

1. Select the **Automation** workspace.

2. If you are using Azure, then select an Automation account.

3. At the top of the window, click **Assets**.

4. Inspect the assets in the list with a Type of **Module**.

### Get a list of installed modules using Windows PowerShell

The following sample commands retrieve all modules installed in Automation.

```powershell
$webServer = 'https://MyWebServer'
$port = 9090
Get-SmaModule "WebServiceEndpoint $webServer "Port $port
```

## Import a module

A module is a compressed file with a .zip extension that contains a folder which includes one of the following file types:

- A module (psm1 file)
- A module manifest (psd1 file)

### Import a module using the management portal

1. Select the Automation workspace.

2. At the bottom of the window, click Import Module.

3. Click Browse for File.

4. Select the module file and click OK.

5. Click the checkmark button on the dialog box.


### Import a module using Windows PowerShell

The following sample commands show how to import a module.

```powershell
$webServer = 'https://MyWebServer'
$port = 9090
$modulePath = 'C:\Modules\MyModule.psm1'
Import-SmaModule "WebServiceEndpoint $webServer "Port $port "Path $modulePath
```

## Enumerate activities in amModule

### Get a list of activities in a module in the management portal

1. Select the Automation workspace.

2. If you are using Azure, then select an Automation account.

3. At the top of the window, click Assets.

4. Locate the module and select it.

5. Scroll to the bottom of the Module Details screen and inspect its activities.

6. Optionally, click the magnifying glass icon to filter for particular activities.

### Get a list of activities in a module using Windows PowerShell

The following sample commands show how to retrieve the activities in a particular module.

```powershell
$webServer = 'https://MyWebServer'
$port = 9090
$moduleName = 'MyModule'
$module = Get-SmaModule "WebServiceEndpoint $webServer "Port $port "Name $moduleName
$module.Activities
```

### Get a list of activities in all modules using Windows PowerShell

The following sample commands show how to retrieve the activities in all modules installed in Automation.

```powershell
$webServer = 'https://MyWebServer'
$port = 9090
$modules = Get-SmaModule "WebServiceEndpoint $webServer "Port $port
$modules | foreach {$_.Activities} | sort Name,ModuleName | ft Name,ModuleName,Description
```

## Next steps
- Learn more about [Service Management automation](service-management-automation.md).
- Learn more about [runbook operations](manage/runbook-operations.md).
