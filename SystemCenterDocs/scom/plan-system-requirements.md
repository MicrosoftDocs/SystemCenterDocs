---
ms.assetid: 1921b7dc-6537-4378-bdc5-de5fbd3e619a
title: System Requirements for System Center 2016 - Operations Manager
description: The system requirements article provides general performance and scalability guidance for consideration as part of your design planning of Operations Manager 2016.  
author: mgoedtel
ms.author: magoedte
manager: carmonm
ms.date: 05/25/2017
ms.custom: na
ms.prod: system-center-2016
ms.technology: operations-manager
ms.topic: article
---

# System requirements for System Center 2016 - Operations Manager

>Applies To: System Center 2016 - Operations Manager

The topic describes general performance and scalability guidance for System Center 2016 - Operations Manager and recommends hardware configurations for a variety of workloads. Because System Center 2016 – Operations Manager is built to be flexible and scalable, the hardware requirements for specific scenarios may differ from the guidelines that are presented here.  A discussion of the factors that affect the performance of each Operations Manager component is detailed in other sections of the planning guide so that they can be adapted to specific requirements.

## Capacity limits for Operations Manager

This information helps you understand the performance and scalability characteristics of the various Operations Manager components and the management group which is comprised of these different components.  

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
| UNIX or Linux computers monitored per dedicated gateway server | 200 |
| Network devices managed by a resource pool with three or more management servers | 1,000 |
| Network devices managed by two resource pools | 2,000 |
| Agents for Application Performance Monitoring (APM) | 700 |
| Applications for Application Performance Monitoring (APM) | 400 |
| URLs monitored per dedicated management server | 3,000 |
| URLs monitored per dedicated management group | 12,000 | 
| URLs monitored per agent | 50 |

## Upgrade sequence
If you are upgrading an installation of System Center 2012 R2 Operations Manager that is integrated with one or more System Center components, it is important that you upgrade in the following order.  

1. Orchestrator - if you have the Operations Manager integration pack installed to support runbooks that perform automation against your Operations Manager management group. 
2. Service Manager - if you configured the connectors to import alert and configuration item data of objects discovered and monitored from Operations Manager. 
3. Data Protection Manager - if you have configured the central console to centrally manage your DPM environment.
4. Operations Manager  
5. Virtual Machine Manager - if you have configured integration with Operations Manager to monitor the health of your VMM components, the virtual machines and virtual machine hosts. 

## Hardware requirements

Use this information to evaluate if your hardware environment is ready to support the installation of or upgrade to System Center 2016 - Operations Manager, considering the minimum hardware requirements for processor, RAM, and disk space.  You should use the information here whether you are deploying one or multiple components and for more specific information to help plan the amount of infrastructure needed for a new Operations Manager deployment, refer to the [Operations Manager 2012 Sizing Helper](http://go.microsoft.com/fwlink/p/?LinkId=231853).

> [!NOTE] 
> While the Operations Manager 2012 Sizing helper has not been updated to reflect the 2016 release of Operations Manager, the information provided is still valid to help you estimate for your design requirements.  However, the number of UNIX/Linux computers per management and gateway server, as noted in the **Unix or Linux Monitoring** section is not correct.  The number of UNIX/Linux computers per server has increased and is noted in the monitored item capacity table earlier in this article.  This will be addressed in an updated release of the sizing helper document.  


| Operations Manager Server Role | x64 Processor (min) | Memory (min) | Disk space (min) |
|:--- |:---|:--- |:--- |
| Management Server | 4-Core 2.66 GHz CPU | 8 GB | 10 GB |
| Gateway Server managing up to 2000 agents | 4-Core 2.66 GHz CPU | 8 GB | 10 GB |
| Gateway Server in resource pool managing up to 500 network devices | 8-Core 2.66 GHz CPU | 32 GB | 10 GB |
| Gateway Server in resource pool managing up to 100 UNIX/Linux computers | 4-Core 2.66 GHz CPU | 4 GB RAM | 10 GB |
| Web Console server | 4-Core 2.66 GHz CPU | 8 GB | 10 GB | 
| SQL Server Reporting Services server | 4-Core 2.66 GHz CPU | 8 GB | 10 GB |

## Software requirements for Operations Manager components

### Server operating system   

The following versions of Windows Server operating system are supported for the following Operations Manager components.

| Component | Windows Server 2012 R2 Standard, Datacenter | Windows Server 2016 Standard, Datacenter | Windows Server Core 2016 |
|:--- |:---|:--- |:--- |
| **Operations Manager** Management Server | yes | yes | yes |
| **Operations Manager** Gateway Server | yes | yes | |
| **Operations Manager** Web Console | yes | yes | |
| **Operations Manager** ACS Collector | yes | yes | |
| **Operations Manager** Operations console | yes | yes | |


### Client operating system 

The following versions of Windows client operating system are supported for the Operations Manager Operations console.

| Windows 7 | Windows 8 | Windows 8.1 | Windows 10 |
|:--- |:---|:--- |:--- |
| yes | yes | yes | yes |

### Microsoft Monitoring Agent operating system 

The following versions of Windows operating system are supported for the Microsoft Monitoring Agent connecting to Operations Manager.

Windows Server 2016, Windows Server 2016 Nano Server, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 Service Pack 1, Windows Server 2008 Service Pack 2, Windows 10, Windows 8 Enterprise, Windows 8 Pro, Windows Embedded POSReady 2009, Windows 7, Windows Embedded Standard 7 Service Pack 1.

- File system: %SYSTEMDRIVE% must be formatted with the NTFS file system.
- Windows PowerShell version: Windows PowerShell version 2.0, or Windows PowerShell version 3.0.
- Microsoft .NET Framework 3.5 or later
  
> [!NOTE] 
> Windows PowerShell is required for local collection of IntelliTrace logs, and to run System Center Operations Manager management packs that use PowerShell scripts.

> Microsoft .NET Framework 3.5 or later is required for local collection of IntelliTrace logs and .NET Application Performance Monitoring.

### Management server/Gateway server 

- Operating System: See [Server Operating System requirements](#server-operating-system-requirements).   
- Windows PowerShell version: Windows PowerShell version 2.0, or Windows PowerShell version 3.0.
- Windows Remote Management: Windows Remote Management must be enabled for the management server.
- NET Framework 4 or .NET Framework 4.5 is required. 

### Operations Manager console 

- Operating System: See [Server Operating System requirements](#server-operating-system-requirements).     
- Windows PowerShell version: Windows PowerShell version 2.0, or Windows PowerShell version 3.0.
- Microsoft Report Viewer 2015 runtime.  

    > [!NOTE] 
    > Report Viewer has a dependency on [Microsoft CLR Types for SQL Server 2014](https://www.microsoft.com/download/details.aspx?id=42295).  The SQL Server System CLR Types package contains the components implementing the geometry, geography, and hierarchy ID types in SQL Server 2014. This component can be installed separately from the server to allow client applications to use these types outside of the server. 

- NET Framework 4 or .NET Framework 4.5 is required. 

### Web console 

- Operating System: See [Server Operating System requirements](#server-operating-system-requirements).  
- Client web browser:  Internet Explorer 11 and SilverLight 5  
- Internet Information Services:  IIS 7.5 and later versions, with the IIS Management Console and the following role services installed:

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
    - ASP.NET (both the 2.0 and 4.0 versions of ASP.NET are required.) 
    - Windows Authentication 
 <br>
- Selected website for web console: Requires a configured http or https binding.
- The System Center 2012 R2 Operations Manager SharePoint Dashboard Viewer Web Part is supported on SharePoint 2010 and SharePoint 2013. However, it is not supported on Office 365 SharePoint.
- NET Framework 4 or .NET Framework 4.5 is required. 

> [!NOTE]
> Installation of the web console requires that **ISAPI and CGI Restrictions** in IIS are enabled for ASP.NET 4. To enable this, select the web server in **IIS Manager**, and then double-click **ISAPI and CGI Restrictions**. Select **ASP.NET v4.0.30319**, and then click **Allow**.

> [!WARNING]
> You must install IIS before installing .NET Framework 4. If you installed IIS after installing .NET Framework 4, you must register ASP.NET 4.0 with IIS. Open a Command prompt window by using the Run As Administrator option, and then run the following command:
**%WINDIR%\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -r**

### Operations Manager reporting server

- Operating System: See [Server Operating System requirements](#server-operating-system-requirements).   
- Microsoft SQL Server: See [SQL Server Requirements](plan-sqlserver-design.md#sql-server-requirements).
- Remote Registry Service: Must be enabled and started.
- Microsoft SQL Server Reporting Services: See [SQL Server Requirements](plan-sqlserver-design.md#sql-server-requirements). 

    > [!NOTE] 
    > System Center 2016 – Operations Manager supports SQL Server Reporting Services in native mode only; do not use SharePoint integrated mode.  

- NET Framework 4 or .NET Framework 4.5 is required. 

## Virtualization

Microsoft supports running all System Center 2016 – Operations Manager server features in any physical or virtual environment that meets the minimum requirements that are stated in this  document.  There are some restrictions on virtualization functionality that is applicable to Operations Manager.  Specifically, Microsoft does not support the use of the following virtualization functionality no matter what virtualization technology is used with Operations Manager: 
- Virtual computers running any Operations Manager 2016 component must not make use of any functionality where all activity on the virtual computer is not immediately committed to the virtual hard drive.  This includes making use of point-in-time snapshots, and writing changes to a temporary virtual hard drive. 
- Virtual computers running any Operations Manager 2016 component cannot be paused or placed into a ‘save state’ status and restarted.  They can only be shut down and restarted just as would be done with a physical computer. 
- Virtual computers that are running any Operations Manager 2016 components cannot be relocated to another host physical server by using any automated process. 
- If the Operations Manager databases are to be hosted on virtualized SQL Server(s), for performance reasons, we recommend that you store the Operational database and data warehouse database on a directly attached physical hard drive and not on a virtual hard disk.

System Center 2016 - Operations Manager runs on virtual machines in Microsoft Azure just as it does on physical computer systems.  We recommend running Operations Manager on Microsoft Azure virtual machines to monitor other virtual machines or resources hosted in Azure, or monitor instances and workloads hosted on-premises.  You can also run Operations Manager on-premises and monitor Microsoft Azure virtual machines or other resources in Azure.  

## Supported coexistence

The following table lists the scenarios in which coexistence between Operations Manager 2016 and earlier versions of Operations Manager is supported.

| Version | Management Group Coexistence |
|:--- |:---|
|  Operations Manager 2012 R2 | Yes

## In-place upgrade 

System Center 2016 - Operations Manager supports an in-place upgrade from the following versions:

- System Center 2016 Technical Preview 5 - Operations Manager
- System Center 2012 R2 Operations Manager with Update Rollup 9

## Active Directory and DNS

Operations Manager integrates with Active Directory for authentication, rights assignment, and authorization.  DNS is leveraged for name resolution of the supporting roles in the management group as well as computers, network devices, and other monitored workloads such as web URLs.  

### Active Directory Domain Services

System Center 2016 – Operations Manager relies on AD DS for a number of services, including definition of security principles, rights assignment, authentication, and authorization. Operations Manager queries AD DS when performing computer and service discovery and can use AD DS for storing and distributing agent configuration information. For Operations Manager to function properly, AD DS and its supporting service, DNS, need to be healthy and at certain minimum configuration levels. In addition, certain domain naming conventions must be followed.

### Domain space naming

An Operations Manager management group cannot be installed into a root Active Directory domain that has a flat DNS namespace. However, you can install the management group into child domains of the root domain. For example, you have a root domain that has a DNS name of "Woodgrove". Because this root domain has a flat DNS namespace, you cannot install an Operations Manager management group into the Woodgrove domain. But, if the Woodgrove domain has a child domain with a DNS name of "National", the fully qualified domain name of the child domain would be national.woodgrove. For more information about configuring Windows for domains with single-label DNS names, see Information about configuring Active Directory domains by using single-label DNS names.

### Domain functional level

Windows Server Active Directory can operate at different functional levels. These levels are distinguished by the version of the Windows Server operating system that is permitted on the domain controllers present in the domain. System Center 2016 – Operations Manager does not have a domain functional level requirement.  

### Forest functional level

The forest functional level is similar to the domain functional level in that it sets a minimum domain controller operating system level across the whole forest. After it is set, domain controllers with down-level operating systems from lower functional levels cannot be introduced into the forest. Operations Manager does not have a forest functional level requirement.

### DNS

DNS must be installed and in a healthy state to support AD DS. Beyond the reliance of Operations Manager on AD DS, there are no specific DNS requirements.
