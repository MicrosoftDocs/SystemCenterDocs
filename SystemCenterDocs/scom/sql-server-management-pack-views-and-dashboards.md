---
ms.assetid: 876c7d8c-0b45-4cb2-b3c0-d8748603875a
title: Views and dashboards in Management Pack for SQL Server
description: This article explains views and dashboards in Management Pack for SQL Server
author: TDzakhov
ms.author: v-tdzakhov
manager: evansma
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Views and Dashboards in Management Pack for SQL Server

Management Pack for SQL Server introduces the following version-independent views and dashboards.

![Generic views and dashboards](./media/sql-server-management-pack/version-independent-views.png)

The **Computers** view displays computers on which agents are installed and management pack discovery is running. This view does not display computers configured for [agentless monitoring](sql-server-management-pack-monitoring-modes.md#configuring-agentless-monitoring-mode).

The **SQL Server Roles** dashboard provides information about instances of SQL Server Database Engine, SQL Server Reporting Services, SQL Server Analysis Services, and SQL Server Integration Services.

![SQL server roles](./media/sql-server-management-pack/sql-server-roles.png)

Some of these views may consist of a very long list of objects and metrics. To find specific objects, you can use the **Scope**, **Search**, and **Find** buttons on the Operations Manager toolbar. For more information, see [Finding data and objects in the Operations Manager consoles](manage-console-finding-data.md).
