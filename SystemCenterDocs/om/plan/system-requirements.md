---
ms.assetid: 1921b7dc-6537-4378-bdc5-de5fbd3e619a
title: System Requirements for System Center 2016 - Operations Manager
description: The system requirements article provides general performance and scalability guidance for consideration as part of your design planning of Operations Manager 2016.  
author: mgoedtel
manager: cfreemanwa
ms.date: 2016-10-13
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---


# System Requirements for System Center 2016 - Operations Manager

>Applies To: System Center 2016 - Operations Manager

The topic describes general performance and scalability guidance for System Center 2016 - Operations Manager and recommends hardware configurations for a variety of workloads. Because System Center 2016 – Operations Manager is built to be flexible and scalable, the hardware requirements for specific scenarios may differ from the guidelines that are presented here.  A discussion of the factors that affect the performance of each Operations Manager component is detailed in other sections of the planning guide so that they can be adapted to specific requirements.

Let's start first by understanding the performance and scalability characteristics of the various Operations Manager components. 

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
| URLs monitored per agent | 500 |


## Hardware

Use this information to evaluate if your hardware environment is ready to support the installation of or upgrade to System Center 2016 - Operations Manager, considering the minimum hardware requirements for processor, RAM, and disk space.  You should use the information here whether you are deploying one or multiple components and for more specific information to help plan the amount of infrastructure needed for a new Operations Manager deployment, refer to the [Operations Manager 2012 Sizing Helper](http://go.microsoft.com/fwlink/p/?LinkId=231853).

> [!NOTE] 
> While the Operations Manager 2012 Sizing helper has not been updated to reflect the 2016 release of Operations Manager, the information provided is still valid to help you estimate for your design requirements.  However, the number of UNIX/Linux computers per management server, as noted in the **Unix or Linux Monitoring** section is not correct.  The number of UNIX/Linux computers per management server has increased and is noted in the monitored item capacity table earlier.  This will be addressed in an updated release of the sizing helper document.

| Operations Manager Server Role | x64 Processor (min) | Memory (min) | Disk space (min) |
|:--- |:---|:--- |:--- |
| Management Server | 4-Core 2.66 GHz CPU | 8 GB | 10 GB |
| Gateway Server managing up to 2000 agents | 4-Core 2.66 GHz CPU | 8 GB | 10 GB |
| Gateway Server in resource pool managing up to 500 network devices | 8-Core 2.66 GHz CPU | 32 GB | 10 GB |
| Gateway Server in resource pool managing up to 100 UNIX/Linux computers | 4-Core 2.66 GHz CPU | 4 GB RAM | 10 GB |
| Web Console server | 4-Core 2.66 GHz CPU | 8 GB | 10 GB | 
| SQL Server Reporting Services server | 4-Core 2.66 GHz CPU | 8 GB | 10 GB |

## Feature requirements for Operations Manager components

### Server Operating System requirements  

The following versions of Windows Server operating system are supported for the following Operations Manager components.

| Component | Windows Server 2012 R2 Standard, Datacenter | Windows Server 2016 Standard, Datacenter | Windows Server Core 2016 |
|:--- |:---|:--- |:--- |
| **Operations Manager** Management Server | yes | yes | yes |
| **Operations Manager** Gateway Server | yes | yes | |
| **Operations Manager** Web Console | yes | yes | |
| **Operations Manager** ACS Collector | yes | yes | |
| **Operations Manager** Operations console | yes | yes | |


### Client Operating System requirements

The following versions of Windows client operating system are supported for the Operations Manager Operations console.

| Windows 7 | Windows 8 | Windows 8.1 | Windows 10 Enterprise |
|:--- |:---|:--- |:--- |
| yes | yes | yes | yes |

### Microsoft Monitoring Agent Operating System requirements

The following versions of Windows operating system are supported for the Microsoft Monitoring Agent connecting to Operations Manager.

Windows Server 2016, Windows Server 2016 Nano Server, Windows 10, Windows 8 Enterprise, Windows 8 Pro, Windows Embedded POSReady 2009, Windows Embedded Standard 7 Service Pack 1, Windows Server 2003 Service Pack 2, Windows Server 2008 R2, Windows Server 2008 Service Pack 2, Windows Server 2012, Windows XP Professional 64-Bit Edition (Itanium) , Windows XP Service Pack 2, Windows XP Service Pack 3.

- File system: %SYSTEMDRIVE% must be formatted with the NTFS file system.
- Windows PowerShell version: Windows PowerShell version 2.0, or Windows PowerShell version 3.0.
- Microsoft .NET Framework 3.5 or later
  
> [!NOTE] 
> Windows PowerShell is required for local collection of IntelliTrace logs, and to run System Center Operations Manager management packs that use PowerShell scripts.

> Microsoft .NET Framework 3.5 or later is required for local collection of IntelliTrace logs and .NET Application Performance Monitoring.

### Management server/Gateway server requirements

- Operating System: See [Server Operating System requirements](#server-operating-system- requirements)
- Windows PowerShell version: Windows PowerShell version 2.0, or Windows PowerShell version 3.0.
- Windows Remote Management: Windows Remote Management must be enabled for the management server.
- NET Framework 4 or .NET Framework 4.5 is required. 

### Operations Manager console requirements

- Operating System: See [Server Operating System requirements](#server-operating-system- requirements)
- Windows PowerShell version: Windows PowerShell version 2.0, or Windows PowerShell version 3.0.
- Microsoft Report Viewer 2015 runtime.  

    > [!NOTE] 
    > Report Viewer has a dependency on [Microsoft CLR Types for SQL Server 2014](https://www.microsoft.com/download/details.aspx?id=42295).  The SQL Server System CLR Types package contains the components implementing the geometry, geography, and hierarchy ID types in SQL Server 2014. This component can be installed separately from the server to allow client applications to use these types outside of the server. 

- NET Framework 4 or .NET Framework 4.5 is required. 

### Web console requirements

- Operating System: See [Server Operating System requirements](#server-operating-system- requirements)
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

- Operating System: See [Server Operating System requirements](#server-operating-system- requirements).
- Microsoft SQL Server: See [SQL Server Requirements](planning-sqlserver-design.md#sql-server-requirements).
- Remote Registry Service: Must be enabled and started.
- Microsoft SQL Server Reporting Services: See [SQL Server Requirements](planning-sqlserver-design.md#sql-server-requirements). 

    > [!NOTE] 
    > System Center 2016 – Operations Manager supports SQL Server Reporting Services in native mode only; do not use SharePoint integrated mode.  

- NET Framework 4 or .NET Framework 4.5 is required. 

## Virtualization

Microsoft supports running all System Center 2016 – Operations Manager server features in any physical or virtual environment that meets the minimum requirements that are stated in this  document.  There are some restrictions on virtualization functionality that is applicable to Operations Manager.  Specifically, Microsoft does not support the use of the following virtualization functionality no matter what virtualization technology is used with Operations Manager: 
- Virtual computers running any Operations Manager 2016 component must not make use of any functionality where all activity on the virtual computer is not immediately committed to the virtual hard drive.  This includes making use of point-in-time snapshots, and writing changes to a temporary virtual hard drive. 
- Virtual computers running any Operations Manager 2016 component cannot be paused or placed into a ‘save state’ status and restarted.  They can only be shut down and restarted just as would be done with a physical computer. 
- Virtual computers that are running any Operations Manager 2016 components cannot be relocated to another host physical server by using any automated process. 
- If the Operations Manager databases are to be hosted on virtualized SQL Server(s), for performance reasons, we recommend that you store the Operational database and data warehouse database on a directly attached physical hard drive and not on a virtual hard disk.

System Center 2016 - Operations Manager runs on virtual machines in Microsoft Azure just as it does on physical computer systems.  We recommend running Operations Manager on Microsoft Azure virtual machines to monitor other virtual machines or resources hosted in Azure, or monitor instances and workloads hosted on-premise.  You can also run Operations Manager on-premise and monitor Microsoft Azure virtual machines or other resources in Azure.  

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

Operations Manager integrates with Active Directory for authentication, rights assignment, and authorization.  DNS is leveraged for name resolution of the supporting roles in the management group as well as computers, network devices, and other monitored workloads such as web URLs.  For further information regarding what AD and DNS requirements you need to evaluate before deploying Operations Manager in your environment, please review [Active Directory and DNS Planning](planning-adds-dns.md). 
