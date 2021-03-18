---
ms.assetid: 1d7cbdf6-687f-4d47-8d7e-cc9e07072e58
title: Management Pack for SQL Server Replication Delivery
description: This article explains how to install Management Pack for SQL Server Replication
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Management Pack for SQL Server Replication Delivery

You can download Management Pack for SQL Server Replication from the [Microsoft portal](https://www.microsoft.com/en-us/download/details.aspx?id=56204) or find it in the System Center Operations Manager Online Catalog.

After you download and unpack the **Microsoft.SQLServer.Windows.Replication.ManagementPack.msi**—a set of MP and MPB files for monitoring of SQL Replication on Windows, the following files become available:

- **Microsoft.SQLServer.Replication.Windows.Discovery.mpb**

  This management pack discovers Microsoft SQL Server Replication Instances.

- **Microsoft.SQLServer.Replication.Windows.Monitoring.mpb**

  This Management Pack enables monitoring of Microsoft SQL Server Replication and depends on the Microsoft SQL Server Replication (Discovery) Management Pack.

- **Microsoft.SQLServer.Replication.Windows.Views.mp**

  This Management Pack contains views and folder structure for Microsoft SQL Server Replication management packs.

- **Microsoft.SQLServer.Replication.Core.Library.mpb**

  This Management Pack is the core library for all versions of SQL Server Replication. It defines all SQL Server Replication base classes and relationships.

- **Microsoft.SQLServer.Replication.Core.Views.mpb**

  This Management Pack is the core library views for all versions of SQL Replication.

- **Microsoft.SQLServer.Visualization.Library.mpb**

  This Management Pack contains basic visual components required for SQL Server dashboards.

## Prerequisites

The environment that you use must meet the following prerequisites before you start using Management Pack for SQL Server Replication:

- Install **.NET Framework 4.5** or higher.

- Import both the **Management Pack for Windows Server Operating System** an the **Management Pack for SQL Server**

- Enable the **Agent Proxy** option on each agent to allow agents to forward data to management servers.
  
  This option should be enabled in cases when the agent workflow scenarios discover any non-hosted objects created by the management pack for each SQL Server instance. For more information on how to enable this option, see [Enabling Agent Proxy Option](ssrmp-management-pack-configuration.md#enabling-agent-proxy-option)

## Importing Management Pack

For more information on how to import management packs, see [How to Import a Management Pack](https://go.microsoft.com/fwlink/?LinkId=142351).