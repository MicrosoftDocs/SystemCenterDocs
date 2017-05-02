---
description: Provides an overview of how you can use build an integration module.
manager:  cfreeman
ms.topic:  article
author:  bwren
ms.author: bwren
ms.prod:  system-center-threshold
keywords:  
ms.date:  10/12/2016
title:  Building an Integration Module
ms.technology:  service-management-automation
ms.assetid:  4503784f-c267-4c81-a423-659adaa1df5a
---

# Building an Integration Module

>Applies To: Windows Azure Pack for Windows Server, System Center 2016 - Service Management Automation

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

|Folder|Files|
|----------|---------|
|MyModule|MyModule.psd1 or<br /><br />MyModule.psm1 or<br /><br />MyModule.dll<br /><br />MyModule-Automation.json|

## See Also
[Service Management Automation](service-management-automation.md)

[Authoring Automation Runbooks](authoring-automation-runbooks.md)

[Working with Integration Modules](manage-integration-modules.md)
