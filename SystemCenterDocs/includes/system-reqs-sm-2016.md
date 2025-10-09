---
title: include file
description: include file to describe the system requirements for Service Manager 2016.
ms.service: system-center
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 10/08/2021
ms.subservice: service-manager
ms.topic: include
ms.assetid: ff4c7819-632e-486f-a329-041b7fa6a478

---

## System requirements for System Center 2016 - Service Manager

The following sections describe the general performance and scalability guidance for SM 2016, and recommend the  hardware configurations for various workloads. Because System Center 2016 is built to be flexible and scalable, the hardware requirements for specific scenarios may differ from the guidelines that are presented here.  

## Capacity limits for Service Manager

[Learn about](../scsm/deploy-topo-scenarios.md) the tested capacity limits for various Service Manager deployment scenarios.

## Supported coexistence

To help simplify upgrades, you can use the following Service Manager 2016 connectors with System Center 2012 R2 components.

- System Center 2012 R2 Virtual Machine manager
- System Center 2012 R2 Orchestrator
- System Center 2012 R2 Operations Manager
- System Center 2012 R2 Configuration Manager
- System Center Configuration Manager (SCCM) CB releases - 1511, 1602, 1606, and 1710.
    - UR5 supports 1802
    - UR9 and UR10 supports from 1806 to 2103. However, there's a limitation that the size of the devices supported by SCCM should be less than 2 PB.
    - UR10 supports 2107


## Hardware

|Server |Processor (min)|Processor (rec)|RAM (min)|RAM (rec)|Hard drive space (min)|Hard drive space (rec)|
|---------------------------------|---------------------|---------------------|---------------|---------------|----------------------------|----------------------------|
|**Service Manager** Management Server|4-Core 2.66 GHz CPU|4-Core 2.66 GHz CPU|8 GB|8 GB|10 GB|10 GB|
|**Service Manager** Database|8-Core 2.66 GHz CPU|8-Core 2.66 GHz CPU|8 GB|32 GB|80 GB|80 GB|
|**Service Manager** Data Warehouse Management Server|4-Core 2.66 GHz CPU|4-Core 2.66 GHz CPU|8 GB|16 GB|10 GB|10 GB|
|**Service Manager** Data Warehouse Databases|8-Core 2.66 GHz CPU|8-Core 2.66 GHz CPU|8 GB|32 GB|400 GB|400 GB|
|**Service Manager** Console|2-Core 2 GHz CPU|2-Core 2 GHz CPU|4 GB|4 GB|10 GB|10 GB|
|**Service Manager** Self-Service Portal (standalone)|4-Core 2.66 GHz CPU|8-Core 2.66 GHz CPU|8 GB|16 GB|80 GB|80 GB|
|**Service Manager** Self-Service Portal + Secondary Management Server (Recommended)|8-Core 2.66 GHz CPU|8-Core 2.66 GHz CPU|16 GB|32 GB|80 GB|80 GB|

## Server operating system

The following versions of Windows Server operating system are supported.

|System Center  component|Windows Server 2012 Standard, Datacenter|Windows Server 2012 R2 Standard, Datacenter|Windows Server 2016|Windows Server 2016 (Server with Desktop Experience)|Windows Server 2016 Nano Server|
|----------------------------|-----------------------|---------------------------|--------------------------|------------------------------|--------------------------------------------------------------------------------|
|**Service Manager** Management Server||&#8226;|&#8226;|&#8226;||
|**Service Manager** Data Warehouse Management Server||&#8226;|&#8226;|&#8226;||
|**Service Manager** Database or Data Warehouse Database||&#8226;|&#8226;|&#8226;||
|**Service Manager** Self-Service Portal (HTML 5)||&#8226;|&#8226;|&#8226;|&nbsp;|



## Client operating system

The following versions of Windows client operating system are supported for the Service Manager console.

|System Center client-side components|Windows&reg; 7|Windows&reg; 8|Windows&reg; 8.1|Windows Server&reg; 2008 R2 SP1|Windows Server&reg; 2012|Windows Server&reg; 2012 R2 Standard, Datacenter|Windows 10 Enterprise|Windows Server&reg; 2016 Standard, Datacenter|
|-----------------------------------------|-------------------------------------------------------------------|-----------------------------------------------------------|-----------------------------------------------------------------|-----------------------------------------------------------------------|-----------------------------------------------------------|--------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------|
|**Service Manager** Console|&#8226;|&#8226;|&#8226;|||&#8226;|&#8226;|&#8226;|


## .NET versions

The following versions of .NET are supported for Service Manager.

|System Center 2016 component|.NET 3.5 SP1|.NET 4|.NET 4.5|.NET 4.5.1|.NET 4.5.2|.NET 4.6|.NET 4.6.1|.NET 4.7|
|-----------------------------------|----------------|----------|------------|--------------|--------------|------------|-------|------|
|**Service Manager** Management Server|&#8226;| | |&#8226;| |&#8226; |&#8226;|&#8226; |
|**Service Manager** Data Warehouse Management Server|&#8226;| | |&#8226;| | &#8226;|&#8226;|&#8226; |
|**Service Manager** console|&#8226;| | |&#8226;| |&#8226; |&#8226;|&#8226; |
|**Service Manager** Self\-Service Portal|&#8226;| | |&#8226;| | &#8226; |&#8226;|&#8226; |

## PowerShell Versions supported

The following versions of PowerShell are supported for Service Manager.

|System Center Component|Windows PowerShell 2.0|Windows PowerShell 3.0|Windows PowerShell 4.0|Windows PowerShell 5.0|
|---------------------------|--------------------------|--------------------------|-----------------------------------------------|-----------------------------------------------|
|**Service Manager** Console|||&#8226;|&#8226;|
|**Service Manager** Management Server|||&#8226;|&#8226;|
|**Service Manager** Data Warehouse Management Server|||&#8226;|&#8226;|


## Software requirements

|                  Component                   |                                                                                                                                                                                     Requirement                                                                                                                                                                                      |
|----------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    **Service Manager management server**     |        The management server needs: [ADO.NET Data Services Update for .NET Framework 3.5](https://www.microsoft.com/download/details.aspx?id=25150) SP1 for Windows Server; SQL Server Native client; Microsoft Report Viewer Redistributable, which is available with the Service Manager media.<br/><br/> The management server must be installed on a 64\-bit edition of Windows.         |
|     **Data warehouse management server**     |                                                                                                         The warehouse management server requires: SQL Server Native client<br/><br/> The data warehouse management server must be installed on a 64\-bit edition of Windows.                                                                                                         |
| **Service Manager/data warehouse databases** |      The Service Manager or data warehouse databases require:  SQL Server Reporting Services \(SSRS\); SQL Server Analysis Management Objects.<br/><br/> The SQL Server and Analysis Services collation settings must be the same for the computers hosting the Service Manager database, data warehouse database, analysis services database, and Reporting Services database.      |
|         **Service Manager console**          | The console requires: Microsoft Report Viewer Redistributable (available on System Center media): Microsoft Excel in order view OLAP data cubes on the console computer;  ADO.NET Data Services Update for .NET Framework 3.5 SP1 for Windows Server; SQL Server Analysis Management Objects<br/><br/> The console can be installed on both 32\-bit and 64\-bit editions of Windows. |
|           **Self-Service portal**            |                                     The Self-Service Portal server requires: Windows 2012 R2 server or later; the IIS role and ASP.NET 4.5 enabled; SQL Server Analysis Management Objects<br/><br/>  Join the server machine to the same domain where the Service Manager SDK Service is running. Ideally, on the primary or secondary server.                                      |
|         Machines using self-service          |                                                                                  The Self Service portal needs a screen resolution above 1024 X 768.<br/><br/> Supported browsers: Microsoft Edge; Microsoft Internet Explorer 10 and 11; Mozilla Firefox 42 and later; Google Chrome 46 and later                                                                                   |
|      **SQL Server Reporting Services**       |                                         In a deployment topology where the computer hosting SSRS isn't on the same computer that hosts the data warehouse management server, you've to add **Microsoft.EnterpriseManagement.Reporting.Code** to the global assembly cache. [Learn about](../scsm/config-remote-ssrs.md) the manual steps.                                         |
|            **Operations Manager**            |                                     Service Manager has the capability to import alerts and configuration items from an Operations Manager environment. [Read about](../scsm/om-considerations.md) installing both Service Manager and Operations Manager in the same environment.<br/><br/> You can create a data mart for Operations Manager.                                      |
|          **Configuration Manager**           |                                                                                                                                       Service Manager can import configuration items from a Configuration Manager environment.                                                                                                                                       |
|           **Network requirements**           |                                                                                                    To view external content from within knowledge articles, computers that host the Service Manager console must have Internet access, either directly or through a proxy server.                                                                                                    |
|               **SMTP server**                |                                                                                                                   You must have access to a Simple Mail Transfer Protocol \(SMTP\) server to use the Notification feature and for incident creation through email.                                                                                                                   |
|            **Windows safe mode**             |                                              Service Manager doesn't operate and the services used by Service Manager don't start if Windows Server is running in safe mode. If you attempt to start the Service Manager services manually while in safe mode, the services fail to start and an error is written into the event log.                                               |

Microsoft SQL Server hosts the databases that System Center 2016 - Service Manager creates. In addition, System Center 2016 - Service Manager requires SQL Server Analysis Services (SSAS) to work with Microsoft Online Analytical Processing (OLAP) cubes. SQL Server Reporting Services (SSRS) is required to support System Center 2016 - Service Manager reporting.

Use this information to evaluate if your SQL Server environment is ready to support the installation of or upgrade to System Center 2016. Use this information whether you're deploying one or multiple components of System Center.

## SQL Server versions

The following table summarizes the support for SQL Server 64-bit Enterprise and Standard versions.

> [!NOTE]
> For the supported versions of SQL, use the service packs that are currently in support by Microsoft.


**Service Manager** | **SQL Server 2012** | **SQL Server 2014 and [SPs](/lifecycle/products/?terms=SQL+Server+2014)**  | **SQL Server 2016 and [SPs](/lifecycle/products/?terms=SQL+Server+2016)**
--- | --- | --- | ---
**Service Manager/Data Warehouse database** | | &#8226;| &#8226;



- System Center 2016 - Service Manager doesn't support setting the MultiSubnetFailover parameter. This parameter isn't used in Service Manager connection strings.
- SQL Server AlwaysOn Availability Groups are supported in System Center 2016 - Service Manager. [Learn more](../scsm/sql-always-on.md).
- To install or upgrade Service Manager, SQL Server machines that host databases must be configured to allow updates. Otherwise, an error appears when Service Manager tries to create a database:
    - *An error occurred while executing a customer action: _ExecuteSqlScripts. This upgrade attempt has failed before permanent modifications were made. Upgrade has successfully rolled back to the original state of the system. Once the corrections are made, you can retry upgrade for this role.*
    - You can check the status of **allow updates** on SQL Server by executing the following stored procedure from within SQL Server Management Studio:
        ```
        sp_configure 'allow updates'
        ```
        In the results table, examine the value for "run_value". If the value of "run value" is 1, set it back to 0 with the following stored procedure, and then run Setup again.

        ```
        sp_configure 'allow updates',0 reconfigure with override
        ```
