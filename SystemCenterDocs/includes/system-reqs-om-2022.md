---
ms.assetid: 
title: System requirements for System Center Operations Manager
description: This article describes the software and hardware system requirements for System Center Operations Manager
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 05/08/2025
ms.topic: include
ms.service: system-center
ms.subservice: operations-manager
ms.update-cycle: 1095-days
---

## Capacity limits for Operations Manager

This information helps you understand the performance and scalability characteristics of the various Operations Manager components supporting a management group.

| Monitored Item | Recommended Limit |
|:--- |:---|
| Simultaneous Operations consoles | 50 |
| Agent-monitored computers reporting to a management server | 3,000 |
| Agent-monitored computers reporting to a gateway server | 2,000 |
| Agentless Exception Monitored (AEM)-computers per dedicated management server | 25,000 |
| Agentless Exception Monitored (AEM)-computers per management group | 100,000 |
| Collective client monitored computers per management server | 2,500 |
| Management servers per agent for multihoming | 4 |
| Agentless-managed computers per management server | 10 |
| Agentless-managed computers per management group | 60 |
| Agent-managed and UNIX or Linux computers per management group | 6,000 (with 50 open consoles); 15,000 (with 25 open consoles) |
| UNIX or Linux computers per dedicated management server | 1,000 |
| UNIX or Linux computers monitored per dedicated gateway server | 100 |
| Network devices managed by a resource pool with three or more management servers | 1,000 |
| Network devices managed by two resource pools | 2,000 |
| Agents for Application Performance Monitoring (APM) | 700 |
| Applications for Application Performance Monitoring (APM) | 400 |
| URLs monitored per dedicated management server | 3,000 |
| URLs monitored per dedicated management group | 12,000 |
| URLs monitored per agent | 50 |

## Upgrade sequence

If you're upgrading an installation of System Center 2019 - Operations Manager that's integrated with one or more System Center components, it's important that you upgrade in the following order. 

1. **Orchestrator** - if you've the Operations Manager integration pack installed to support runbooks that perform automation against your Operations Manager management group. 
1. **Service Manager** - if you configured the connectors to import alert and configuration item data of objects discovered and monitored from Operations Manager. 
1. **Data Protection Manager** - if you've configured the central console to centrally manage your DPM environment. 
1. **Operations Manager** 
1. **Virtual Machine Manager** - if you've configured integration with Operations Manager to monitor the health of your VMM components, the virtual machines, and virtual machine hosts. 

## Hardware requirements

Use this information to evaluate if your hardware environment is ready to support the installation of or upgrade to System Center 2022 - Operations Manager, considering the minimum hardware requirements for processor, memory, and disk space. You should use the information here whether you're deploying one or multiple components, and for more specific information to help plan the amount of infrastructure needed for a new Operations Manager deployment, see [Operations Manager Sizing Helper](https://techcommunity.microsoft.com/t5/system-center-blog/operations-manager-2012-sizing-helper-tool/ba-p/345075)

>[!NOTE]
> While the Operations Manager 2012 Sizing helper hasn't been updated to reflect the 2016 and higher release of Operations Manager, the information provided is still valid to help you estimate for your design requirements. However, the number of UNIX/Linux computers per management and gateway server, as noted in the **Unix or Linux Monitoring** section isn't correct. The number of UNIX/Linux computers per server has increased and is noted in the monitored item capacity table earlier in this article.

| Operations Manager Server Role | x64 Processor (min) | Memory (min) | Disk space (min) |
|:--- |:---|:--- |:--- |
| Management Server | 4-Core 2.66 GHz CPU | 8 GB | 10 GB |
| Gateway Server managing up to 2000 agents | 4-Core 2.66 GHz CPU | 8 GB | 10 GB |
| Gateway Server in resource pool managing up to 500 network devices | 8-Core 2.66 GHz CPU | 32 GB | 10 GB |
| Gateway Server in resource pool managing up to 100 UNIX/Linux computers | 4-Core 2.66 GHz CPU | 4-GB RAM | 10 GB |
| Web Console server | 4-Core 2.66 GHz CPU | 8 GB | 10 GB |
| SQL Server Reporting Services server | 4-Core 2.66 GHz CPU | 8 GB | 10 GB |

## Software requirements for Operations Manager components

### Server operating system 

The following versions of Windows Server operating system are supported for the following Operations Manager components.


| Component                                                          | Windows Server 2019 Standard, Datacenter | Windows Server 2019 Server Core | Windows Server 2022 Standard, Datacenter | Windows Server 2022 Server Core |
|:--------------------------------------------------------------------|:-----------------------------------------|:-------------------------|:-----------------------------------------|:--------------------------------| :-----------------------------------------|:--------------------------------|
| **Operations Manager** Management Server                            | Yes                                      | Yes    | Yes      | Yes          |
| **Operations Manager** Gateway Server                               | Yes                                      | Yes    | Yes      | Yes          |
| **Operations Manager** Web Console                                  | Yes                                      |        | Yes      |              |
| **Operations Manager** ACS Collector                                | Yes                                      |        | Yes      |              |
| **Operations Manager** Operations console                           | Yes                                      |        | Yes      |              |
| **Operations Manager** Operational, Data Warehouse,<br>ACS database | Yes                                      | Yes    | Yes      | Yes          |
| **Operations Manager** Reporting server                             | Yes                                      |        |Yes       |              |

### Operations Manager operational, data warehouse, and ACS audit database

- Operating System: See [Server Operating System requirements](#server-operating-system).
- Microsoft SQL Server: See [SQL Server Requirements](../scom/plan-sqlserver-design.md#sql-server-requirements).

### Management server/Gateway server

- Operating System: See [Server Operating System requirements](#server-operating-system).
- Windows PowerShell version: Windows PowerShell version 2.0, or Windows PowerShell version 3.0.
- Windows Remote Management: Windows Remote Management must be enabled for the management server.
- .NET Framework 4.7.2 or .NET Framework 4.8 is required. 

### Operations Manager console

- Operating System: See [Server Operating System requirements](#server-operating-system).
- Windows PowerShell version: Windows PowerShell version 2.0, or Windows PowerShell version 3.0.
- .NET Framework 4.7.2 or .NET Framework 4.8 is required. 

### Web console

- Operating System: See [Server Operating System requirements](#server-operating-system).
- Client web browser for Silverlight-enabled dashboards:  For backward compatibility with Silverlight-enabled dashboards, Internet Explorer 11 and Silverlight 5 are required.

    >[!NOTE]
    > Operations Manager 2019 and later only includes the 64-bit version of the Operations console. 
    > The Web console doesn't support running IE in Compatibility View, otherwise you will receive a blank page when attempting to access the console. 

- Client web browser for HTML5 web console:

    - Internet Explorer version 11
    - Microsoft Edge version 88 and later
    - Google Chrome version 88 and later
    - Internet Information Services:  IIS 7.5 and later versions with the IIS Management Console and the following role services installed:
    - Static Content
    - Default Document
    - Directory Browsing
    - HTTP Errors
    - HTTP Logging
    - Request Monitor
    - Request Filtering
    - Static Content Compression
    - Web Server (IIS) Support
    - IIS 6 Metabase Compatibility
    - ASP.NET (both the 3.5 and 4.7.2 or higher versions of ASP.NET are required.)
    - Windows Authentication
 <br>
- Selected website for web console: Requires a configured http or https binding.
- .NET Framework 4.7.2 or .NET Framework 4.8 is required. 

> [!NOTE]
> Installation of the web console requires that **ISAPI and CGI Restrictions** in IIS are enabled for ASP.NET 4.8. To enable this, select the web server in **IIS Manager**, and then double-click **ISAPI and CGI Restrictions**. Select **ASP.NET v4.8**, and select **Allow**.

### Operations Manager reporting server

- Operating System: See [Server Operating System requirements](#server-operating-system).
- Microsoft SQL Server: See [SQL Server Requirements](../scom/plan-sqlserver-design.md#sql-server-requirements).
- Remote Registry Service: Must be enabled and started.
- Microsoft SQL Server Reporting Services: See [SQL Server Requirements](../scom/plan-sqlserver-design.md#sql-server-requirements).

    > [!NOTE]
    > System Center 2016 – Operations Manager and later support SQL Server Reporting Services in native mode only; don't use SharePoint integrated mode.

- .NET Framework 4.7.2 or .NET Framework 4.8 is required. 

## Client operating system

Windows 10 and Windows 11 client operating system are supported for the Operations Manager 2022 Operations console.

## Microsoft Monitoring Agent operating system

>[!NOTE]
> Operations Manager 2022 and later includes the 64-bit version of the agent.

- Windows Server 2025 - Standard, Datacenter, Server Core
- Windows Server 2022 - Standard, Datacenter, Server Core
- Windows Server 2019 - Standard, Datacenter, Server Core
- Windows Server 2016 - Standard, Datacenter, Server Core
- Windows Server 2012 R2 - Standard, Datacenter, Server Core
- Windows Server 2012 - Standard, Datacenter, Server Core
- Windows 10 - Enterprise, Pro
- Windows 11 - Enterprise, Pro
- File system: %SYSTEMDRIVE% must be formatted with the NTFS file system.
- Windows PowerShell version 3.0.
- Microsoft .NET Framework (both the 3.5 and 4.7.2 or higher versions of Microsoft .NET are required.)

    > [!NOTE]
    > Windows PowerShell is required for local collection of IntelliTrace logs, and to run System Center Operations Manager management packs that use PowerShell scripts.
    > Microsoft .NET Framework 3.5 or later is required for local collection of IntelliTrace logs and .NET Application Performance Monitoring.

## Virtualization

Microsoft supports running all System Center 2022 – Operations Manager server features in any physical or virtual environment that meets the minimum requirements that are stated in this  document. There are some restrictions on virtualization functionality that's applicable to Operations Manager.  Specifically, Microsoft doesn't support the use of the following virtualization functionality no matter what virtualization technology is used with Operations Manager:
- Virtual computers running any Operations Manager component must not make use of any functionality where all activity on the virtual computer isn't immediately committed to the virtual hard drive.  This includes making use of point-in-time snapshots, and writing changes to a temporary virtual hard drive.
- Virtual computers running any Operations Manager component can't be paused or placed into a ‘save state’ status and restarted.  They can only be shut down and restarted as would be done with a physical computer.

System Center 2016 - Operations Manager and higher runs on virtual machines in Microsoft Azure as it does on physical computer systems.  We recommend running Operations Manager on Microsoft Azure virtual machines to monitor other virtual machines or resources hosted in Azure, or monitor instances and workloads hosted on-premises.  You can also run Operations Manager on-premises and monitor Microsoft Azure virtual machines or other resources in Azure.

- Virtual computers that are running Operations Manager components can be replicated to another virtualized environment by using [Azure Site Recovery](/en-in/azure/site-recovery/site-recovery-workload). The virtualized environment referred here can be either on on-premises or Azure, and it would fail over to this environment on account of any disaster.
- If the Operations Manager databases are to be hosted on virtualized SQL Server(s), for performance reasons, we recommend that you store the Operational database and data warehouse database on a directly attached physical hard drive and not on a virtual hard disk.


## Supported coexistence

The following table lists the scenarios in which coexistence between Operations Manager 2022 and earlier versions of Operations Manager is supported.

| Version | Management Group Coexistence |
|:--- |:---|
|  Operations Manager 2019 to the latest update rollup| Yes|

## In-place upgrade

System Center 2022 - Operations Manager supports an in-place upgrade from the following versions:

- System Center 2019

## Active Directory and DNS

Operations Manager integrates with Active Directory for authentication, rights assignment, and authorization.  DNS is used for name resolution of the supporting roles in the management group as well as computers, network devices, and other monitored workloads such as web URLs.

### Active Directory Domain Services

System Center Operations Manager relies on AD DS for many services, including definition of security principles, rights assignment, authentication, and authorization. Operations Manager queries AD DS when performing computer and service discovery and can use AD DS for storing and distributing agent configuration information. For Operations Manager to function properly, AD DS and its supporting service, DNS, need to be healthy and at certain minimum configuration levels. In addition, certain domain naming conventions must be followed.

### Domain space naming

An Operations Manager management group can't be installed into a root Active Directory domain that has a flat DNS namespace. However, you can install the management group into child domains of the root domain. For example, you've a root domain that has a DNS name of "Woodgrove". Because this root domain has a flat DNS namespace, you can't install an Operations Manager management group into the Woodgrove domain. But, if the Woodgrove domain has a child domain with a DNS name of "National", the fully qualified domain name of the child domain would be national.woodgrove. For more information about configuring Windows for domains with single-label DNS names, see Information about configuring Active Directory domains by using single-label DNS names.

### Domain functional level

Windows Server Active Directory can operate at different functional levels. These levels are distinguished by the version of the Windows Server operating system that is permitted on the domain controllers present in the domain. System Center Operations Manager doesn't have a domain functional level requirement.

### Forest functional level

The forest functional level is similar to the domain functional level in that it sets a minimum domain controller operating system level across the whole forest. After it's set, domain controllers with down-level operating systems from lower functional levels can't be introduced into the forest. Operations Manager doesn't have a forest functional level requirement.

### DNS

DNS must be installed and in a healthy state to support AD DS. Beyond the reliance of Operations Manager on AD DS, there are no specific DNS requirements.
