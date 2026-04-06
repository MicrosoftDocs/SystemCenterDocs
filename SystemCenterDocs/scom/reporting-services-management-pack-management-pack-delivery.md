---
ms.assetid: 170dc7fd-11a3-411c-a164-e8fce974deee
title: Management Pack for SQL Server Reporting Services delivery
description: This article explains how to install Management Pack for SQL Server Reporting Services
author: Anastas1ya
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.topic: concept-article
ms.service: system-center
ms.subservice: operations-manager
ms.update-cycle: 1095-days
---

# Management Pack for SQL Server Reporting Services Delivery

You can download Management Pack for SQL Server Reporting Services from the [Microsoft portal](https://www.microsoft.com/download/details.aspx?id=57381) or System Center Operations Manager Online Catalog.

After you download and unpack the **Microsoft.SQLServer.ReportingServices.ManagementPack.msi** package - a set of MP and MPB files for monitoring of Reporting Services on Windows, the following files become available:

- **Microsoft.SQLServer.ReportingServices.Discovery.mpb**

    This Management Pack discovers Microsoft SQL Server Reporting Services (Native Mode) and related objects. The management pack contains the discovery logic only and requires a separate monitoring management pack to be imported to monitor discovered objects.

- **Microsoft.SQLServer.ReportingServices.Monitoring.mpb**

    This management pack enables monitoring of Microsoft SQL Server Reporting Services.

- **Microsoft.SQLServer.ReportingServices.Core.Library.mpb**

    This library contains the basic components required for monitoring of Microsoft SQL Server Reporting Services.

- **Microsoft.SQLServer.ReportingServices.Core.Views.mp**

    This management pack defines views for Microsoft SQL Server Reporting Services.

- **Microsoft.SQLServer.Visualization.Library.mpb**

    This library contains basic visual components required for SQL Server dashboards.

- **Microsoft.SQLServer.Core.Library.mpb**

    This management pack is a core SQL Server library. It defines all SQL Server base classes and relationships.

## Prerequisites

The environment that you use must meet the following prerequisites before you start using Management Pack for SQL Server Reporting Services:

- Install **.NET Framework 4.5** or higher.

- Import **Management Pack for Windows Server Operating System**.

- Enable the **Agent Proxy** option on each agent to allow agents to forward data to management servers. For more information, see [Enabling Agent Proxy Option](sql-server-management-pack-enabling-agent-proxy.md).

- Enable the TCP/IP protocol for SQL Server instances that host the reporting server database.

- Enable the **SQL Server Browser** service.

    This service is required for Reporting Services discovery and monitoring and must be running on computers with Reporting Services and on computers that host the reporting server database.

- Import the **Microsoft SQL Server on Windows (Discovery)** management pack.

    This management pack doesn't discover database objects for SSRS Catalog Database or SSRS Temporary Database.

    Import Management Pack for SQL Server to enable discovery, monitoring, and health rollup for SSRS databases and deployment performance collection. For more information, see [Discovery of SQL Server Reporting Services Deployment](reporting-services-management-pack-monitoring-configuration.md#discovery-of-sql-server-reporting-services-deployment).

- Use a domain account for monitoring.

    Monitoring with a domain account is highly recommended. For more information, see [Least-Privilege Monitoring Configuration](reporting-services-management-pack-least-privilege-monitoring.md).

    You can use the Local System account or HealthService SSID as an action account.

>[!NOTE]
>Management Pack for SQL Server Reporting Services doesn't support most of the non-printable characters, except #x9 | #xA | #xD | [#x20-#xD7FF] | [#xE000-#xFFFD] | [#x10000-#x10FFFF], which are supported. Using unsupported non-printable characters in object names leads to inevitable workflow failure.

## Importing Management Pack

For more information on how to import management packs, see [How to import, export, and remove an Operations Manager management pack](manage-mp-import-remove-delete.md).
