---
ms.assetid: 1d7cbdf6-687f-4d47-8d7e-cc9e07072e58
title: Management pack for SQL Server Replication Delivery
description: This article explains how to install Management pack for SQL Server Replication
author: Anastas1ya
manager: evansma
ms.date: 07/24/2025
ms.author: jsuri
ms.topic: concept-article
ms.service: system-center
ms.subservice: operations-manager
---

# Management pack for SQL Server Replication Delivery

You can download Management Pack for SQL Server Replication from the [Microsoft portal](https://www.microsoft.com/download/details.aspx?id=56204) or find it in the System Center Operations Manager Online Catalog.

After you download and unpack the **Microsoft.SQLServer.Windows.Replication.ManagementPack.msi**—a set of MP and MPB files for monitoring of SQL Replication on Windows, the following files become available:

- **Microsoft.SQLServer.Replication.Windows.Discovery.mpb**

  This management pack discovers Microsoft SQL Server Replication Instances.

- **Microsoft.SQLServer.Replication.Windows.Monitoring.mpb**

  This management pack enables monitoring of Microsoft SQL Server Replication and depends on the Microsoft SQL Server Replication (Discovery) Management Pack.

- **Microsoft.SQLServer.Replication.Windows.Views.mp**

  This management pack contains views and folder structure for Microsoft SQL Server Replication management packs.

- **Microsoft.SQLServer.Replication.Core.Library.mpb**

  This management pack is the core SQL Server Replication library. It defines all SQL Server Replication base classes and relationships.

- **Microsoft.SQLServer.Replication.Core.Views.mpb**

  This management pack is the core SQL Replication library that provides views.

- **Microsoft.SQLServer.Visualization.Library.mpb**

  This management pack contains basic visual components required for SQL Server dashboards.

## Prerequisites

Before you use management pack for SQL Server Replication, ensure that the environment that you use must meet the following prerequisites:

- Install **.NET Framework 4.5** or higher.

- Import both the **Management Pack for Windows Server Operating System** and the **Management Pack for SQL Server**

- Enable the **Agent Proxy** option on each agent to allow agents to forward data to management servers. For more information, see [Enable Agent Proxy Option](sql-server-management-pack-enabling-agent-proxy.md).

>[!NOTE]
>Management Pack for SQL Server Replication doesn't support most of the non-printable characters, except #x9 | #xA | #xD | [#x20-#xD7FF] | [#xE000-#xFFFD] | [#x10000-#x10FFFF], which are supported. Using unsupported non-printable characters in object names leads to inevitable workflow failure.

## Import Management Pack

For more information on how to import management packs, see [How to import, export, and remove an Operations Manager management pack](manage-mp-import-remove-delete.md).
