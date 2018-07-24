---
title: System Center Operations Manager 1801 Release Notes
description: This article describes issues and workarounds for System Center Operations Manager 1801.  
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 06/11/2018
ms.custom: na
ms.prod: system-center-2016
monikerRange: 'sc-om-1801'
ms.assetid: 
ms.technology: operations-manager
ms.topic: article
---

# System Center Operations Manager 1801 Release Notes

The following release notes apply to System Center Operations Manager 1801.

## Telemetry for HTML5 dashboards
**Description:** System Center Operations Manager collects diagnostics and usage data about itself, which is used by Microsoft to improve the installation experience, quality, and security of future releases.  With the release of the new HTML5 dashboards, usage telemetry is collected with Application Insights, not from the Usage and Diagnostic feature in the management group.  For more information on what user telemetry is collected by Application Insights, see [Usage analysis with Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-usage-overview).

**Workaround:** Disable the Diagnostic and Usage data collection setting in the Operations console from the **Administration** workspace under **Settings\Privacy**.       

## Edit Company Knowledge
**Description:** If the company knowledge of an alert/monitor/rule is already saved while editing in the Operations console and then the company knowledge of the same alert/monitor/rule is edited and saved using the new HTLM5 dashboards in the Web console, the content that was saved originally using the Operations console is overridden with the content saved through the Web console.

**Workaround:** None

## Access Silverlight dashboards in Web Console using a different URL
**Description:** With HTML5 dashboards in Operations Manager 1801, the entire Web console is HTML based. Silverlight dashboards cannot be displayed in the Web console. To access  existing Silverlight dashboards, you have to access using the following URL using Internet Explorer with Silverlight enabled - `http(s)://<Servername>/dashboard`. 

## Attempting to upgrade Reporting server fails prerequisites check
**Description:** While attempting to perform an upgrade of System Center 2016 - Operations Manager Reporting server to version 1801, the prerequisites checker will report the following error: **Management Server Upgraded Check - The management server to which this component reports has not been upgraded.** and the upgrade cannot proceed.  This error occurs in a distributed management group scenario where the Reporting server is on a server  separate from one or more management servers in the management group.   

**Workaround:** Install the System Center 2016 - Operations Manager Operations console on the server hosting the Reporting server role and then retry upgrading the Reporting server role to version 1801.  Once the upgrade is successfully completed, you can uninstall the upgraded Operations console from the Reporting server.  

## Application Performance Monitoring (APM) agent-component issues
**Description:** The Application Performance Monitoring (APM) feature in System Center Operations Manager version 1801 agent can cause a crash with IIS Application pools and may crash the SharePoint Central Administration v4 application pool running .NET Framework 2.0 and prevent it from starting.  This behavior can occur on an IIS web server even if the APM feature has not been enabled and configured after the agent is installed.     

**Workaround:** If the APM feature is not required on the server, reinstall the agent and include the **NOAPM=1** parameter on the setup command line to prevent the APM feature from being included.  Alternatively, you can reconfigure the agent already installed using [Windows Installer repair option](https://msdn.microsoft.com/library/windows/desktop/aa367988%28v=vs.85%29.aspx) and remove the APM component - **msiexec.exe /fvomus "<path to x64 installer package>\MOMagent.msi" NOAPM=1**.  For IIS web servers where the agent is already installed but the APM feature has not been enabled and configured, grant the application pool account **Read** access permission to: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\System Center Operations Manager\12\APMAgent**.  This permissions issue prevents the APM feature from being able to read that key and may cause the application pool process to crash.

## In-place upgrade from Operations Manager 2016 will fail if ACS Linux/UNIX MP installed
**Description**: If you have already installed the Audit Collection Services (ACS) Linux/UNIX management packs, and you are attempting to upgrade from Operations Manager 2016 RTM to the latest update rollup, the upgrade will fail and results in removal of the management server role.  

**Cause**: There is an issue with the installer package during the upgrade process, where setup tries to upgrade the ACS management pack but it has a dependency on the Microsoft.Linux.Universal.Library.MP. If this dependency management pack is not upgraded, importing the ACS MP will fail during the process and the following error is displayed:

```
Error:Found error in 2|Microsoft.ACS.Linux.Universal|7.7.1124.0|Microsoft.ACS.Linux.Universal|| with message:  
Could not load management pack <ID=Microsoft.Linux.Universal.Library, KeyToken=31bf3856ad364e35, Version=7.7.1103.0>. The management pack was not found in the store.  
: Version mismatch. The management pack (<Microsoft.Linux.Universal.Library, 31bf3856ad364e35, 7.6.1064.0>) requested from the database was version 7.7.1103.0 but the actual version available is 7.6.1064.0.  
```

The upgrade failure will cause setup to roll back and leave the management server in an inconsistent state where the feature will need to be reinstalled.  

**Workaround**:  Before performing the upgrade of the management server, upgrade Microsoft.Linux.Universal.Library management pack or delete the ACS management pack in the management group.
