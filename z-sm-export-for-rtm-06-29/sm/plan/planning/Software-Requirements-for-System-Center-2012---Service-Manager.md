---
title: Software Requirements for System Center 2012 - Service Manager
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 787b218d-2f31-41e2-a8c7-3365972d029b
translation.priority.ht: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# Software Requirements for System Center 2012 - Service Manager
This topic describes the software requirements for [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] in System Center 2012, [!INCLUDE[sc2012sp1_long](../../../sm/deploy/upgrade/includes/sc2012sp1_long_md.md)], and [!INCLUDE[smblue_1](../../../sm/deploy/deploy-guide/includes/smblue_1_md.md)]. Where applicable to a specific [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] version, items are noted accordingly.  
  
## Software Requirements  
 All software requirements for [!INCLUDE[smblue_1](../../../sm/deploy/deploy-guide/includes/smblue_1_md.md)] are listed at [System Requirements for System Center 2012 R2](http://go.microsoft.com/fwlink/p/?LinkId=309285).  
  
 All software requirements for [!INCLUDE[sc2012sp1_long](../../../sm/deploy/upgrade/includes/sc2012sp1_long_md.md)] are listed at [System Requirements for System Center 2012 SP1](http://go.microsoft.com/fwlink/?LinkId=268322).  
  
 The software requirements for [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] with no service pack are the same as [!INCLUDE[smblue_1](../../../sm/deploy/deploy-guide/includes/smblue_1_md.md)], except that [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] is not supported on [!INCLUDE[win8_server_2](../../../sm/deploy/upgrade/includes/win8_server_2_md.md)] or where noted. Additional requirements and related information is shown in the following table and sections.  
  
> [!NOTE]  
>  The [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server and data warehouse management server must be installed on the 64\-bit edition of the Windows operating system. The [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)] can be installed on both the 32\-bit and 64\-bit editions of Windows.  
>   
>  [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] 2012 with no service pack is supported on SQL Server 2008 R2 without a service pack, however it is not supported with SQL Server 2012. [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] 2012 SP1 and [!INCLUDE[smblue_1](../../../sm/deploy/deploy-guide/includes/smblue_1_md.md)] require SQL Server 2008 R2 SP1 or later.  
  
### Software requirements table  
  
|||  
|-|-|  
|[!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server|In addition to the [System Requirements for System Center 2012 R2](http://go.microsoft.com/fwlink/p/?LinkId=309285), the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management server  requires:<br /><br /> -   ADO.NET Data Services Update for .NET Framework 3.5 SP1 for Windows Server 2008 R2<br />-   SQL Server 2008 R2 Native Client or SQL Server 2012 Native client<br />-   Microsoft Report Viewer Redistributable, which is available with the [!INCLUDE[smshort12](../../../sm/deploy/deploy-guide/includes/smshort12_md.md)] media. For more information, see How to Install the Microsoft Report Viewer Redistributable Security Update in the [Deployment Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209670).|  
|Data warehouse management server|In addition to the [System Requirements for System Center 2012 R2](http://go.microsoft.com/fwlink/p/?LinkId=309285), the data warehouse management server requires:<br /><br /> -   SQL Server 2008 R2 Native Client or SQL Server 2012 Native client|  
|[!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] or data warehouse databases|In addition to the [System Requirements for System Center 2012 R2](http://go.microsoft.com/fwlink/p/?LinkId=309285), the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] or data warehouse databases require:<br /><br /> -   SQL Server Reporting Services \(SSRS\)<br />-   The SQL Server and Analysis Services collation settings must be the same for the computers hosting the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database, data warehouse database, analysis services database, and Reporting Services database.<br />-   For [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] in [!INCLUDE[sc2012](../../../sm/plan/planning/includes/sc2012_md.md)] SP1 and [!INCLUDE[smblue_1](../../../sm/deploy/deploy-guide/includes/smblue_1_md.md)]:  SQL Server 2012 Analysis Management Objects, which are part of the SQL Server 2012 Feature Pack, are required regardless of the SQL Server version that you use<br />-   For System Center 2012 only: SQL Server 2008 R2 Analysis Management Objects|  
|[!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)]|In addition to the [System Requirements for System Center 2012 R2](http://go.microsoft.com/fwlink/p/?LinkId=309285), the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)] requires:<br /><br /> -   Microsoft Report Viewer Redistributable, which is available with the [!INCLUDE[smlong12](../../../sm/deploy/deploy-guide/includes/smlong12_md.md)] media. For more information, see How to Install the Microsoft Report Viewer Redistributable Security Update in the [Deployment Guide for System Center 2012 – Service Manager](http://go.microsoft.com/fwlink/p/?LinkId=209670).<br />-   You must have Microsoft Excel 2007 or later installed in order view OLAP data cubes on the computer running the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)].<br />-   ADO.NET Data Services Update for .NET Framework 3.5 SP1 for Windows Server 2008 R2. \*<br />-   For [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] in [!INCLUDE[sc2012](../../../sm/plan/planning/includes/sc2012_md.md)] SP1 and [!INCLUDE[smblue_1](../../../sm/deploy/deploy-guide/includes/smblue_1_md.md)]: SQL Server 2012 Analysis Management Objects are required regardless of the SQL Server version that you use<br />-   For System Center 2012 only: SQL Server 2008 R2 Analysis Management Objects|  
|[!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)]: Web Content Server|In addition to the [System Requirements for System Center 2012 R2](http://go.microsoft.com/fwlink/p/?LinkId=309285), the [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)] Web Content Server requires:<br /><br /> -   Microsoft Internet Information Services \(IIS\) 7 with IIS 6 metabase compatibility installed.<br />-   A Secure Sockets Layer \(SSL\) certificate can be used on the IIS server that hosts the [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)].<br />-   For [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] in [!INCLUDE[sc2012](../../../sm/plan/planning/includes/sc2012_md.md)] SP1 and [!INCLUDE[smblue_1](../../../sm/deploy/deploy-guide/includes/smblue_1_md.md)]: SQL Server 2012 Analysis Management Objects are required regardless of the SQL Server version that you use<br />-   For System Center 2012 only: SQL Server 2008 R2 Analysis Management Objects|  
|[!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)]: SharePoint Web Parts|One of the following versions of Microsoft SharePoint:<br /><br /> -   Microsoft SharePoint Foundation 2010<br />-   Microsoft SharePoint Server 2010<br />-   Microsoft SharePoint 2010 for Internet Sites Enterprise<br />-   If your [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database uses SQL Server 2012, then you must have Service Pack 1 or later applied to your SharePoint 2010 installation.<br /><br /> Software requirements for SharePoint Web Parts for the [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)] are based on Microsoft SharePoint Server 2010 specifications. For more information, see [Hardware and Software Requirements \(SharePoint Server 2010\)](http://go.microsoft.com/fwlink/p/?LinkID=219606).<br /><br /> You must install the English language pack in non\-English SharePoint installations so that the [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)] installs correctly. **Note:**  [!INCLUDE[win8_server_2](../../../sm/deploy/upgrade/includes/win8_server_2_md.md)] and [!INCLUDE[winblue_server_2](../../../sm/plan/planning/includes/winblue_server_2_md.md)] are supported on the server hosting the SharePoint Web Parts with SharePoint 2010 SP2. SharePoint 2013 is not supported on the server hosting the SharePoint Web Parts.|  
|Excel Services in SharePoint Server 2010|Excel Services in SharePoint Server 2010 is required for hosting dashboards for advanced analytical reports. For more information about installing and configuring Excel Services, see [Configure Excel Services for a BI test environment](http://go.microsoft.com/fwlink/p/?LinkID=227285).|  
|Computers accessing the [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)]|All [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)] web console requirements are listed at [Self\-Service Web Console Support](http://go.microsoft.com/fwlink/?LinkId=268327)|  
|SQL Server Reporting Services|In a deployment topology where the computer hosting SSRS is not on the same computer that hosts the data warehouse management server, you have to add **Microsoft.EnterpriseManagement.Reporting.Code** to the global assembly cache. For more information, see [Manual Steps to Configure the Remote SQL Server Reporting Services &#91;SP1&#93;](assetId:///d917271d-38e0-4be2-a646-dad908d2e790) in the [Service Manager for System Center 2012 Deployment Guide](http://go.microsoft.com/fwlink/p/?LinkID=209670).|  
  
 \* For more information about the ADO.NET Data Service Update, see [ADO.NET Data Services Update for .NET Framework 3.5 SP1 for Windows 7 and Windows Server 2008 R2](http://go.microsoft.com/fwlink/p/?LinkID=224398).  
  
###  <a name="BKMK_SQL"></a> Microsoft SQL Server 2008  
 To download trial software of the English versions of either Microsoft SQL Server 2008 Standard Edition or SQL Server 2008 Enterprise Edition, see [SQL Server 2008](http://go.microsoft.com/fwlink/p/?LinkID=51646).  
  
 To download SP1 for SQL Server 2008, see [SQL Server 2008 Service Pack 1](http://go.microsoft.com/fwlink/p/?LinkID=148449).  
  
 To download the trial software for the English version of SQL Server 2008 R2, see [SQL Server 2008 R2](http://go.microsoft.com/fwlink/p/?LinkID=208018).  
  
 To download Service Pack 1 for Microsoft SQL Server 2008 R2, see [Microsoft® SQL Server® 2008 R2 Service Pack 1](http://go.microsoft.com/fwlink/p/?LinkID=235126)  
  
 Use the following configuration with SQL Server 2008 SP1:  
  
-   SQL Server full\-text search: Full\-text search must be selected during installation on the computers running SQL Server that will host the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] and data warehouse databases. For more information about FTS, see [SQL Server 2008 Full\-Text Search: Internals and Enhancements](http://go.microsoft.com/fwlink/p/?LinkID=129544).  
  
-   SQL Server configured to use case\-insensitive databases.  
  
-   Service Account configured in accordance with your organization’s requirements.  
  
-   The SQL Server Reporting Services \(MSSQLSERVER\) service, configured and running. For more information about how to configure the MSSQLSERVER service, see [How to: Verify a Reporting Services Installation](http://go.microsoft.com/fwlink/p/?LinkID=91847).  
  
-   For this release, make sure that you use the same collation in SQL Server and Analysis Services on the computers that host the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] database, the data warehouse database, and the analysis services database. For more information about SQL Server collations, see [Using SQL Server Collations](http://go.microsoft.com/fwlink/p/?LinkID=146998).  
  
 If your SQL Server installation is using the default collation \(SQL\_Latin1\_General\_CP1\_CI\_AS\), a warning message appears, stating that the collation is not one of the supported collations for [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] and that an unsupported collation can cause unpredictable behavior in multilingual environments.  
  
> [!CAUTION]  
>  Support for languages other than English in [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] is not possible when you are using the collation SQL\_Latin1\_General\_CP1\_CI\_AS. If later you decide to support multiple languages using a different collation, you have to reinstall SQL Server. There are no issues with using the SQL\_Latin1\_General\_CP1\_CI\_AS collation with the English\-only installations of [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)]. SQL\_Latin1\_General\_CP1\_CI\_AS is supported despite the warning message in setup. It is generally used for installations where the Service Manager databases will share a SQL Server instance with other System Center components which must be installed on SQL\_Latin1\_General\_CP1\_CI\_AS.  If Service Manager will be installed on its own SQL Server instance, it is recommended to use the newer and more complete collation Latin1\_General\_100\_CP1\_CI\_AS. For more information about language support, see [Language Support for System Center 2012 \- Service Manager](../../../sm/plan/planning/Language-Support-for-System-Center-2012---Service-Manager.md).  
  
 You can define the collation when you install SQL Server. During Setup, on the **Server Configuration** page, click the **Collation** tab, and then click **Customize** for both the **Database Engine** and **Analysis Services**entries.  
  
### Microsoft SQL Server 2012  
 To download trial software of the English versions of Microsoft SQL Server 2012, see the [SQL Server 2012 Trial](http://go.microsoft.com/fwlink/p/?LinkID=208018) page on the Microsoft web site.  
  
 Other considerations for SQL Server 2012 are similar to SQL Server 2008. [!INCLUDE[crabout](../../../sm/deploy/deploy-guide/includes/crabout_md.md)] SQL Server, see [Microsoft SQL Server 2008](../../../sm/plan/planning/Software-Requirements-for-System-Center-2012---Service-Manager.md#BKMK_SQL).  
  
### SQL Server Reporting Services  
 When you install SSRS, select the option to install the native mode default configuration. For more information, see [Considerations for Installing Reporting Services](http://go.microsoft.com/fwlink/p/?LinkID=163942).  
  
 Do not use the same SSRS instance that you are using for [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] with any other System Center components.  
  
### SQL Server Analysis Services  
 SQL Server Analysis Services \(SSAS\) is required for [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)].  
  
###  <a name="BKMK_NET2"></a> Microsoft .NET Framework 3.5 SP1  
 Microsoft .NET Framework 3.5 SP1 is required for running [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)]. Microsoft .NET Framework 3.5 SP1 is included with the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] installation media.  
  
### Microsoft .NET Framework 4  
 The [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)] for [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] consists of two parts, a web content server and SharePoint Web Parts. The web content server requires Microsoft .NET Framework 4. To download .NET Framework 4, see [Microsoft .NET Framework 4 \(Web Installer\)](http://go.microsoft.com/fwlink/p/?LinkID=208148).  
  
### Microsoft SharePoint Server 2010  
 The [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)] for [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] consists of two parts, a web content server and a SharePoint website. You must install SharePoint Web Parts on a computer that hosts SharePoint Server 2010. A link to download SharePoint Server 2010 is on the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] Prerequisites page in Setup, or you can download an evaluation copy of SharePoint Server 2010 at [Download Microsoft SharePoint Server 2010](http://go.microsoft.com/fwlink/p/?LinkID=189313).  
  
> [!IMPORTANT]  
>  You must install the English language pack in non\-English SharePoint installations so that the [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)] installs correctly.  
  
### Windows PowerShell 2.0  
 Windows PowerShell 2.0 is required for [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)]. You enable Windows PowerShell 2.0 in Windows Server 2008 using [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)]. For more information see [How to: Enable Windows PowerShell](http://go.microsoft.com/fwlink/p/?LinkId=231856)  
  
### Microsoft SQL Server Analysis Management Objects  
 For [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] in [!INCLUDE[sc2012](../../../sm/plan/planning/includes/sc2012_md.md)] SP1 and [!INCLUDE[smblue_1](../../../sm/deploy/deploy-guide/includes/smblue_1_md.md)]: The [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)] requires Microsoft SQL Server 2012 Analysis Management Objects \(AMOs\), which are part of the SQL Server 2012 Feature Pack, so that it can work with SSAS. Microsoft AMOs are also required for the web content server \(part of the [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)]\). Two different setup files are available for installing Microsoft AMOs, based on the microprocessor architecture that you are using, as indicated in the following list:  
  
-   [SQL Server 2012 Analysis Management Objects X86](http://go.microsoft.com/fwlink/?LinkID=239665)  
  
-   [SQL Server 2012 Analysis Management Objects X64](http://go.microsoft.com/fwlink/?LinkID=239666)  
  
 For System Center 2012 only: The [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)] requires Microsoft Analysis Management Objects \(AMOs\) so that it can work with SSAS. Microsoft AMOs are also required for the web content server \(part of the [!INCLUDE[smssp](../../../sm/deploy/deploy-guide/includes/smssp_md.md)]\). Three different setup files are available for installing Microsoft AMOs, based on the microprocessor architecture that you are using, as indicated in the following list:  
  
-   [x86 Package](http://go.microsoft.com/fwlink/p/?LinkID=218847)  
  
-   [x64 Package](http://go.microsoft.com/fwlink/p/?LinkID=218910)  
  
-   [IA\-64 Package](http://go.microsoft.com/fwlink/p/?LinkID=218912)  
  
### Internet Information Services  
 When you install the IIS role, you must select the ASP.NET, Basic Authentication, and Windows Authentication options.  
  
### Operations Manager  
 [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] has the capability to import alerts and configuration items from your Operations Manager 2007 environment. You must have Operations Manager 2012, Operations Manager 2007 SP1, or Operations Manager 2007 R2 installed to work with [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)].  
  
> [!IMPORTANT]  
>  You cannot use Operations Manager 2007 SP1 to monitor [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] management servers. You must use Operations Manager 2007 R2 or Operations Manager 2012.  
  
 If you plan to install both [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] and Operations Manager 2007 in the same environment, see [Operations Manager Considerations in System Center 2012 \- Service Manager](../../../sm/plan/planning/Operations-Manager-Considerations-in-System-Center-2012---Service-Manager.md).  
  
 You can create a data mart for Operations Manager.  
  
### Configuration Manager  
 [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] can import configuration items from your [!INCLUDE[sccmlongname](../../../sm/plan/planning/includes/sccmlongname_md.md)] environment. You must have Configuration Manager 2007 SP1, Configuration Manager 2007 R2, or Configuration Manager 2012 installed to work with [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)].  
  
### Network Requirements  
 In [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)], you can view external content from within knowledge articles. To view external content, computers that host the [!INCLUDE[smcons](../../../sm/deploy/deploy-guide/includes/smcons_md.md)] must have Internet access, either directly or through a proxy server.  
  
### SMTP Server  
 You must have access to a Simple Mail Transfer Protocol \(SMTP\) server to use the Notification feature and for incident creation through email.  
  
### Windows Safe Mode  
 [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] does not operate and the services used by [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] do not start if Windows Server 2008 is running in safe mode. If you attempt to start the [!INCLUDE[smshort](../../../sm/deploy/deploy-guide/includes/smshort_md.md)] services manually while in safe mode, the services fail to start and an error is written into the event log.  
  
## See Also  
 [Supported Configurations for System Center 2012 \- Service Manager](../../../sm/plan/planning/Supported-Configurations-for-System-Center-2012---Service-Manager.md)