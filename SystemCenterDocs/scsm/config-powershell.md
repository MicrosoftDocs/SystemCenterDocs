---
title: Configure PowerShell to run in Service Manager
description: Before you use PowerShell with Service Manager, you need to prepare and then import Service Manager cmdlets.
manager: evansma
ms.custom: na
ms.prod: system-center
author: jyothisuri
ms.author: jsuri
ms.date: 05/06/2019
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b785d6a-2011-4fd9-987b-46e5eb164896
---

# Configure Windows PowerShell to run in Service Manager

::: moniker range=">= sc-sm-1801 <= sc-sm-1807"

[!INCLUDE [eos-notes-service-manager.md](../includes/eos-notes-service-manager.md)]

::: moniker-end

Before you can run commands in the Windows PowerShell command-line interface in System Center - Service Manager, you must set execution policy to RemoteSigned and import the data warehouse cmdlet module.

The Service Manager cmdlets are implemented in the following two modules:

- **System.Center.Service.Manager**. This module is imported automatically every time a Service Manager Windows PowerShell session is opened.

- **Microsoft.EnterpriseManagement.Warehouse.Cmdlets**. This module must be imported manually.

## Cmdlets in Authoring Tool workflows

When you use the Service Manager Authoring tool to create a workflow, then custom scripts using Windows PowerShell cmdlets called by the workflow fail. This is due to a problem in the Service Manager MonitoringHost.exe.config file.

To work around this problem, update the MonitoringHost.exe.config XML file using the following steps.

1. Navigate to %ProgramFiles%\Microsoft System Center\Service Manager or the location where you installed Service Manager.

2. Edit the MonitoringHost.exe.config file and add the section in italic type from the example below in the corresponding section of your file. You must insert the section before `<publisherPolicy apply="yes" />`.

3. Save your changes to the file.

4. Restart the System Center Management service on the Service Manager management server.

```xml
<?xml version="1.0"?>
<configuration>
    <configSections>
        <section name="uri" type="System.Configuration.UriSection, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
    </configSections>
    <uri>
        <iriParsing enabled="true" />
    </uri>
    <runtime>
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
            <dependentAssembly>
                <assemblyIdentity name="Microsoft.Mom.Modules.DataTypes" publicKeyToken="31bf3856ad364e35" />
                <publisherPolicy apply="no" />
                <bindingRedirect oldVersion="6.0.4900.0" newVersion="7.0.5000.0" />
            </dependentAssembly>
            <dependentAssembly>
                <assemblyIdentity name="Microsoft.EnterpriseManagement.HealthService.Modules.WorkflowFoundation" publicKeyToken="31bf3856ad364e35" />
                <publisherPolicy apply="no" />
                <bindingRedirect oldVersion="6.0.4900.0" newVersion="7.0.5000.0" />
            </dependentAssembly>
            <dependentAssembly>
                <assemblyIdentity name="Microsoft.EnterpriseManagement.Modules.PowerShell" publicKeyToken="31bf3856ad364e35" />
                <bindingRedirect oldVersion="6.0.4900.0" newVersion="7.0.5000.0" />
            </dependentAssembly>
            <publisherPolicy apply="yes" />
            <probing privatePath="" />
        </assemblyBinding>
        <gcConcurrent enabled="true" />
    </runtime>
</configuration>
```

## Execution policy

Use the following procedure to set execution policy to RemoteSigned in Service Manager. This is necessary to enable the importation of the Service Manager cmdlet modules, automatically or manually.

You have to run this command only once on the computer where you intend to use Windows PowerShell cmdlets for Service Manager.

### To set execution policy

1. On the computer where you want to run Windows PowerShell, click **Start**, click **All Programs**, click **Microsoft System Center \<version\>**, click **Service Manager**, and then click **Service Manager Shell**.
2. At the Windows PowerShell prompt, type the following command, and then press ENTER:

    ```powershell
    Set-ExecutionPolicy –Force RemoteSigned
    ```
3. Type *exit*, and then press ENTER to close the **Administrator: Windows PowerShell** window.

## Import the data warehouse cmdlet module

To be able to use the data warehouse cmdlets in Service Manager, you must first manually import the Windows PowerShell data warehouse cmdlets module for Service Manager. You can import the data warehouse cmdlets module on the Service Manager management server, the data warehouse management server, or both.

### To import the data warehouse cmdlets module

1. On a management server, open a Service Manager Windows PowerShell session. Or, on a data warehouse management server open a Windows PowerShell session.
    Ensure that the Windows PowerShell prompt is at the Service Manager installation folder.
2. At the Windows PowerShell command prompt, type the following command, and then press ENTER:

    ```powershell
    Import-Module ".Microsoft.EnterpriseManagement.Warehouse.Cmdlets.psd1"
    ```

3. Type *exit*, and then press ENTER to close the **Administrator: Windows PowerShell** window.

## Next steps

- Review [Register with the data warehouse to enable reporting](register-dw.md) to run the Data Warehouse Registration Wizard to register the Service Manager management group with the Service Manager data warehouse management server. Registering with the data warehouse makes it possible for you to run reports.
