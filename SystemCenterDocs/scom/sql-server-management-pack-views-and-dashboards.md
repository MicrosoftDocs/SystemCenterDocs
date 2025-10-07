---
ms.assetid: 876c7d8c-0b45-4cb2-b3c0-d8748603875a
title: Views and Dashboards in management pack for SQL Server
description: This article explains views and dashboards in management pack for SQL Server
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 04/09/2025
ms.topic: concept-article
ms.service: system-center
ms.subservice: operations-manager
---

# Views and Dashboards in Management Pack for SQL Server

Management Pack for SQL Server introduces the following version-independent views and dashboards.

![Screenshot showing Generic views and dashboards.](./media/sql-server-management-pack/version-independent-views.png)

The **Computers** view displays computers on which agents are installed and management pack discovery is running. This view doesn't display computers configured for [agentless monitoring](sql-server-management-pack-monitoring-modes.md#configuring-agentless-monitoring-mode).

The **SQL Server Roles** dashboard provides information about instances of SQL Server Database Engine, SQL Server Reporting Services, SQL Server Analysis Services, and SQL Server Integration Services.

![Screenshot of SQL server roles.](./media/sql-server-management-pack/sql-server-roles.png)

Some of these views may consist of a long list of objects and metrics. To find specific objects, you can use the **Scope**, **Search**, and **Find** buttons on the Operations Manager toolbar. For more information, see [Find data and objects in the Operations Manager consoles](manage-console-finding-data.md).
