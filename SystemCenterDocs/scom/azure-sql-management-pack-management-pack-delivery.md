---
ms.assetid: c253b065-5690-4230-88dd-0f794c1480f3
title: Management Pack for Azure SQL Database Delivery
description: This article explains how to install Management Pack for Azure SQL Database
author: Anastas1ya
manager: evansma
ms.date: 04/23/2025
ms.author: jsuri
ms.topic: concept-article
ms.service: system-center
ms.subservice: operations-manager
---

# Management Pack for Azure SQL Database Delivery

You can download Management Pack for Azure SQL Database from the [Microsoft portal](https://www.microsoft.com/download/details.aspx?id=38829) or System Center Operations Manager Online Catalog.

After you download and unpack the **Microsoft.SqlServer.Azure.ManagementPack.msi** package—a set of MP and MPB files for monitoring of Azure SQL Database, the following files become available:

- Microsoft.SQLServer.Azure.mpb
- Microsoft.SQLServer.Azure.Presentation.mp
- Microsoft.SQLServer.UserMonitoring.mpb
- Microsoft.SQLServer.Core.Library.mpb
- Microsoft.SQLServer.Visualization.Library.mpb

> [!NOTE]
> SQL Azure Federation and Federation member workflows are deprecated in this management pack.

## Prerequisites

Before you import Management Pack for Azure SQL Database, ensure to install the **.NET Framework 4.5.2** or higher.

>[!NOTE]
>Management Pack for Azure SQL Database doesn't support most of the non-printable characters, except #x9 | #xA | #xD | [#x20-#xD7FF] | [#xE000-#xFFFD] | [#x10000-#x10FFFF], which are supported. Using unsupported non-printable characters in object names leads to inevitable workflow failure.

## Import Management Pack

Management Pack for Azure SQL Database provides monitoring of [Azure SQL Database](https://azure.microsoft.com/services/sql-database/) using Azure REST API and T-SQL queries.

For more information on how to import management packs, see [How to import, export, and remove an Operations Manager management pack](manage-mp-import-remove-delete.md).

The management pack supports monitoring of 2000 databases in a single Management Group.

>[!NOTE]
>If you've been using an agnostic version of [Management Pack for SQL Server](sql-server-management-pack-supported-configuration.md) prior to the upgrade, you can remove both the **Microsoft.SQLServer.Generic.Dashboards.mp** management pack and the **Microsoft.SQLServer.Generic.Presentation.mp** management pack after the upgrade. For a non-agnostic version of Management Pack for SQL Server, the removal of these management packs isn't possible.
