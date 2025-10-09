---
ms.assetid: 90109309-a692-414d-8877-2853d44d3bb4
title: Management pack for SQL Server Analysis Services Delivery
description: This article explains how to install management pack for SQL Server Analysis Services
author: epomortseva
manager: evansma
ms.date: 04/17/2025
ms.author: v-gajeronika
ms.topic: concept-article
ms.service: system-center
ms.subservice: operations-manager
---

# Management Pack for SQL Server Analysis Services Delivery

Management Pack for SQL Server Analysis Services provides monitoring of SQL Server 2012 (and higher) Analysis
Services instances, databases, and partitions.

You can download Management Pack for SQL Server Analysis Services from the [Microsoft portal](https://www.microsoft.com/download/details.aspx?id=57382) or System Center Operations Manager Online Catalog.

After you download and unpack the **Microsoft.SQLServer.AnalysisServices.ManagementPack.msi** package - a set of MP and MPB files for monitoring of Analysis Services on Windows, the following files become available:

- **Microsoft.SQLServer.AnalysisServices.Windows.Discovery.mpb**

    This management pack discovers Microsoft SQL Server Analysis Services Instances and related objects. The management pack contains discovery logic only and requires a separate monitoring management pack to be imported for discovered objects monitoring.

- **Microsoft.SQLServer.AnalysisServices.Windows.Monitoring.mpb**

    This management pack enables Microsoft SQL Server Analysis Services monitoring. It depends on Microsoft SQL Analysis Services (Discovery) management pack.

- **Microsoft.SQLServer.AnalysisServices.Core.Views.</i>mp**

    This management pack defines views for Microsoft SQL Server Analysis Services.

- **Microsoft.SQLServer.AnalysisServices.Core.Library.mpb**

    This library contains basic components required for Microsoft SQL Server Analysis Services monitoring.

- **Microsoft.SQLServer.Visualization.Library.mpb**

    This library contains basic visual components required for SQL Server dashboards.

- **Microsoft.SQLServer.Core.Library.mpb**

    This management pack is a core SQL Server library. It defines all SQL Server base classes and relationships.

## Prerequisites

The environment that you use must meet the following prerequisites before you start using Management Pack for SQL Server Analysis Services:

- Install **.NET Framework 4.5** or higher.

- Import **Management Pack for Windows Server Operating System**.

- Enable the **Agent Proxy** option on each agent that is installed on the clustered servers. For more information, see [Enable Agent Proxy Option](sql-server-management-pack-enabling-agent-proxy.md). Enabling this option for standalone servers isn't required.

- Enable the **SQL Server Browser** service. This service is required for Analysis Services discovery and monitoring and must be installed and running on computers with Analysis Services. SQL Server Analysis Services port configuration depends on the SQL Server Browser settings. For more information, see [SQL Server Browser Service (Database Engine and SSAS)](/sql/database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas).

- Associate Microsoft SQL Server Run As profiles with the account that has administrative privileges for both the Windows Server and the SQL Server Analysis Services instance.

> [!NOTE]
> Management Pack for SQL Server Analysis Services doesn't support most of the non-printable characters, except #x9 | #xA | #xD | [#x20-#xD7FF] | [#xE000-#xFFFD] | [#x10000-#x10FFFF]. Using unsupported non-printable characters in object names leads to inevitable workflow failure.

## Import Management Pack

For more information on how to import management packs, see [How to import, export, and remove an Operations Manager management pack](manage-mp-import-remove-delete.md).
