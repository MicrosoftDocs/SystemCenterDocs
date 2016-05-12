---
title: System Requirements for Service Provider Foundation for System Center 2012 SP1
ms.custom: na
ms.prod: system-center-2012-sp1
ms.reviewer: na
ms.suite: na
ms.technology: 
  - service-provider-foundation
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7329a502-7fd0-4f4f-bebe-cc558589c086
---
# System Requirements for Service Provider Foundation for System Center 2012 SP1
The following tables describe the prerequisites for installing [!INCLUDE[spflong](Token/spflong_md.md)] for [!INCLUDE[sc2012sp1_long](Token/sc2012sp1_long_md.md)], the first release of [!INCLUDE[spfshort](Token/spfshort_md.md)]. For requirements for the current version, see [System Requirements for Service Provider Foundation for System Center 2012 R2](assetId:///f7c87718-29bb-4fdd-8e2d-82c81936b346). For System Center 2012 R2 requirements, see [Preparing your environment for System Center 2012 R2 Service Provider Foundation](assetId:///f7c87718-29bb-4fdd-8e2d-82c81936b346).

For information on capacity planning for database storage, memory, and core processors, see [Capacity Planning for Service Provider Foundation](Capacity-Planning-for-Service-Provider-Foundation.md).

### Required hardware and settings

|Hardware|Minimum required and recommended values, per web service|
|------------|------------------------------------------------------------|
|RAM|2 gigabytes \(GB\) minimum, 4 GB preferred.|
|Available hard disk space|1 GB minimum, 3 GB preferred.|

### Required operating system and software

|Software|Action required|
|------------|-------------------|
|Operating system \- [!INCLUDE[win8_server_2](Token/win8_server_2_md.md)]|Install on the server.|
|Secure Sockets Layer \(SSL\) server certificate for the [!INCLUDE[spfshort](Token/spfshort_md.md)] website|Obtain or create an SSL server certificate  before installation. Applicable certificates will appear in the [!INCLUDE[spfshort](Token/spfshort_md.md)] setup wizard on the **Specify a location for the SPF files** page. Any preselected certificate may or may not be the most applicable certificate for your environment. You can obtain a certificate in the following ways:<br /><br />-   Purchase and import a certificate from a certification authority.<br />-   Import an Active Directory Certificate.<br />-   Create a self\-signed certificate. For more information, see [How to Create an SSL Certificate for Testing Service Provider Foundation](How-to-Create-an-SSL-Certificate-for-Testing-Service-Provider-Foundation.md).|
|Microsoft ASP.NET Model View Controller \(MVC\) 4|Install from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=277086).|
|Microsoft SQL Server 2008 R2 or SQL Server 2012; supported editions include:<br /><br />-   SQL Server 2008 R2: <br />    Standard, Datacenter, and Enterprise.<br />-   SQL Server 2012: <br />    Standard, Business Intelligence, and Enterprise.|Install if needed.<br /><br />Although it is not required to install [!INCLUDE[spfshort](Token/spfshort_md.md)], SQL Server is required on at least one server to contain the Service Provider Foundation database.<br /><br />The Setup program detects the existing installations of SQL Server and configures the use of any existing Service Provider Foundation database.|
|Windows Communication Foundation \(WCF\) Data Services 5.0 for Open Data Protocol \(OData\) V3|Install from the [Microsoft Download Center](http://go.microsoft.com/fwlink/p/?LinkId=263941).|
|[!INCLUDE[vmm12long](Token/vmm12long_md.md)] Console<br /><br />Although you do not need to install the full [!INCLUDE[vmm12sp1_long](Token/vmm12sp1_long_md.md)], you will need to make references to a server that has [!INCLUDE[vmm12sp1_med](Token/vmm12sp1_med_md.md)] running and that can be accessed by supplied credentials.|Install from the Microsoft System Center Virtual Machine Manager 2012 Setup Wizard; see [How To Install the VMM Console](assetId:///08ea3103-14cf-4d05-88fd-1ff443e6df6d).<br /><br />This is required so that Setup can install the VMM web service.|
|Management OData Internet Information Services \(IIS\) Extension|Add this feature in [!INCLUDE[win8_server_2](Token/win8_server_2_md.md)] Server Manager.|
|Windows Process Activation service. This features includes:<br /><br />-   Process Model<br />-   Configuration application programming interfaces \(APIs\)|Add this feature in [!INCLUDE[win8_server_2](Token/win8_server_2_md.md)] Server Manager.|
|Web Server \(IIS\). This server role includes:<br /><br />-   IIS Management Scripts and Tools Role Service<br />-   IIS Security Basic Authentication<br />-   IIS Application Deployment ASP.NET 4.5<br />-   IIS Security Windows Authentication<br />-   Internet Server API \(IASPI\) extensions and filters<br />-   ASP.NET 4.5 Role Service|Add this role in [!INCLUDE[win8_server_2](Token/win8_server_2_md.md)] Server Manager if not already installed.|
|[!INCLUDE[powshelllongname](Token/powshelllongname_md.md)] 3.0|None. Installed with [!INCLUDE[win8_server_2](Token/win8_server_2_md.md)].|
|Microsoft .NET Framework 3.5. This feature includes:<br /><br />-   ASP.NET 3.5<br />-   Common Language Runtime 2.0|None. Installed with [!INCLUDE[win8_server_2](Token/win8_server_2_md.md)].|
|.NET Framework 4.5. This feature includes:<br /><br />-   ASP.NET 4.5<br />-   WCF services HTTP Activation<br />-   Common Language Runtime 4.5|None. Installed with [!INCLUDE[win8_server_2](Token/win8_server_2_md.md)].|

## See Also
[Capacity Planning for Service Provider Foundation](Capacity-Planning-for-Service-Provider-Foundation.md)
[How to Install Service Provider Foundation for System Center 2012 SP1](How-to-Install-Service-Provider-Foundation-for-System-Center-2012-SP1.md)
[Deploying Service Provider Foundation](Deploying-Service-Provider-Foundation.md)
[Administering Service Provider Foundation](Administering-Service-Provider-Foundation.md)
[Architecture Overview of Service Provider Foundation](Architecture-Overview-of-Service-Provider-Foundation.md)


