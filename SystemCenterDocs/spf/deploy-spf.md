---
title: Deploy System Center Service Provider Foundation (SPF)
description: This article describes how to install and deploy System Center Service Provider Foundation (SPF)
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 04/09/2025
ms.topic: install-set-up-deploy
ms.service: system-center
ms.subservice: service-provider-foundation
ms.custom:
  - UpdateFrequency2
  - intro-deployment
  - engagement-fy24
  - sfi-ropc-nochange
---

# Deploy SPF



This article describes how to install System Center - Service Provider Foundation (SPF). 

SPF is part of System Center - Orchestrator. SPF exposes an extensible OData web service that interacts with System Center Virtual Machine Manager (VMM) that enables service providers and hosters to design and implement multitenant self-service portals that integrate IaaS capabilities into System Center.

## Before you start

Here are some considerations before you deploy SPF:

- Read the [planning article](plan-spf.md) to ensure deployment prerequisites are in place.
- You can install SPF on a single server or on multiple servers.
- We recommend you install as an administrator so that you can configure customer experience and Microsoft update settings during installation.
- Remember you’ll need a SQL Server database for SPF on the same server or on a remote server.
- Before you install, ensure to close any open programs and check there’s no restart pending.
- Side-by-side installation of different SPF versions on the same server isn't supported.
- You can install SPF on a VM.
- The credentials of the user who installs SPF are used for the sign-in credentials for the dbo SQL Server security object for the SPF database. Use the `T:Microsoft.SystemCenter.Foundation.Cmdlet.Get-SCSPFConnectionString` and `T:Microsoft.SystemCenter.Foundation.Cmdlet.Set-SCSPFConnectionString` cmdlets to manage connections to the database.

## Create a certificate

SPF needs a server certificate for website bindings. The SPF website is the endpoint for the Admin and VMM services that use REST and OData technology to communicate with clients and portal applications. You can generate and use a self-signed certificate or use an existing/new CA certificate. We don't recommend self-signed certificates in a production environment. If you generate a self-signed certificate, note the following:

- A self-signed certificate should be used only for testing purposes.
- The FQDN should be specified for the certification path instead of **localhost**.
- The self-signed certificate should be in the personal or web hosting store.

## Install SPF

To install SPF, follow these steps:

1.	On the server on which you want to install SPF, double-click **SetupOrchestrator.exe** on the installation media to start the Setup Wizard.
2.	In the main Setup page, select **Service Provider Foundation**.
3.	In **Service Provider Foundation Setup**, select **Install**.
4.	In **License Terms**, review the license agreement. If you agree with the terms, select **I have read, understood, and agree with the terms of the license agreement** > **Next**.
5.	In **Prerequisites**, wait for the wizard to complete the prerequisite verification, and review the results. If any of the prerequisites are missing, install them and select **Check prerequisites** again. Then select **Next**.
6.	In **Configure the database server**, specify the SQL Server computer name, or accept the default localhost. In **Port Number**, accept the default or modify the setting and then select **Next**.
7.	In **Specify a location for the SPF files**, accept or change the location for the web service files. Optionally, change Website and port settings. The server certificate is used to configure the site bindings for the SPF website in IIS. You can select to automatically generate a self-signed certificate for test purposes. Then select **Next**.
8.	In **Configure the Admin web service**, specify the domain and username of each security group or user who will use this web service in the format: domain\user name with a semicolon to separate multiple entries.
9. Specify the account you want the application pool to use. It should be a domain account with permissions to make changes on the server. We recommend you use a service account and not Network Service. If you use a Network Service, the account must be a VMM administrator.
10. Configure the settings for the Provider, VMM, and Usage web services.
11. In **Microsoft Update**, select how you want to install updates and select **Next**.
12. In **Installation summary**, review the settings. Select **Install** when you're ready.
13. Select **Close** when you see the **Setup is complete** message.
14. Repeat this procedure if needed. For example, for a web farm.

If installation fails, refer to the log files: `Microsoft Service Provider*.log”`, in the *%SYSTEMDRIVE%\%TEMP%* folder.

## Next steps

- [Manage SPF](manage-register-spf.md)
- [Manage SPF](manage-register-spf.md)
