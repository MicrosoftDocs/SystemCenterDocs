---
title: Software Requirements for Service Manager
manager: carmonm
description: The article describes System Center 2016 - Service Manager software requirements.
ms.custom: na
ms.prod: system-center-2016
author: bandersmsft
ms.author: banders
ms.date: 10/12/2016
ms.reviewer: na
ms.suite: na
ms.technology: service-manager
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 787b218d-2f31-41e2-a8c7-3365972d029b
---

# Software Requirements for System Center 2016 - Service Manager

>Applies To: System Center 2016 - Service Manager

This article describes the software requirements for Service Manager in System Center 2016 - Service Manager.

## Software requirements

 All basic software requirements for System Center 2016 Service Manager are listed at [System requirements for Service Manager](../orchestrator/system-requirements.md).  

> [!NOTE]  
>  The Service Manager management server and data warehouse management server must be installed on the 64\-bit edition of the Windows operating system. The Service Manager console can be installed on both the 32\-bit and 64\-bit editions of Windows.  


### Software requirements table  

|Service Manager component| requirement|  
|---|---|  
|Service Manager management server|In addition to the [System Requirements for System Center 2016](../plan/../orchestrator/system-requirements.md), the Service Manager management server  requires:<br /><br /> -   ADO.NET Data Services Update for .NET Framework 3.5 SP1 for Windows Server<br />-   SQL Server Native client<br />-   Microsoft Report Viewer Redistributable, which is available with the Service Manager media.|  
|Data warehouse management server|In addition to the [System Requirements for System Center 2016](../plan/../orchestrator/system-requirements.md), the data warehouse management server requires:<br /><br /> -   SQL Server Native client|  
|Service Manager or data warehouse databases|In addition to the [System Requirements for System Center 2016](../plan/../orchestrator/system-requirements.md), the Service Manager or data warehouse databases require:<br /><br /> -   SQL Server Reporting Services \(SSRS\)<br />-   The SQL Server and Analysis Services collation settings must be the same for the computers hosting the Service Manager database, data warehouse database, analysis services database, and Reporting Services database.<br />-   SQL Server Analysis Management Objects.|  
|Service Manager console|In addition to the [System Requirements for System Center 2016](../plan/../orchestrator/system-requirements.md), the Service Manager console requires:<br /><br /> -   Microsoft Report Viewer Redistributable, which is available with the System Center 2016 - Service Manager media.<br />-   You must have Microsoft Excel 2007 or later installed in order view OLAP data cubes on the computer running the Service Manager console.<br />-   ADO.NET Data Services Update for .NET Framework 3.5 SP1 for Windows Server. \*<br />-   SQL Server Analysis Management Objects|  
|Self-Service Portal|In addition to the [System Requirements for System Center 2016](../plan/../orchestrator/system-requirements.md), the Self-Service Portal server requires:<br /><br /> -   Windows 2012 R2 server or Windows Server 2016 <br> - Join the server machine to the same domain where the Service Manager SDK Service is running. Ideally, on the primary or secondary server. <br> - Enable the IIS role and ASP.NET 4.5 <br> - SQL Server Analysis Management Objects <br>|  
|Computers accessing the Self-Service Portal|The Self Service portal needs a screen resolution above 1024 X 768. It is supported on the following browsers. <br> - Microsoft Edge <br> - Microsoft Internet Explorer 10 and 11 <br> - Mozilla Firefox 42 and later <br> -Google Chrome 46 and later|  
|SQL Server Reporting Services|In a deployment topology where the computer hosting SSRS is not on the same computer that hosts the data warehouse management server, you have to add **Microsoft.EnterpriseManagement.Reporting.Code** to the global assembly cache. For more information, see [Manual Steps to Configure the Remote SQL Server Reporting Services](config-remote-ssrs.md).|  

 \* For more information about the ADO.NET Data Service Update, see [ADO.NET Data Services Update for .NET Framework 3.5](https://go.microsoft.com/fwlink/p/?LinkID=224398).  


### Operations Manager

Service Manager has the capability to import alerts and configuration items from your Operations Manager environment.

If you plan to install both Service Manager and Operations Manager in the same environment, see [Operations Manager Considerations in System Center 2016 \- Service Manager](om-considerations.md).  

You can create a data mart for Operations Manager.  

### Configuration Manager

Service Manager can import configuration items from your Microsoft System Center Configuration Manager environment.

### Network requirements

In Service Manager, you can view external content from within knowledge articles. To view external content, computers that host the Service Manager console must have Internet access, either directly or through a proxy server.  

### SMTP server

You must have access to a Simple Mail Transfer Protocol \(SMTP\) server to use the Notification feature and for incident creation through email.  

### Windows safe mode

Service Manager does not operate and the services used by Service Manager do not start if Windows Server is running in safe mode. If you attempt to start the Service Manager services manually while in safe mode, the services fail to start and an error is written into the event log.  

## Next steps

- Review [SQL Server requirements](sm-sql-reqs.md) to evaluate if your SQL Server environment is ready to support the installation of or upgrade to System Center 2016 - Service Manager.
