---
ms.assetid: c253b065-5690-4230-88dd-0f794c1480f3
title: Management Pack for Azure SQL Database delivery
description: This article explains how to install Management Pack for Azure SQL Database
author: TDzakhov
manager: evansma
ms.author: jsuri
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Management Pack for Azure SQL Database Delivery

You can download Management Pack for Azure SQL Database from the [Microsoft portal](https://www.microsoft.com/download/details.aspx?id=38829) or System Center Operations Manager Online Catalog.

After you download and unpack the **Microsoft.SqlServer.Azure.ManagementPack.msi** package—a set of MP and MPB files for monitoring of Azure SQL Database, the following files become available:

- Microsoft.SqlServer.Azure.mpb
- Microsoft.SqlServer.Azure.Presentation.</i>mp
- Microsoft.SqlServer.UserMonitoring.mpb
- Microsoft.SQLServer.Core.Library.mpb
- Microsoft.SQLServer.Visualization.Library.mpb

>[!NOTE]
>SQL Azure Federation and Federation member workflows are deprecated in this management pack.

## Prerequisites

Make sure to install the **.NET Framework 4.5.2** or higher before importing Management Pack for Azure SQL Database.

>[!NOTE]
>Management Pack for Azure SQL Database does not support most of the non-printable characters, except #x9 | #xA | #xD | [#x20-#xD7FF] | [#xE000-#xFFFD] | [#x10000-#x10FFFF], which are supported. Using unsupported non-printable characters in object names leads to inevitable workflow failure.

## Importing Management Pack

Management Pack for Azure SQL Database provides monitoring of [Azure SQL Database](https://azure.microsoft.com/services/sql-database/) using Azure REST API) and T-SQL queries.

For more information on how to import management packs, see [How to import, export, and remove an Operations Manager management pack](manage-mp-import-remove-delete.md).

The management pack supports monitoring of 2000 databases in a single Management Group.

>[!NOTE]
>If you have been using an agnostic version of [Management Pack for SQL Server](sql-server-management-pack-supported-configuration.md) prior to the upgrade, you can remove both the **Microsoft.SQLServer.Generic.Dashboards.mp** management pack and the **Microsoft.SQLServer.Generic.Presentation.mp** management pack after the upgrade. For a non-agnostic version of Management Pack for SQL Server, the removal of these management packs is not possible.
