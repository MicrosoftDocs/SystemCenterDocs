---
ms.assetid: 170dc7fd-11a3-411c-a164-e8fce974deee
title: Management Pack for SQL Server Reporting Services Delivery
description: This article explains how to install Management Pack for SQL Server Reporting Services
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Management Pack for SQL Server Reporting Services Delivery

You can download Management Pack for SQL Server Reporting Services from the [Microsoft portal](https://www.microsoft.com/en-us/download/details.aspx?id=57381) or System Center Operations Manager Online Catalog.

After you download and unpack the **Microsoft.SQLServer.ReportingServices.ManagementPack.msi** package—a set of MP and MPB files for monitoring of Reporting Services on Windows, the following files become available:

- **Microsoft.SQLServer.ReportingServices.Discovery.mpb**

    This Management Pack discovers Microsoft SQL Server Reporting Services (Native Mode) and related objects. The management pack contains the discovery logic only and requires a separate monitoring management pack to be imported to monitor discovered objects.

- **Microsoft.SQLServer.ReportingServices.Monitoring.mpb**

    This management pack enables monitoring of Microsoft SQL Server Reporting Services (Monitoring, Native Mode).

- **Microsoft.SQLServer.ReportingServices.Core.Library.mpb**

    This library contains basic components required for monitoring of Microsoft SQL Server Reporting Services (Monitoring, Native Mode).

- **Microsoft.SQLServer.ReportingServices.Core.Views.mp**

    This management pack defines views for Microsoft SQL Server Reporting Services (Native Mode).

- **Microsoft.SQLServer.Visualization.Library.mpb**

    This library contains basic visual components required for SQL Server dashboards.

- **Microsoft.SQLServer.Core.Library.mpb**

    This management pack is the core library for all versions of SQL Server. It defines all SQL Server base classes and relationships.

## Prerequisites

The environment that you use must meet the following prerequisites before you start using Management Pack for SQL Server Reporting Services:

- Install **.NET Framework 4.5** or higher.

- Import **Management Pack for Windows Server Operating System**.

- Enable the **Agent Proxy** option on all agents installed on servers that host either SQL Server Reporting Services instance or SQL Server instance with respective SSRS Catalog Database. For more information, see [Enabling Agent Proxy Option](rsmp-monitoring-configuration.md#enabling-agent-proxy-option).
  
  This option should be enabled in cases when the agent workflow scenarios discover any non-hosted objects created by the management pack for each SQL Server instance.

- Enable the TCP/IP protocol for SQL Server instances that host the reporting server database.

- Enable the **SQL Server Browser** service.

    This service is required for Reporting Services discovery and monitoring and must be running on computers with Reporting Services and on computers that host the reporting server database.

- Import the **Microsoft SQL Server on Windows (Discovery)** management pack.

    This management pack does not discover database objects for SSRS Catalog Database or SSRS Temporary Database.
  
    Import Management Pack for SQL Server to enable discovery, monitoring, and health rollup for SSRS databases and deployment performance collection. For more information, see [Discovery of SQL Server Reporting Services Deployment](rsmp-monitoring-configuration.md#discovery-of-sql-server-reporting-services-deployment).

- Use a domain account for monitoring.

    Monitoring with a domain account is highly recommended. For more information, see [Least-Privilege Monitoring Configuration](rsmp-least-privilege-monitoring.md).

    You can use the Local System account or HealthService SSID as an action account.

## Importing Management Pack

For more information on how to import management packs, see [How to Import a Management Pack](https://go.microsoft.com/fwlink/?LinkId=142351).