---
title: include file
description: include file to provide information about how to upgrade to System Center Service Provider Foundation (SPF) 1801 from a previous version.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date:  02/21/2023
ms.topic: include
ms.service:  system-center
ms.subservice:  service-provider-foundation
ms.assetid: 3cd2845a-bcc9-4aab-b26b-a17a3a1ae98b
---

## Upgrade to System Center 1801 -  Service Provider Foundation

The following sections describe the procedures required to upgrade from System Center 2012 R2 SPF or System Center 2016 SPF to SPF 1801.

## Prerequisites

- SPF:
    - On System Center 2012 R2, install [update rollup 12](https://support.microsoft.com/help/3209618/update-rollup-12-for-system-center-2012-r2-orchestrator-service-provid) or later in order to upgrade to 1801.
    - On System Center 2016, install [update rollup 2](https://support.microsoft.com/help/3209598/update-rollup-2-for-system-center-2016-orchestrator-service-provider-f) or later in order to upgrade to 1801.
- VMM:
    -  On System Center 2012 R2, install [update rollup 12](https://support.microsoft.com/help/3209585/update-rollup-12-for-system-center-2012-r2-virtual-machine-manager) or later in order to upgrade to 1801.
    - On System Center 2016, install [update rollup 2](https://support.microsoft.com/help/3209586/update-rollup-2-for-system-center-2016-virtual-machine-manager) or later in order to upgrade to 1801.
- Microsoft Azure Pack - Install [update rollup 12](https://support.microsoft.com/help/4043909/update-rollup-12-for-windows-azure-pack) or later.
- VMM management console - The machine running the VMM 2012 R2 or 2016 management console should have the latest VMM updates installed.


## Assumptions
The upgrade instructions in this article assume the following scenario:

- SPF and VMM are running on System Center 2016.
- We highly recommend that you reuse the current SPF server name to simplify the seamless integration into your existing Microsoft Azure Pack deployment.
- The VMM console is installed on a separate computer.
- The upgrade uses the existing SPF server name.
- These upgrade instructions assume that the VMM 1810 upgrade has already been completed, and that the necessary backups of the current Microsoft Azure Pack environment have been performed.

## Upgrade order

Here's the recommended upgrade order for the above scenario:

1. Update the VMM console to 1801. If required, update the VMM server to 1801.
2. Update SPF to 1801.


## Before you start

1. Ensure Microsoft Azure Pack, SPF, and VMM are all running the required updates.
2. We recommend that you shut down VMM and Microsoft Azure Pack servers, removing all database activity.
3. Verify SPF [system requirements](../spf/system-requirements-spf.md?preserve-view=true&view=sc-spf-1801). Ensure that SPF must run on Windows Server 2016 - Core or Desktop experience.
4. Verify VMM [console requirements](../vmm/system-requirements.md?preserve-view=true&view=sc-vmm-1801#vmm-console-operating-system).


## Run the SPF upgrade

### Prepare the SPF 1801 machine

1. Create a new server running Windows Server 2016 on which to install SPF 1801. You can use a VM. In our example, we'll create a machine call **SERVER-SPF-UPGRADE**.
2. Install the prerequisites on the new VM as follows:
    - Install [SQL ODBC Drivers](https://www.microsoft.com/download/details.aspx?id=36434).
    - Install [SQL Native Client](https://www.microsoft.com/download/details.aspx?id=50402)
    - Install SQL Server [command line utilities](https://www.microsoft.com/download/details.aspx?id=53591).
    - Install SQL Server [CLR types](https://www.microsoft.com/download/details.aspx?id=42295).
    - Install IIS with the following features: PowerShell: Install-WindowsFeature Web-Server, Web-WebServer, Web-Common-Http, Web-Default-Doc, Web-Dir-Browsing, Web-Http-Errors, Web-Static-Content, Web-Health, Web-Http-Logging, Web-Request-Monitor, Web-Http-Tracing, Web-Performance, Web-Stat-Compression, Web-Security, Web-Filtering, Web-Basic-Auth, Web-Windows-Auth, Web-App-Dev, Web-Net-Ext45, Web-Asp-Net45, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Mgmt-Tools, Web-Mgmt-Console, Web-Scripting-Tools, NET-Framework-45-ASPNET, NET-WCF-HTTP-Activation45, ManagementOdata, WAS, WAS-Process-Model, WAS-Config-APIs.
    - Install [WCF Data Services 5.0 for OData V3](https://www.microsoft.com/download/details.aspx?id=29306).
    - Install [ASP.NET MVC 4](https://www.microsoft.com/download/details.aspx?id=30683).
3. Install the latest Windows updates on the VM.
4. Restart the VM to ensure there are no pending reboots.
5. Don't join the VM to a domain.

### Remove SPF 2012 R2/2016

1. Uninstall the VMM admin console on the SPF machine.
2. Uninstall the SPF Web Component on the SPF machine.
3. Rename the machine. For example, from **SERVER-SPF-01** to **SERVER-SPF-OLD**.

### Set up the SPF 1801 machine

1. Rename the VM you set up to the original name of the SPF machine, so from **SERVER-SPF-UPGRADE** to **SERVER-SPF-01**.
2. Join the VM to the domain.
3. Install the [VMM console](../vmm/install-console.md?preserve-view=true&view=sc-vmm-1801). For a core installation, you can install from the [command line](../vmm/install-console.md?preserve-view=true&view=sc-vmm-2016#install-the-console-from-the-command-prompt) or set up from the user interface and change to Core later.
4. Install [SPF 2016](../spf/deploy-spf.md?preserve-view=true&view=sc-spf-1801) using the existing SQL Server database name during setup.


## Post-upgrade tasks
1. SPF needs a server certificate for website binding. You can use the self-signed certificate generated during setup, but we don't recommend this for a production environment.
2. If you do use a self-signed certificate:
    - It should be used only for testing purposes.
    - The FQDN should be specified for the certification path instead of "localhost".
    - It should be located in the personal or web hosting store.

## Test Microsoft Azure Pack

Test everything's working as follows:

1. Start VMM 1801.
2. In the Microsoft Azure Pack  Admin portal, check in this order: 1) VMs; 2) Gallery items; 3) Templates; 4) SPF configuration settings. Ensure everything's working as expected.
3. In the Microsoft Azure Pack Tenant portal, check in this order: 1) Deployment settings; 2) VMs; 3) Plans; 4) Deployment options. Ensure everything's working as expected.