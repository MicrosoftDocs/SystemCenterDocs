---
title: Plan SPF deployment
description: This topic provides an overview of how to plan for a Service Provider Foundation installation.
author: rayne-wiselman
ms.author: raynew
manager: cfreeman
ms.date: 10/14/2016
ms.topic: article
ms.prod: system-center-threshold
ms.technology: service-provider-foundation
ms.assetid: 617ee2c1-4dea-40e6-85b3-d87b15c0221d
---

# Plan SPF deployment

>Apples To: System Center 2016 - Service Provider Foundation

This article helps you make sure you have prerequisites and planning steps in place, before you deploy System Center 2016 - Service Provider Foundation (SPF).

## Deployment prerequisites

Deployment requirements for SPF include:

-	Make sure you have the minimum [hardware](https://technet.microsoft.com/system-center-docs/system-requirements/minimum-hardware-recommendations-for-system-center-technical-preview) and [software](https://technet.microsoft.com/system-center-docs/system-requirements/operating-systems-compatibility-for-system-center-technical-preview) requirements on the SPF server.
-	The SPF server needs SQL Server for its database. The SQL Server database can be local, or on a remote server and should have at least 5 GB of storage. When you install SPF you need to specify the server name and port number. [Learn more]( https://technet.microsoft.com/system-center-docs/system-requirements/sql-server-version-compatibility-for-system-center-technical-preview) about supported SQL Server versions.
-	The VMM console should be installed on the SPF server. SPF can also run on the same server as the VMM management server. VMM must be deployed in your infrastructure.
-	If you want to use usage metering to manage tenant costs, you need a System Center Operations Manager server, and a Data Warehouse server, running Windows 2012 R2 or later.
-	The following Server Manager features should be installed on the SPF server:
    - Role: Web Server (IIS) server. Include the following services:
        - Basic Authentication
        - Windows Authentication
        - Application Deployment ASP.NET 4.5
        - Application Development ISAPI Extensions
        - Application Deployment ISAPI Filters
        - IIS Management Scripts and Tools Role Service
    - Feature: Management OData IIS Extension
    - Feature: .NET Framework 4.5 features, WCF Services, HTTP Activation
-	Install the following web services:
    - [WCF Data Services 5.0 for OData V3](http://go.microsoft.com/fwlink/p/?LinkId=263941)
    - [ASP.NET MVC 4](http://go.microsoft.com/fwlink/?LinkID=277086)
-	You need an SSL server certificate. You can generate a test certificate automatically during setup, but we recommend you use that for testing purposes only, and obtain a certificate from a CA for your production environment.
-	A side-by-side installation of different SPF versions on the same server isn’t supported.
-	You can install on a VM.
-	Make sure that you have a domain user account with administrative privileges on the computers on which you want to install Service Provider Foundation.

## Administrator roles

Administrator roles
Here’s what you need:

- SQL Server administrator: A DBA role with full administrator rights on the SQL Server instance used by SPF. The administrator should be able to grant permissions to create databases, and to grant those permissions to the SPF administrator.
- SPF administrator: The SPF administration account should be a local administrator on the server on which you install SPF.
- Application pool user: This IIS role should have full administrator permissions in VMM, and permissions to create, read, update, and delete on the SPF database. For portal applications, these operations can be restricted to specific tables.

## Plan security

SPF implements Windows and IIS security features. Requirements include:

- Domain credentials must be used.
- SPF relies on IIS for user authentication. Only SSL (HTTPS) requests are accepted from provider endpoints, using default port 8090. Typically, the request should have the security context of the logged on user to make the request.
- When the setup wizard installs a web service, it creates a local security group on the computer, to run the service. You can specify users or groups with access to each web service and assign them to this local group. SPF checks that users sending requests belong to the appropriate local security group.
- The setup wizard creates application domain pools in IIS for each web service. You can specify the Network Service account, or an account that belongs to the security group. The wizard creates the following security group application pools:
SPF_Admin: Admin
    - SPF_VMM: VMM
    - SPF_Provider: Provider
    - SPF_Usage: Usage


## Plan capacity

- Database storage: 5 GB is sufficient even for large SPF databases.
- Web service: By default, SPF supports up to 1000 concurrent requests for its web services. We recommend this be a lower number in a production environment. You can change this configuration by specifying the value for the MaxRequestsPerTimeSlot key in the C:\inetpub\SPF\web.config file.
- Hardware recommendations: The following server scenarios each pertain to the recommendations listed in the following table.
    - Virtual Machine Manager (VMM) with or without SQL Server
    - Service Provider Foundation with or without SQL Server

**5000 or less VMs** | **5000-12,000 VMs** | **12,000 - 25,000 VMs**
--- | --- | ---
4 processor cores, 8 GB RAM | 8 processor cores, 8 GB RAM | 16 processor cores, 8 GB RAM.<br/><br/> Recommended for computers running VMM with or without SQL Server.

## Plan database

There are two database scenario configurations:

- Install SPF and connect to an existing database. In this scenario the SPF administrator must verify that the permissions for the database were granted by the database administrator as follows:
    - Alter: Create tables
    - Connect with Grant: Connect to existing database
    - Select with Grant, Update with Grant, Delete with Grant, Insert with Grant: Grant permissions to application pool users
    - Alter all logins: Create SQL Server logins for application pool users.

- Create a new database. In this scenario the database administrator must create the database (SCSPFDB) and then SPF administrator installs SPF, and has permissions to configure the database as needed. For example to add tables. SPF administrators must create SPF Application Pool in Internet Information Services (IIS) and create a database user for an Application Pool User with the following permissions:
    - Connect: Connect to the SPF database
    - Select, Update, Delete, Insert: Perform basic operations
    - Create the SQL Server logon for Application Pool User with default database set to SCSPFDB.: To log on to SQL Server and access the database.


## Next steps

[Deploy SPF](../deploy/deploy-spf.md)
