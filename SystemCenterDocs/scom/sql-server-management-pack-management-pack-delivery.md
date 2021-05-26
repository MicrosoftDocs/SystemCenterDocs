---
ms.assetid: 9e13d0f4-84b2-42bf-836f-b23791616971
title: Management Pack for SQL Server delivery
description: This article explains how to install Management Pack for SQL Server
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 5/31/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Management Pack for SQL Server Delivery

You can download Management Pack for SQL Server from the [Microsoft portal](https://www.microsoft.com/download/details.aspx?id=56203) or System Center Operations Manager Online Catalog.

The package includes the following files:

- **SQLServerMP.Windows.msi**—a set of MP and MPB files for monitoring of SQL on Windows.
- **SQLServerMP.Linux.msi**—a set of MP and MPB files for monitoring of SQL on Linux.

Management Pack for SQL Server consists of the following files:  

- Microsoft.SQLServer.Core.Library.mpb
- Microsoft.SQLServer.Core.Views.</i>mp
- Microsoft.SQLServer.Core.WebDashboards.</i>mp
- Microsoft.SQLServer.IS.Windows.mpb
- Microsoft.SQLServer.IS.Windows.Views.</i>mp
- Microsoft.SQLServer.Visualization.Library.mpb
- Microsoft.SQLServer.Linux.Views.</i>mp
- Microsoft.SQLServer.Linux.Discovery.mpb
- Microsoft.SQLServer.Linux.Monitoring.mpb
- Microsoft.SQLServer.Windows.Views.mpb
- Microsoft.SQLServer.Windows.Discovery.mpb
- Microsoft.SQLServer.Windows.Monitoring.mpb

>[!NOTE]
>Do not import **Microsoft.SQLServer.Core.WebDashboards.mp** if the version of System Center Operations Manager that you use is lower than 2019. **Microsoft.SQLServer.Core.WebDashboards.mp** contains SQL Server MP Dashboards for the new Operations Manager Web Console introduced in System Center Operations Manager 2019.

## Prerequisites

The environment that you use must meet the following prerequisites before you start using Management Pack for SQL Server:

- Install **.NET Framework 4.5** or higher.

- Import both the **Management Pack for Windows Server Operating System** and the **Management Pack for UNIX and Linux Operating Systems**.

- Remove overrides for the **SQL on Windows: Discover Installation Source (seed)** discovery when upgrading Management Pack for SQL Server 2017+ to the current one.

- Enable the **Allow log on locally** security policy for the domain account that is used as an action account.

- Enable the **Agent Proxy** option on each agent to allow agents to forward data to management servers. For more information, see [Enabling Agent Proxy Option](sql-server-management-pack-enabling-agent-proxy.md).

- Enable and run SQL Server Browser for [agentless monitoring](sql-server-management-pack-monitoring-modes.md#configuring-agentless-monitoring-mode) mode.
  
- Remove the Microsoft SQL Server 2017+ Integration Services on Window management pack before importing this management pack.

  Management pack for SQL Server 2017+ Integration Services cannot be upgraded and has to be removed before importing this management pack.

- Grant an author set of privileges on SCOM SDK.

  This management pack requires an author set of privileges to create a management pack for storing overrides. If the default action account does not have these privileges, create a new account and map this account to the Microsoft SQL Server Run As Profile.

>[!NOTE]
>Management Pack for SQL Server does not support most of the non-printable characters, except #x9 | #xA | #xD | [#x20-#xD7FF] | [#xE000-#xFFFD] | [#x10000-#x10FFFF], which are supported. Using unsupported non-printable characters in object names leads to inevitable workflow failure.

## Importing Management Pack

If you already have any of the version-specific management packs, discovery and monitoring provided by this management pack will be disabled and will be performed solely by the existing version-specific management packs.

To disable monitoring of SQL Server 2012/2014/2016 instances that might already be monitored by any of the version-specific management packs, the **MSSQL on Windows: Automatic setup of DB Engine discovery filter** rule is used.

This rule looks for existing instances and adds the corresponding versions to the **SQL Server versions to be excluded** parameter, which is then saved as an override to the **Microsoft SQLServer overrides** management pack. The rule then disables itself and saves its state to the **Microsoft SQLServer overrides** management pack.

If you remove the **Microsoft SQLServer overrides** management pack while still having version-specific management packs, the rule will re-create this management pack anew.

To make the version-agnostic management pack the primary source of monitoring, remove version-specific management packs and then remove (or modify) the **Microsoft SQLServer overrides** management pack.

When you import version-specific management packs after importing the version-agnostic management pack, monitoring provided by the version-agnostic management pack will not be disabled.

For more information on how to import management packs, see [How to import, export, and remove an Operations Manager management pack](manage-mp-import-remove-delete.md).