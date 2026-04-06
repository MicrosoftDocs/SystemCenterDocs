---
title: include file
description: include file to provide information about how to upgrade to System Center Service Provider Foundation (SPF) 2022.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 08/20/2025
ms.topic: include
ms.service:  system-center
ms.subservice:  service-provider-foundation
ms.update-cycle: 1095-days
ms.assetid: 
---

## Upgrade to System Center 2022 -  Service Provider Foundation

The following sections describe the procedures required to upgrade from SPF 2019 to 2022.

## Prerequisites

- SPF:
    - SPF 2019 installed.
- VMM:
    - VMM 2019 installed
- Windows Azure Pack - Install [update rollup 12](https://support.microsoft.com/help/4043909/update-rollup-12-for-windows-azure-pack) or later.
- VMM management console - The machine running the VMM 2019 management console should have the latest VMM updates installed.


## Assumptions
The upgrade instructions in this article assume the following scenario:

- SPF and VMM are running on System Center 2019.
- We highly recommend that you reuse the current SPF server name to simplify the seamless integration into your existing Windows Azure Pack deployment.
- The VMM console is installed on a separate computer.
- The upgrade uses the existing SPF server name.
- These upgrade instructions assume that the VMM 2022 upgrade has already been completed, and that the necessary backups of the current Windows Azure Pack environment have been performed.

## Upgrade order

Here's the recommended upgrade order for the above scenario:

1. Update the VMM console to 2022. If necessary, update the VMM server to 2022.
2. Update SPF to 2022.


## Before you start

1. Ensure Windows Azure Pack, SPF, and VMM are all running the required updates.
2. We recommend that you shut down VMM and Windows Azure Pack servers, removing all database activity.
3. Verify SPF [system requirements](../spf/system-requirements-spf.md). Ensure that SPF must run on Windows Server 2022 - Core or Desktop experience.
4. Verify VMM [console requirements](../vmm/system-requirements.md?preserve-view=true&view=sc-vmm-1801#vmm-console-operating-system).


## Run the SPF upgrade

Prepare the SPF 2022 computer on which you want to run the upgrade.

1. Create a new server running Windows Server 2022 on which you want to install SPF 2022. You can also use a Virtual Machine (VM).
2. In our example, we'll create a machine call **SERVER-SPF-UPGRADE**.
3. Install the prerequisites on the new VM as follows:
    - Install [SQL ODBC Drivers](/sql/connect/odbc/download-odbc-driver-for-sql-server?view=sql-server-2016&preserve-view=true).
    - Install [SQL Native Client](https://www.microsoft.com/en-us/download/details.aspx?id=50402)
    - Install SQL Server [command line utilities](https://www.microsoft.com/en-us/download/details.aspx?id=53591).
    - Install SQL Server [CLR types](https://www.microsoft.com/en-us/download/details.aspx?id=42295).
    - Install IIS with the following features: PowerShell: Install-WindowsFeature Web-Server, Web-WebServer, Web-Common-Http, Web-Default-Doc, Web-Dir-Browsing, Web-Http-Errors, Web-Static-Content, Web-Health, Web-Http-Logging, Web-Request-Monitor, Web-Http-Tracing, Web-Performance, Web-Stat-Compression, Web-Security, Web-Filtering, Web-Basic-Auth, Web-Windows-Auth, Web-App-Dev, Web-Net-Ext45, Web-Asp-Net45, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Mgmt-Tools, Web-Mgmt-Console, Web-Scripting-Tools, NET-Framework-45-ASPNET, NET-WCF-HTTP-Activation45, ManagementOdata, WAS, WAS-Process-Model, WAS-Config-APIs.
    - Install [WCF Data Services 5.0 for OData V3](https://www.microsoft.com/download/details.aspx?id=29306).
    - Install [ASP.NET MVC 4](https://www.microsoft.com/download/details.aspx?id=30683).
4. Install the latest Windows updates on the VM.
5. Restart the VM to ensure there are no pending reboots.
   >[!NOTE]
   > Don't join the VM to a domain.


### Remove SPF 2019

1. Uninstall the VMM admin console on the SPF machine.
2. Uninstall the SPF Web Component on the SPF machine.
3. Rename the machine. For example, from **SERVER-SPF-01** to **SERVER-SPF-OLD**.

### Set up the SPF 2022 computer

1. Rename the VM you set up. Use the original name of the SPF computer. So, change the VM name from **SERVER-SPF-UPGRADE** to **SERVER-SPF-01**.
2. Join the VM to the domain.
3. Install the [VMM console](../vmm/install-console.md). For a core installation, you can install from the [command line](../vmm/install-console.md#install-the-console-from-the-command-prompt), or set up from the user interface and change to Core later.
4. Install [SPF 2022](../spf/deploy-spf.md), using the existing SQL Server database name during setup.


## Post-upgrade tasks
1. SPF needs a server certificate for website binding. You can use the self-signed certificate generated during setup, but we don't recommend this for a production environment.
2. If you do use a self-signed certificate:
    - It should be used only for testing purposes.
    - The FQDN should be specified for the certification path instead of "localhost".
    - It should be in the personal or web hosting store.

## Test Windows Azure Pack

Test everything's working as follows:

1. Start VMM 2022.
2. In the Windows Azure Pack  Admin portal, check in this order: 
    1. VMs
    1. Gallery items
    1. Templates
    1. SPF configuration settings. 
   Ensure everything's working as expected.
3. In the Windows Azure Pack Tenant portal, check in this order: 
    1. Deployment settings
    1. VMs 
    1. Plans
    1. Deployment options. 
   Ensure everything's working as expected.