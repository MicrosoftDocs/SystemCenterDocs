---
ms.assetid: 9e13d0f4-84b2-42bf-836f-b23791616971
title: Management Pack Delivery
description: This article explains how to install Management Pack for SQL Server
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 2/5/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Management Pack Delivery

You can download Management Pack for SQL Server from the [Microsoft portal](https://www.microsoft.com/) and System Center Operations Manager Online Catalog.

The package includes the following files:

- **SQLServerMP.Windows.msi**—a set of MP and MPB files for monitoring SQL on Windows.

- **SQLServerMP.Linux.msi**—a set of MP and MPB files for monitoring SQL on Linux.

- **SQLServerMPGuide.pdf**—the operations guide.

- **SQLServerDashboardsGuide.pdf**—the operations guide for SQL MP Dashboards.

- **SQLServerMPWorkflowList.pdf**—a complete list of SQL Server MP workflows.

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
>Do not import **Microsoft.SQLServer.Core.WebDashboards.mp** if the version of System Center Operations Manager that you use is lower than 2019. This file contains SQL Server MP Dashboards for the new Operations Manager Web Console introduced in System Center Operations Manager 2019.

## Prerequisites

The environment that you use must meet the following prerequisites before you start using Management Pack for SQL Server:

- Install **.NET Framework 4.5** or higher.

- Import both the **Management Pack for Windows Server Operating System** and the **Management Pack for UNIX and Linux Operating Systems**

- Remove overrides for the **SQL on Windows: Discover Installation Source (seed)** discovery when upgrading Management Pack for SQL Server 2017+ to the current one

- Enable the **Allow log on locally** security policy for the domain account that is used as an action account.

- Enable the **Agent Proxy** option on each agent that may use this management pack for monitoring to allow agents to forward data to the Management Server on behalf of another entity.
  
  This option should be enabled if the agent workflow scenarios discover any non-hosted objects created by the management pack for each SQL Server instance.

- Enable and run SQL Server Browser for [Agentless Monitoring](./ssmp-monitoring-modes.md#configuring-agentless-monitoring-mode) mode.
  
  *Agent Monitoring* mode supports TCP/IP, "Named Pipes" and "Shared Memory" protocols and does not require SQL Server Browser.

  *Agentless Monitoring* mode supports TCP/IP and "Named Pipes" protocols and required SQL Server Browser.

  *Mixed Monitoring* mode supports only TCP/IP protocol and does not require SQL Server Browser.
  
- Remove the Microsoft SQL Server 2017+ Integration Services on Window management pack before importing this management pack.

  Management pack for SQL Server 2017+ Integration Services cannot be upgraded and has to be removed before importing this management pack.

- Grant the **Author set of privileges** on SCOM SDK

  This management pack requires an author set of privileges to create a management pack for storing overrides. If the default action account does not have these privileges, create a new account and map this account to the Microsoft SQL Server Run As Profile.

## Importing Management Pack

Management Pack for SQL Server is version-agnostic. It supports discovery and monitoring of SQL Server 2012 through 2019 and higher, including SQL on Linux with SQL Server 2017 and higher.

For more information on how to import management packs, see [How to Import a Management Pack](https://go.microsoft.com/fwlink/?LinkId=142351).

If you already have any of the version-specific management packs, discovery and monitoring provided by this management pack will be disabled and will be performed solely by the existing version-specific management packs to avoid double monitoring.

To disable monitoring of SQL Server 2012/2014/2016 instances that might already be monitored by any of the version-specific management packs, the **MSSQL on Windows: Automatic setup of DB Engine discovery filter** rule is used.

This rule looks for existing instances and adds the corresponding versions to the **SQL Server versions to be excluded** parameter, which is then saved as an override to the **Microsoft SQLServer overrides** management pack. The rule then disables itself and saves its state to the **Microsoft SQLServer overrides** management pack.

If you remove the **Microsoft SQLServer overrides** management pack while still having version-specific management packs, the rule will re-create this management pack anew.

To make the version-agnostic management pack the primary source of monitoring, remove version-specific management packs and then remove (or modify) the **Microsoft SQLServer overrides** management pack.

When you import version-specific management packs after importing the version-agnostic management pack, monitoring provided by the version-agnostic management pack will not be disabled.

## Disabled Space Monitoring Workflows for SQL on Linux

Because SQL Server on Linux does not provide required data, the following rules and monitors are disabled by default:

- Rules:

  - MSSQL on Linux: DB Memory-Optimized Data Filegroup Free Space Total (MB)
  
  - MSSQL on Linux: DB Memory-Optimized Data Filegroup Free Space Total (%)
  
  - MSSQL on Linux: DB FILESTREAM Filegroup Free Space Total (%)
  
  - MSSQL on Linux: DB FILESTREAM Filegroup Free Space Total (MB)
  
  - MSSQL on Linux: DB Filegroup Free Space Total (%)
  
  - MSSQL on Linux: DB Filegroup Free Space Total (MB)
  
  - MSSQL on Linux: DB Filegroup Allocated Free Space (%)
  
  - MSSQL on Linux: DB Filegroup Allocated Free Space (MB)
  
  - MSSQL on Linux: DB Free Outer Space (MB)
  
  - MSSQL on Linux: DB Allocated Free Space (MB)
  
  - MSSQL on Linux: DB Transaction Log Free Space Total (%)
  
  - MSSQL on Linux: DB Allocated Space Used (MB)
  
  - MSSQL on Linux: DB Free Space Total (%)
  
  - MSSQL on Linux: DB Free Space Total (MB)
  
  - MSSQL on Linux: DB Allocated Space (MB)

- Monitors:
  
  - DB Free Space Left
  
  - DB Space Percentage Change
  
  - Transaction Log Free Space (%)
  
  - DB FILESTREAM Filegroup Free Space