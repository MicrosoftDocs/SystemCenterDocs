---
title: Software Requirements for System Center 2016 - Service Manager
description: The article describes System Center 2016 - Service Manager software requirements.
ms.custom: engagement-fy23, UpdateFrequency.5
ms.service: system-center
author: jyothisuri
ms.author: jsuri
ms.date: 11/01/2024
ms.reviewer: na
ms.suite: na
ms.subservice: service-manager
ms.tgt_pltfrm: na
ms.topic: concept-article
ms.assetid: 787b218d-2f31-41e2-a8c7-3365972d029b
monikerRange: 'sc-sm-2016'
---

# Software Requirements for System Center 2016 - Service Manager

This article describes the software requirements for Service Manager in System Center 2016 - Service Manager.

## Software requirements

 All the basic software requirements for System Center 2016 Service Manager are listed in [System requirements for Service Manager](system-requirements.md).  

> [!NOTE]  
> The Service Manager management server and data warehouse management server must be installed on the 64\-bit edition of the Windows operating system. The Service Manager console can be installed on both the 32\-bit and 64\-bit editions of Windows.  

### Software requirements table  

|Service Manager component| requirement|  
|---|---|  
|Service Manager management server|In addition to the [System Requirements for System Center 2016](system-requirements.md), the Service Manager management server  requires:<br /><br /> -   ADO.NET Data Services Update for .NET Framework 3.5 SP1 for Windows Server<br />-   SQL Server Native client<br />-   Microsoft Report Viewer Redistributable, which is available with the Service Manager media.|  
|Data warehouse management server|In addition to the [System Requirements for System Center 2016](system-requirements.md), the data warehouse management server requires:<br /><br /> -   SQL Server Native client|  
|Service Manager or data warehouse databases|In addition to the [System Requirements for System Center 2016](system-requirements.md), the Service Manager or data warehouse databases require:<br /><br /> -   SQL Server Reporting Services \(SSRS\)<br />-   The SQL Server and Analysis Services collation settings must be the same for the computers hosting the Service Manager database, data warehouse database, analysis services database, and Reporting Services database.<br />-   SQL Server Analysis Management Objects.|  
|Service Manager console|In addition to the [System Requirements for System Center 2016](system-requirements.md), the Service Manager console requires:<br /><br /> -   Microsoft Report Viewer Redistributable, which is available with the System Center 2016 - Service Manager media.<br />-   You must have Microsoft Excel 2007 or later installed to view OLAP data cubes on the computer running the Service Manager console.<br />-   ADO.NET Data Services Update for .NET Framework 3.5 SP1 for Windows Server. \*<br />-   SQL Server Analysis Management Objects|  
|Self-Service Portal|In addition to the [System Requirements for System Center 2016](system-requirements.md), the Self-Service Portal server requires:<br /><br /> -   Windows 2012 R2 server or Windows Server 2016 <br> - Join the server machine to the same domain where the Service Manager SDK Service is running. Ideally, on the primary or secondary server. <br> - Enable the IIS role and ASP.NET 4.5 <br> - SQL Server Analysis Management Objects <br>|  
|Computers accessing the Self-Service Portal|The Self Service portal needs a screen resolution above 1024 X 768. It's supported on the following browsers. <br> - Microsoft Edge <br> - Microsoft Internet Explorer 10 and 11 <br> - Mozilla Firefox 42 and later <br> -Google Chrome 46 and later|  
|SQL Server Reporting Services|In a deployment topology where the computer hosting SSRS isn't on the same computer that hosts the data warehouse management server, you have to add **Microsoft.EnterpriseManagement.Reporting.Code** to the global assembly cache. For more information, see [Manual Steps to Configure the Remote SQL Server Reporting Services](config-remote-ssrs.md).|  

 \* For more information about the ADO.NET Data Service Update, see [ADO.NET Data Services Update for .NET Framework 3.5](https://support.microsoft.com/topic/description-of-the-ado-net-data-services-update-for-net-framework-3-5-sp1-for-windows-server-2003-windows-xp-windows-vista-and-windows-server-2008-may-7-2010-e525c2b3-249c-7d66-3cb2-c029c786c745).  

### Operations Manager

Service Manager has the capability to import alerts and configuration items from your Operations Manager environment.

If you plan to install both Service Manager and Operations Manager in the same environment, see [Operations Manager Considerations in System Center 2016 \- Service Manager](om-considerations.md).  

You can create a data mart for Operations Manager.  

### Configuration Manager

Service Manager can import configuration items from your Configuration Manager environment.

### Network requirements

In Service Manager, you can view external content from within knowledge articles. To view external content, computers that host the Service Manager console must have Internet access, either directly or through a proxy server.  

### SMTP server

You must have access to a Simple Mail Transfer Protocol \(SMTP\) server to use the Notification feature and for incident creation through email.  

### Windows safe mode

Service Manager doesn't operate and the services used by Service Manager don't start if Windows Server is running in safe mode. If you attempt to start the Service Manager services manually while in safe mode, the services fail to start and an error is written into the event log.  

## Next steps

- Review [SQL Server requirements](sm-sql-reqs.md) to evaluate if your SQL Server environment is ready to support the installation of or upgrade to System Center 2016 - Service Manager.
