---
title: Prepare Your Environment for Service Provider Foundation
description: This topic provides an overview of how to make sure your environment is ready to install Service Provider Foundation.
ms.prod: system-center-threshold
ms.technology: service-provider-foundation
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7329a502-7fd0-4f4f-bebe-cc558589c086
ms.date:  2016-10-12
author: rayne-wiselman
ms.author: raynew
manager: cfreeman
---
# Prepare Your Environment for Service Provider Foundation
>Apples To: System Center 2016

The following tables describe the prerequisites for installing Service Provider Foundation for System Center 2016.  

For information on capacity planning for database storage, memory, and core processors, see [Capacity Planning for Service Provider Foundation](../Plan/Capacity-Planning.md).  

### Required hardware and settings  

|Hardware|Minimum required and recommended values, per web service|  
|------------|------------------------------------------------------------|  
|RAM|2&nbsp;gigabytes \(GB\) minimum, 4&nbsp;GB preferred.|  
|Available hard disk space|1&nbsp;GB minimum, 3&nbsp;GB preferred.|  

### Required operating system and software  

|Software|Action required|  
|------------|-------------------|  
|Operating system \- Windows Server 2012 or Windows Server 2016|Install on the server.|  
|Secure Sockets Layer \(SSL\) server certificate for the Service Provider Foundation website|Obtain or create an SSL server certificate  before installation. Applicable certificates will appear in the Service Provider Foundation setup wizard on the **Specify a location for the SPF files** page. Any preselected certificate may or may not be the most applicable certificate for your environment. You can obtain a certificate in the following ways:<br /><br />-   Purchase and import a certificate from a certification authority.<br />-   Import an Active Directory Certificate.<br />-   Create a self\-signed certificate. For more information, see [How to Create an SSL Certificate for Testing Service Provider Foundation](../Manage/How-to-Create-an-SSL-Certificate.md).|  
|Microsoft ASP.NET Model View Controller \(MVC\)&nbsp;4|Install from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=277086).|  
|Microsoft SQL Server&nbsp;2008&nbsp;R2 or SQL&nbsp;Server&nbsp;2012; supported editions include:<br /><br />-   SQL Server&nbsp;2008&nbsp;R2: <br />    Standard, Datacenter, and Enterprise.<br />-   SQL Server 2012: <br />    Standard, Business Intelligence, and Enterprise.|Install if needed.<br /><br />Although it is not required to install Service Provider Foundation, SQL&nbsp;Server is required on at least one server to contain the Service Provider Foundation database.<br /><br />The Setup program detects the existing installations of SQL Server and configures the use of any existing Service Provider Foundation database.|  
|Windows Communication Foundation \(WCF\) Data Services&nbsp;5.0 for Open Data Protocol \(OData\)&nbsp;V3|Install from the [Microsoft Download Center](http://go.microsoft.com/fwlink/p/?LinkId=263941).|  
|Virtual Machine Manager \(VMM\), you will need to make references to a server that has Virtual Machine Manager  running and that can be accessed by supplied credentials.|Install from the Microsoft System Center Virtual Machine Manager 2012 Setup Wizard; see [How To Install the VMM Console](http://technet.microsoft.com/en-us/library/gg610627.aspx).<br /><br />This is required so that Setup can install the VMM web service.|  
|Management OData Internet Information Services \(IIS\) Extension|Add this feature in Windows Server 2012 Server Manager.|  
|Windows Process Activation service. This features includes:<br /><br />-   Process Model<br />-   Configuration application programming interfaces \(APIs\)|Add this feature in Windows Server.|  
|Web Server \(IIS\). This server role includes:<br /><br />-   IIS Management Scripts and Tools Role Service<br />-   IIS Security Basic Authentication<br />-   IIS Application Deployment ASP.NET 4.5<br />-   IIS Security Windows Authentication<br />-   Internet Server API \(IASPI\) extensions and filters<br />-   ASP.NET 4.5 Role Service|Add this role in Windows Server if not already installed.|  
|Windows PowerShell 3.0|None. Installed with Windows Server.|  
|Microsoft .NET Framework&nbsp;3.5. This feature includes:<br /><br />-   ASP.NET 3.5<br />-   Common Language Runtime&nbsp;2.0|None. Installed with Windows Server.|  
|.NET Framework&nbsp;4.5. This feature includes:<br /><br />-   ASP.NET 4.5<br />-   WCF services HTTP Activation<br />-   Common Language Runtime&nbsp;4.5|None. Installed with Windows Server.|  

## See Also  
[Capacity Planning for Service Provider Foundation](../Plan/Capacity-Planning.md)  
[Deploying Service Provider Foundation](../Deploy/Deploying-Service-Provider-Foundation.md)  
[Architecture Overview of Service Provider Foundation](../Get-Started/Architecture-Overview.md)  
