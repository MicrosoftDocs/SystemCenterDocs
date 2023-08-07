---
ms.assetid: f08056ae-d899-464c-9746-052833dfe2dd
title: Turn off telemetry settings in Service Management Automation (SMA)
description: This article provides information about how to turn off the telemetry settings in System Center Service Management Automation
author: jyothisuri
ms.author: jsuri
manager: mkluck
ms.date: 08/07/2023
ms.topic: article
ms.prod: system-center
ms.technology: service-management-automation
ms.custom: UpdateFrequency2, engagement-fy23
---

# Turn off telemetry settings in Service Management Automation

::: moniker range=">= sc-sma-1801 <= sc-sma-1807"

[!INCLUDE [eos-notes-service-management-automation.md](../includes/eos-notes-service-management-automation.md)]

::: moniker-end


This article provides information about how to turn off the telemetry settings in System Center - Service Management Automation (SMA).

By default, SMA sends diagnostic and connectivity data to Microsoft. Microsoft uses this data to provide and improve the quality, security, and integrity of Microsoft products and services.

Administrators can turn off this feature at any point of time.


> [!NOTE]
> Microsoft doesn't collect any personal data from the customers. We only listen to events that would help diagnostics in SMA. [Learn more](#telemetry-data-collected).


## Turn off telemetry in SMA

Use the following procedure:
1. [Import the PowerShell SMA module](/powershell/module/microsoft.systemcenter.servicemanagementautomation/import-smamodule).
2. Run the following PowerShell cmdlet to disable sharing of usage and connectivity data in SMA.

   ```powershell

   Set-SmaAdminConfiguration -WebServiceEndpoint <String> -Telemetry
   $false
   ```

   >[!NOTE]
   > You can use the [Get-SmaAdminConfiguration](/powershell/module/Microsoft.SystemCenter.ServiceManagementAutomation/Get-SmaAdminConfiguration) command to check the current admin configuration settings.

## Telemetry data collected

| **Data related To** | **Data collected**|
| --- | --- |
| **Installation and other configuration information** | SMA version <br /><br /> ID used for correlation with other System Center products <br /><br />ID used to identify specific SMA installation<br /><br />If telemetry is opted out<br /><br /> If new database is created <br /><br />Processor and memory details of the system <br /><br />PowerShell version installed on the system<br /><br />Version information of IIS <br /><br />SQL version and whether Always On, Clustered, and Remote are being used|
| **Usage** | Runbooks and their state - such as  published, edit, new, debug enabled, verbose enabled, progress enabled. <br /><br /> Script runbooks <br /><br /> Workflow runbooks <br /><br /> Runbooks with assigned worker <br /><br /> Runbook workers <br /><br /> Modules, portable modules, module activities, and module names <br /><br /> Entities – certificates, credentials, connections, variables, schedules <br /><br /> Jobs – running, suspended, completed, failed <br /><br /> Average load times – script runbooks, workflow runbooks|

## Next steps

- Learn about authoring [automated run books](authoring-automation-runbooks.md).