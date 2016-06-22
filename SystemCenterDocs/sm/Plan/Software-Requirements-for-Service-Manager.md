---
title: Software Requirements for Service Manager
ms.custom: na
ms.prod: system-center-threshold
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f864d8f1-7acf-4aa7-a810-50e272f7e25f
---
# Software Requirements for Service Manager
This topic describes the software requirements for System Center 2016 Technical Preview \- Service Manager. Where applicable to a specific version, items are noted accordingly.

## Software Requirements
The software requirements for System Center 2016 Technical Preview \- Service Manager are listed below.

> [!NOTE]
> The System Center 2016 Technical Preview \- Service Manager management server and data warehouse management server must be installed on the 64\-bit edition of the Windows operating system. The Service Manager console can be installed on both the 32\-bit and 64\-bit editions of Windows.

### Software requirements table

|||
|-|-|
|System Center 2016 Technical Preview \- Service Manager management server|In addition to the [System Requirements for System Center 2012 R2](http://go.microsoft.com/fwlink/p/?LinkId=309285), the System Center 2016 Technical Preview \- Service Manager management server  requires:<br /><br />-   ADO.NET Data Services Update for .NET Framework 3.5 SP1 for Windows Server 2008 R2<br />-   SQL Server 2008 R2 Native Client or SQL Server 2012 Native client<br />-   Microsoft Report Viewer Redistributable, which is available with the System Center 2016 Technical Preview \- Service Manager media. For more information, see How to Install the Microsoft Report Viewer Redistributable Security Update in the [Deployment Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209670).|
|Data warehouse management server|In addition to the [System Requirements for System Center 2012 R2](http://go.microsoft.com/fwlink/p/?LinkId=309285), the data warehouse management server requires:<br /><br />-   SQL Server 2008 R2 Native Client or SQL Server 2012 Native client|
|System Center 2016 Technical Preview \- Service Manager or data warehouse databases|In addition to the [System Requirements for System Center 2012 R2](http://go.microsoft.com/fwlink/p/?LinkId=309285), the System Center 2016 Technical Preview \- Service Manager or data warehouse databases require:<br /><br />-   SQL Server Reporting Services \(SSRS\)<br />-   The SQL Server and Analysis Services collation settings must be the same for the computers hosting the System Center 2016 Technical Preview \- Service Manager database, data warehouse database, analysis services database, and Reporting Services database.<br />-   System Center 2016 Technical Preview \- Service Manager requires SQL Server 2012 Analysis Management Objects, which are part of the SQL Server 2012 Feature Pack, regardless of the SQL Server version that you use.|
|Service Manager console|In addition to the [System Requirements for System Center 2012 R2](http://go.microsoft.com/fwlink/p/?LinkId=309285), the Service Manager console requires:<br /><br />-   Microsoft Report Viewer Redistributable, which is available with the System Center 2016 Technical Preview \- Service Manager media. For more information, see How to Install the Microsoft Report Viewer Redistributable Security Update in the [Deployment Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209670).<br />-   You must have Microsoft Excel 2007 or later installed in order view OLAP data cubes on the computer running the Service Manager console.<br />-   ADO.NET Data Services Update for .NET Framework 3.5 SP1 for Windows Server 2008 R2. \*<br />-   System Center 2016 Technical Preview \- Service Manager requires SQL Server 2012 Analysis Management Objects, which are part of the SQL Server 2012 Feature Pack, regardless of the SQL Server version that you use.|
|Self\-Service Portal: Web Content Server|In addition to the [System Requirements for System Center 2012 R2](http://go.microsoft.com/fwlink/p/?LinkId=309285), the Self\-Service Portal Web Content Server requires:<br /><br />-   Microsoft Internet Information Services \(IIS\) 7 with IIS 6 metabase compatibility installed.<br />-   A Secure Sockets Layer \(SSL\) certificate can be used on the IIS server that hosts the Self\-Service Portal.<br />-   System Center 2016 Technical Preview \- Service Manager requires SQL Server 2012 Analysis Management Objects, which are part of the SQL Server 2012 Feature Pack, regardless of the SQL Server version that you use.|
|Self\-Service Portal: SharePoint Web Parts|One of the following versions of Microsoft SharePoint:<br /><br />-   Microsoft SharePoint Foundation 2010<br />-   Microsoft SharePoint Server 2010<br />-   Microsoft SharePoint 2010 for Internet Sites Enterprise<br />-   If your System Center 2016 Technical Preview database uses SQL Server 2012, then you must have Service Pack 1 or later applied to your SharePoint 2010 installation.<br /><br />Software requirements for SharePoint Web Parts for the Self\-Service Portal are based on Microsoft SharePoint Server 2010 specifications. For more information, see [Hardware and Software Requirements (SharePoint Server 2010)](http://go.microsoft.com/fwlink/p/?LinkID=219606).<br /><br />You must install the English language pack in non\-English SharePoint installations so that the Self\-Service Portal installs correctly. **Note:** Windows Server 2012 and Windows Server 2012 R2 are supported on the server hosting the SharePoint Web Parts with SharePoint 2010 SP2.SharePoint 2013 is not supported on the server hosting the SharePoint Web Parts.|
|Excel Services in SharePoint Server 2010|Excel Services in SharePoint Server 2010 is required for hosting dashboards for advanced analytical reports. For more information about installing and configuring Excel Services, see [Configure Excel Services for a BI test environment](http://go.microsoft.com/fwlink/p/?LinkID=227285).|
|Computers accessing the Self\-Service Portal|All Self\-Service Portal web console requirements are listed at [Self-Service Web Console Support](http://go.microsoft.com/fwlink/?LinkId=268327)|
|SQL Server Reporting Services|In a deployment topology where the computer hosting SSRS is not on the same computer that hosts the data warehouse management server, you have to add **Microsoft.EnterpriseManagement.Reporting.Code** to the global assembly cache. For more information, see [Manual Steps to Configure the Remote SQL Server Reporting Services [SP1]](assetId:///d917271d-38e0-4be2-a646-dad908d2e790) in the [Service Manager for System Center 2012 Deployment Guide](http://go.microsoft.com/fwlink/p/?LinkID=209670).|

\* For more information about the ADO.NET Data Service Update, see [ADO.NET Data Services Update for .NET Framework 3.5 SP1 for Windows 7 and Windows Server 2008 R2](http://go.microsoft.com/fwlink/p/?LinkID=224398).

### <a name="BKMK_SQL"></a>Microsoft SQL Server 2008
To download trial software of the English versions of either Microsoft SQL Server 2008 Standard Edition or SQL Server 2008 Enterprise Edition, see [SQL Server 2008](http://go.microsoft.com/fwlink/p/?LinkID=51646).

To download SP1 for SQL Server 2008, see [SQL Server 2008 Service Pack 1](http://go.microsoft.com/fwlink/p/?LinkID=148449).

To download the trial software for the English version of SQL Server 2008 R2, see [SQL Server 2008 R2](http://go.microsoft.com/fwlink/p/?LinkID=208018).

To download Service Pack 1 for Microsoft SQL Server 2008 R2, see [Microsoft® SQL Server® 2008 R2 Service Pack 1](http://go.microsoft.com/fwlink/p/?LinkID=235126)

Use the following configuration with SQL Server 2008 SP1:

-   SQL Server full\-text search: Full\-text search must be selected during installation on the computers running SQL Server that will host the System Center 2016 Technical Preview \- Service Manager and data warehouse databases. For more information about FTS, see [SQL Server 2008 Full-Text Search: Internals and Enhancements](http://go.microsoft.com/fwlink/p/?LinkID=129544).

-   SQL Server configured to use case\-insensitive databases.

-   Service Account configured in accordance with your organization’s requirements.

-   The SQL Server Reporting Services \(MSSQLSERVER\) service, configured and running. For more information about how to configure the MSSQLSERVER service, see [How to: Verify a Reporting Services Installation](http://go.microsoft.com/fwlink/p/?LinkID=91847).

-   For this release, make sure that you use the same collation in SQL Server and Analysis Services on the computers that host the System Center 2016 Technical Preview \- Service Manager database, the data warehouse database, and the analysis services database. For more information about SQL Server collations, see [Using SQL Server Collations](http://go.microsoft.com/fwlink/p/?LinkID=146998).

If your SQL Server installation is using the default collation \(SQL\_Latin1\_General\_CP1\_CI\_AS\), a warning message appears, stating that the collation is not one of the supported collations for System Center 2016 Technical Preview \- Service Manager and that an unsupported collation can cause unpredictable behavior in multilingual environments.

> [!CAUTION]
> Support for languages other than English in System Center 2016 Technical Preview \- Service Manager is not possible when you are using the collation SQL\_Latin1\_General\_CP1\_CI\_AS. If later you decide to support multiple languages using a different collation, you have to reinstall SQL Server. There are no issues with using the SQL\_Latin1\_General\_CP1\_CI\_AS collation with the English\-only installations of System Center 2016 Technical Preview \- Service Manager. SQL\_Latin1\_General\_CP1\_CI\_AS is supported despite the warning message in setup. It is generally used for installations where the Service Manager databases will share a SQL Server instance with other System Center components which must be installed on SQL\_Latin1\_General\_CP1\_CI\_AS.  If Service Manager will be installed on its own SQL Server instance, it is recommended to use the newer and more complete collation Latin1\_General\_100\_CP1\_CI\_AS. For more information about language support, see [Language Support for Service Manager](Language-Support-for-Service-Manager.md).

You can define the collation when you install SQL Server. During Setup, on the **Server Configuration** page, click the **Collation** tab, and then click **Customize** for both the **Database Engine** and **Analysis Services**entries.

### Microsoft SQL Server 2012
To download trial software of the English versions of Microsoft SQL Server 2012, see the [SQL Server 2012 Trial](http://go.microsoft.com/fwlink/p/?LinkID=208018) page on the Microsoft web site.

Other considerations for SQL Server 2012 are similar to SQL Server 2008.

### SQL Server Reporting Services
When you install SSRS, select the option to install the native mode default configuration. For more information, see [Considerations for Installing Reporting Services](http://go.microsoft.com/fwlink/p/?LinkID=163942).

Do not use the same SSRS instance that you are using for System Center 2016 Technical Preview \- Service Manager with any other System Center components.

### SQL Server Analysis Services
SQL Server Analysis Services \(SSAS\) is required for System Center 2016 Technical Preview \- Service Manager.

### <a name="BKMK_NET2"></a>Microsoft .NET Framework 3.5 SP1
Microsoft .NET Framework 3.5 SP1 is required for running System Center 2016 Technical Preview \- Service Manager. Microsoft .NET Framework 3.5 SP1 is included with the System Center 2016 Technical Preview \- Service Manager installation media.

### Microsoft .NET Framework 4
The Self\-Service Portal for System Center 2016 Technical Preview \- Service Manager consists of two parts, a web content server and SharePoint Web Parts. The web content server requires Microsoft .NET Framework 4. To download .NET Framework 4, see [Microsoft .NET Framework 4 (Web Installer)](http://go.microsoft.com/fwlink/p/?LinkID=208148).

### Microsoft SharePoint Server 2010
The Self\-Service Portal for System Center 2016 Technical Preview \- Service Manager consists of two parts, a web content server and a SharePoint website. You must install SharePoint Web Parts on a computer that hosts SharePoint Server 2010. A link to download SharePoint Server 2010 is on the System Center 2016 Technical Preview \- Service Manager Prerequisites page in Setup, or you can download an evaluation copy of SharePoint Server 2010 at [Download Microsoft SharePoint Server 2010](http://go.microsoft.com/fwlink/p/?LinkID=189313).

> [!IMPORTANT]
> You must install the English language pack in non\-English SharePoint installations so that the Self\-Service Portal installs correctly.

### Windows PowerShell 2.0
Windows PowerShell 2.0 is required for System Center 2016 Technical Preview \- Service Manager. You enable Windows PowerShell 2.0 in Windows Server 2008 using System Center 2016 Technical Preview \- Service Manager. For more information see [How to: Enable Windows PowerShell](http://go.microsoft.com/fwlink/p/?LinkId=231856)

### Microsoft SQL Server Analysis Management Objects
System Center 2016 Technical Preview \- Service Manager requires Microsoft SQL Server 2012 Analysis Management Objects \(AMOs\), which are part of the SQL Server 2012 Feature Pack, so that it can work with SSAS. Microsoft AMOs are also required for the web content server \(part of the Self\-Service Portal\). Two different setup files are available for installing Microsoft AMOs, based on the microprocessor architecture that you are using, as indicated in the following list:

-   [SQL Server 2012 Analysis Management Objects X86](http://go.microsoft.com/fwlink/?LinkID=239665)

-   [SQL Server 2012 Analysis Management Objects X64](http://go.microsoft.com/fwlink/?LinkID=239666)

For System Center 2012 only: The Service Manager console requires Microsoft Analysis Management Objects \(AMOs\) so that it can work with SSAS. Microsoft AMOs are also required for the web content server \(part of the Self\-Service Portal\). Three different setup files are available for installing Microsoft AMOs, based on the microprocessor architecture that you are using, as indicated in the following list:

-   [x86 Package](http://go.microsoft.com/fwlink/p/?LinkID=218847)

-   [x64 Package](http://go.microsoft.com/fwlink/p/?LinkID=218910)

-   [IA-64 Package](http://go.microsoft.com/fwlink/p/?LinkID=218912)

### Internet Information Services
When you install the IIS role, you must select the ASP.NET, Basic Authentication, and Windows Authentication options.

### Operations Manager
System Center 2016 Technical Preview \- Service Manager has the capability to import alerts and configuration items from your Operations Manager 2007 environment. You must have Operations Manager 2012, Operations Manager 2007 SP1, or Operations Manager 2007 R2 installed to work with System Center 2016 Technical Preview \- Service Manager.

> [!IMPORTANT]
> You cannot use Operations Manager 2007 SP1 to monitor System Center 2016 Technical Preview \- Service Manager management servers. You must use Operations Manager 2007 R2 or Operations Manager 2012.

You can create a data mart for Operations Manager.

### Configuration Manager
System Center 2016 Technical Preview \- Service Manager can import configuration items from your Configuration Manager environment. You must have Configuration Manager 2007 SP1, Configuration Manager 2007 R2, or Configuration Manager 2012 installed to work with System Center 2016 Technical Preview \- Service Manager.

### Network Requirements
In System Center 2016 Technical Preview \- Service Manager, you can view external content from within knowledge articles. To view external content, computers that host the Service Manager console must have Internet access, either directly or through a proxy server.

### SMTP Server
You must have access to a Simple Mail Transfer Protocol \(SMTP\) server to use the Notification feature and for incident creation through email.

### Windows Safe Mode
System Center 2016 Technical Preview \- Service Manager does not operate and the services used by System Center 2016 Technical Preview \- Service Manager do not start if Windows Server 2008 is running in safe mode. If you attempt to start the System Center 2016 Technical Preview \- Service Manager services manually while in safe mode, the services fail to start and an error is written into the event log.


