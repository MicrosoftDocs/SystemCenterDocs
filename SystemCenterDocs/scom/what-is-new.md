---
ms.assetid: c46cb9b2-e66e-4f06-9020-2157b063df3a
title: What's New in Operations Manager
description: This article describes what's new in System Center Operations Manager compared to previous versions. 
author: mgoedtel
ms.author: magoedte
manager: cfreeman
ms.date: 11/09/2017
ms.custom: na
ms.prod: system-center-2016
ms.technology: operations-manager
ms.topic: article
---

# What's New in Operations Manager

The content in this section describes what's new and changed in System Center 2016 - Operations Manager.

::: moniker range="sc-om-1711"

## New features in Operations Manager 1711

### Linux monitoring 

You can now use a Linux agent with FluentD support for log file monitoring at par with Windows Server.  This update provides the following improvements over previous log file monitoring:

- Wild card characters in log file name and path.
- New match patterns for customizable log search like simple match, exclusive match, correlated match, repeated correlation and exclusive correlation.
- Support for generic Fluentd plugins published by the fluentd community.

### Improved HTML console experience

The Web console has been redesigned and is now a fully HTML-based console and no longer has a dependency on Silverlight.  The monitoring tree and dashboards support the HTLM5 markup language.  

### Enhanced SDK Client performance 
We have made performance improvements in the Operations console that typically prevent the console from responding while a new management pack is being imported or deleted, or a configuration change to a MP is saved.  

### Updates and recommendations for third-party Management Packs

In System Center 2016 we released the MP Updates and Recommendations feature which has been expanded now to include discovery and downloads of third-party management pack updates, based on feedback from customers. 

### Linux Kerberos support 
Operations Manager can now support Kerberos authentication wherever the WS-Management protocol is used by the management server to communicate with UNIX and Linux computers, providing greater security by no longer needing to enable basic authentication for Windows Remote Management (WinRM). 

### Service Map integration
Service Map automatically discovers application components on Windows and Linux systems and maps the communication between services. It automatically builds a common reference map of dependencies across your servers, processes, and third-party services. Integration between Service Map and System Center Operations Manager allows you to automatically create distributed application diagrams in Operations Manager that are based on the dynamic dependency maps in Service Map.  For further information on planning and configuring  integration, see [Service Map integration with System Center Operations Manager](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-service-map-scom).  

::: moniker-end

## Improve desktop console performance

With the release of System Center 2016 - Operations Manager, we have made performance improvements to state and diagram views in the Operations console to improve load performance  (these improvements are in addition to the alert view optimizations).


## Send E-mail notifications with external authentication

Operations Manager now supports sending notifications from an e-mail server, either within the organization or external and configuring a Run As account to authenticate with that external messaging system.


## Non Silverlight Web console (except Dashboard views)

With the release of System Center 2016 - Operations Manager, we have removed the Silverlight dependency from all the Web console views except Dashboard views.
This feature provides the following value:
- No more Silverlight prerequisite to access Operations Manager Web console
- Operations Manager Web console can be accessed from multiple web browsers like Edge, Chrome and Firefox
- Performant experience

> [!NOTE]
> Dashboard views are still dependent on Silverlight, which can be accessed through Internet Explorer with Silverlight plug in.  


## Access Schedule Maintenance Mode from Monitoring pane and maintenance mode from client side

Schedule Maintenance mode is a feature released in System Center 2016 - Operations Manager to suspend monitoring of an object during regular software or hardware maintenance activities, such as software updates or hardware replacements. Entities can be put to maintenance in older versions of Operations Manager, but they cannot be put into maintenance mode at a future time. The newly created Maintenance Mode Scheduling wizard gives the ability to choose different types of entities to put into maintenance and to schedule maintenance at a future time.

With the release of System Center 2016 - Operations Manager, Operators can access the “Maintenance Schedules” feature from the monitoring pane without the dependency on administrators to schedule maintenance at a future time. We now supports allowing a server administrator to set the agent-managed computer in maintenance mode directly from the computer itself, without needing to perform this from the Operations console.  This can be performed with the new PowerShell cmdlet **Start-SCOMAgentMainteannceMode**.  


## Management Pack Updates and Recommendations

We have added a new capability to Operations Manager to assess the management packs.  Operations Manager includes a new feature called Updates and Recommendations, to help you proactively identify new technologies or components (i.e. workloads) deployed in your IT infrastructure that were not monitored by Operations Manager or are not monitored using the latest version of a management pack. For more information about Updates and Recommendations see  [Management Pack Assessment](manage-mp-mpassessment.md).


## Alert data management

With the release of System Center 2016 – Operations Manager, you get better visibility of the alerts being generated in your management group which helps you reduce alerts that you don't consider actionable or relevant.   

This feature provides the following benefits:

- Identify the number of alerts each management pack has generated.

- Identify the number of alerts generated by a monitor/rule with in each management pack.

- Identify different source/s (along with alert count) which have generated an alert for a particular type of alert.

- Filter the data for the desired duration so that you can understand what was happening during a particular period of time.

- This information enables you to make informed decisions on tuning the thresholds or disabling the alerts which you consider noisy.

This feature is available for members of the Operations Manager Administrators role from the Tune Management Packs screen in the Operations console.  


## Extensible network monitoring

In System Center 2016 - Operations Manager, we include a tool which will allow you to create a custom management pack to monitor generic network devices (non-certified as of Operations Manager 2012 R2) and include resource utilization metrics, such as processor and memory. Or you can create extended monitoring workflows for an existing network device already monitored by your management group. This tool enables customers to generate a management pack for their network devices to get extended network monitoring. In addition to the current extended monitoring support for Network devices (Processor and Memory monitoring), this tool enables customers to add monitoring of additional device components such as fan, temperature sensor, voltage sensor and power supply.  


## Monitoring Nano Server and workloads

In the System Center 2016 – Operations Manager release, we have included support to monitor Nano Server:

-  Discover a Nano Server and push Nano-compatible agent to the server from the console

-  Monitor Internet Information Services (IIS) and Domain Name System (DNS) roles

-  Supports ACS security audit event collection

-  Support Active Directory Integration for managing agent assignment

-  Deploy the Nano-compatible agent manually using a PowerShell script included in this release

-  Manage updating the Nano-compatible agent directly from the console as you do today with the Windows agent, or manually on Nano Server using a PowerShell script included in this release

For specific instructions on how to configure System Center 2016 - Operations Manager to monitor Nano Server, see [Monitoring Nano Server](manage-deploy-windows-agent-nano.md).


## Scalability improvement with Unix/Linux agent monitoring

Operations Manager includes improved scalability in how many Unix/Linux agents that can be monitored per Management server.  You can now monitor up to 2X the number of Unix/Linux servers per management server, against the previously supported scale.

Operations Manager now uses the new Async Windows Management Infrastructure (MI) APIs instead of WSMAN Sync APIs, which Operations Manager uses by default. To leverage this  scalability improvement, you need to create the new Registry key “UseMIAPI” to enable Operations Manager to use the new Async MI APIs on management servers monitoring Linux/Unix systems.  Perform the following steps:

1. Open the **Registry Editor** from an elevated **Command Prompt**.

2. Create registry key **UseMIAPI** under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Operations Manager\3.0\Setup**.

If you need to restore the original configuration using the WSMAN Sync APIs, you can delete the UseMIAPI registry key.


## Extend Operations Manager with Operations Management Suite

With Microsoft Operations Management Suite you can extend your management capabilities by connecting your Operations Management infrastructure to management and analysis services provided through your Azure account. The main scenarios for connecting System Center 2016 - Operations Manager to Microsoft Operations Management Suite include:

-   Configuration Assessment

-   Alert Management

-   Capacity Planning

For more information please review the Microsoft Operations Management Suite [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx) documentation.


## Partner Program in Administration pane

Customers can view certified System Center Operations Manager partner solutions directly from the console. Customers can obtain a view of the partner solutions and visit the partner websites to download and install the solutions.  

## What’s new in System Center 2016 Operations Manager UNIX/Linux monitoring

- New Management Packs and providers for Apache HTTP Server and MySQL/MariaDB database server monitoring.

- The Operations Manager agents for UNIX and Linux include Open Management Infrastructure (OMI) version 1.1.0. OMI is now packaged separately (in a package named omi) from the Operations Manager agent providers (in a package named scx).

- Shell command and script rules and monitors are multi-threaded in the agent and will run in parallel.

-	New UNIX/Linux Script templates have been added for:
  -	Two-state monitors
  - Three-state monitors
  - Agent tasks
  - Performance-collecting rules
  - Alert-generating rules

These templates allow you to copy and paste a monitoring script into a template for simple integration with Operations Manager monitoring. The script can be shell, perl, Python, Ruby, or any other script language with a corresponding interpreter specified by the script’s shebang.

- Recovery and diagnostic task templates are now available to create recovery and diagnostic tasks with shell commands and scripts

- Default credentials can now be used when discovery UNIX and Linux computers with the Discovery Wizard or PowerShell

- Discovery of logical disks (file systems) for UNIX and Linux agents can be filtered by file system name or type. Discovery rule overrides can be used to exclude file systems that you do not wish to monitor.
