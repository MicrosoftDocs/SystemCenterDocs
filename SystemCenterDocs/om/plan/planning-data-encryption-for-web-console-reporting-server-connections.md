---
ms.assetid: d7f96cca-113c-4732-a3ba-e7f593350015
title: Data Encryption for Web console and Reporting server Connections
description:  
author: mgoedtel
manager: cfreemanwa
ms.date: 10/12/2016
ms.custom: na
ms.prod: system-center-threshold
ms.technology: operations-manager
ms.topic: article
---

# Data Encryption for Web console and Reporting server Connections

>Applies to: System Center 2016 - Operations Manager

You can configure the Operations Manager Web console and Reporting server to use Secure Sockets Layer (SSL) connections to ensure that both incoming requests and outbound responses are encrypted prior to transmission.  Operations Manager can use Federal Information Processing Standard (FIPS) compliant algorithms for secure data encryption when accessing the Web console and when running reports in the Operations console from the Reporting server.

Separate unique certificates will need to be requested and generated before you can proceed with configuring SSL connections for either role.  

## Web console encryption

When you install the web console, you must specify a web site for use with the web console. The default port for accessing the web console from a browser using Windows-based authentication is the same port as the web site that is selected when the web console was installed. If the web site chosen has been configured to use SSL, then you must also select Enable SSL. 

You must also select an authentication mode for use with the web console. Use mixed authentication for intranet scenarios and network authentication for extranet scenarios.

The web console uses two encryption algorithms:

-	SHA256
-	HMACSHA256

These algorithms may not be sufficient to meet compliance standards. For instance, they do not meet the Federal Information Processing Standard (FIPS). In order to meet a compliance standard, you need to map these names, in the appropriate configuration files, to appropriate encryption algorithms.

## Reporting server encryption

SQL Server Reporting Services Native mode uses the HTTP SSL (Secure Sockets Layer) service to establish encrypted connections to a report server. If you have certificate (.cer) file installed in a local certificate store on the report server computer, you can bind the certificate to a Reporting Services URL reservation to support report server connections through an encrypted channel.  

Because Internet Information Services (IIS) also uses HTTP SSL, there are significant interoperability issues that you must account for if you plan to run IIS and SQL Reporting Services on the same computer in support of Operations Manager Reporting server. Be sure to review the Interoperability Issues with IIS section in the [Configure SSL Connections on a Native Mode Report Server](https://msdn.microsoft.com/library/ms345223%28v=sql.120%29.aspx#interoperability-issues-with-iis) for guidance on how to address these issues.

To configure SQL Server Reporting Services Native mode for SSL encryption before configuring Operations Manager Reporting server to use SSL, please see [Configure SSL Connections on a Native Mode Report Server](https://msdn.microsoft.com/library/ms345223%28v=sql.120%29.aspx).

## FIPS Compliance

After you install these two roles, you need to manually edit several configuration files to enable this algorithm on the IIS web server hosting the Web console, and the SQL Server report server.

Enabling FIPS compliance for System Center 2016 - Operations Manager requires that the underlying infrastructure used (Server OS, Active Directory etc.), also be FIPS compliant.  

The following is a summarized list of steps required to configure FIPS for your Web console server.

-	Install the Microsoft.EnterpriseManagement.Cryptography.dll. 
-	Edit several instances of the **machine.config** file. 
-	Edit the **WebHost\web.config** file. 
-	Edit the **MonitoringView\web.config** file. 

You will need the Global Assembly Cache Tool, gacutil.exe. This utility is part of the Windows .NET Framework SDK, which is a installation component included in the Windows Software Development Kit.  For more information, see [Gacutil.exe (Global Assembly Cache Tool)](https://msdn.microsoft.com/library/ex0ss12c.aspx).

The following is a summarized list of steps required to configure FIPS for your Reporting server:

- Change the configuration for the **ReportServer** and **ReportManager** **Web.config** file. 

## Certificates

You can configure the Operations Manager web console and report server to use Secure Sockets Layer (SSL) connections to ensure that both incoming requests and outbound responses are encrypted prior to transmission.  

Separate certificates will need to be requested and generated before you can proceed with configuring SSL connections for either role.  One unique certificate for the SQL server hosting reporting services and the other for the server hosting the web console.


## Next steps

- To configure the Web console to use SSL encryption or support FIPS compliance, please review [Configure Authentication with the Web console](../manage/configure-authentication-with-web-console.md)

- To configure the Reporting server to support FIPS compliance, please review [Configure Authentication with the Reporting server](../manage/configure-authentication-with-reporting-server.md) 
