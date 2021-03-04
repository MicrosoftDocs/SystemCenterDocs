---
ms.assetid: c253b065-5690-4230-88dd-0f794c1480f3
title: Management Pack Delivery
description: This article explains how to install Management Pack for Azure SQL Database
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 2/5/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Management Pack Delivery

You can download Management Pack for Azure SQL Database from the [Microsoft portal](https://www.microsoft.com/en-us/download/details.aspx?id=38829) or System Center Operations Manager Online Catalog.

The package includes the following files:

- **Microsoft.SqlServer.Azure.ManagementPack.msi**—a set of MP and MPB files for monitoring of Azure SQL Databases.

Management Pack for Azure SQL Database consists of the following files:  

- Microsoft.SqlServer.Azure.mpb

- Microsoft.SqlServer.Azure.Presentation.mp

- Microsoft.SqlServer.UserMonitoring.mpb

- Microsoft.SQLServer.Core.Library.mpb

- Microsoft.SQLServer.Visualization.Library.mpb

>[!NOTE]
>SQL Azure Federation and Federation member workflows are deprecated in this management pack.

## Prerequisites

The environment that you use must meet the following prerequisites before you start using Management Pack for Azure SQL Database:

- Install **.NET Framework 4.5.2** or higher.

## Importing Management Pack

Management Pack for Azure SQL Database provides monitoring of [Azure SQL Database](https://azure.microsoft.com/en-us/services/sql-database/) using [Azure REST API](https://docs.microsoft.com/rest/api/azure/) and T-SQL queries.

For more information on how to import management packs, see [How to Import a Management Pack](https://go.microsoft.com/fwlink/?LinkId=142351).

The management pack supports monitoring of 2000 databases in a single Management Group.

>[!NOTE]
>If you have been using an agnostic version of [Management Pack for SQL Server](ssmp-supported-configuration.md) prior to the upgrade, you can remove both the **Microsoft.SQLServer.Generic.Dashboards.mp** management pack and the **Microsoft.SQLServer.Generic.Presentation.mp** management pack after the upgrade. For a non-agnostic version of Management Pack for SQL Server, the removal of these management packs is not possible.