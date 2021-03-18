---
ms.assetid: 9e13d0f4-84b2-42bf-836f-b23791616971
title: Management Pack for SQL Server Delivery
description: This article explains how to install Management Pack for SQL Server
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Management Pack for SQL Server Delivery

You can download Management Pack for SQL Server from the [Microsoft portal](https://www.microsoft.com/en-us/download/details.aspx?id=56203) or System Center Operations Manager Online Catalog.

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

### Notes to Release

- **Previous generations of management packs for SQL Server 2012, 2014, and 2016 reached the end of support**

  This management pack is virtually a new version of the version-agnostic management pack for SQL Server 2017 and higher (last version - 7.0.7.0 as of July 2018). 
  
  All upcoming versions of the management pack, including the current one are intended for monitoring of SQL Server 2012, 2014, 2016, 2017, and higher. 
  
  Previous generations of management packs for SQL Server 2008—2016 have reached the end of support with the first public release of the management pack for SQL Server 2012 and higher (April, 2019).

- **Upgradability issues of path SQL Server 2017+ MP v.7.0.7.0 → any version of the current management pack**
  
  When upgrading SQL Server 2017+ Management Pack, all instances of SQL Server 2017 will be automatically rediscovered. Such behavior affects reporting because historical data collected for these instances becomes unavailable.
  
  Management pack for SQL Server 2017+ Integration Services cannot be upgraded and has to be removed before importing this update.

- **Localization for SQL Server 2017+ MP cannot be imported over the current version of SQL Server MP**

  This management pack cannot be localized with localization packs made for SQL Server 2017+ MP. If you already have a localized version of SQL Server 2017+ MP (7.0.0.0 or 7.0.7.0), you do not need to remove the localization pack before importing this management pack.

## Prerequisites

The environment that you use must meet the following prerequisites before you start using Management Pack for SQL Server:

- Install **.NET Framework 4.5** or higher.

- Import both the **Management Pack for Windows Server Operating System** and the **Management Pack for UNIX and Linux Operating Systems**.

- Remove overrides for the **SQL on Windows: Discover Installation Source (seed)** discovery when upgrading Management Pack for SQL Server 2017+ to the current one.

- Enable the **Allow log on locally** security policy for the domain account that is used as an action account.

- Enable the **Agent Proxy** option on each agent to allow agents to forward data to Management Servers.
  
  This option should be enabled in cases when the agent workflow scenarios discover any non-hosted objects created by the management pack for each SQL Server instance.

- Enable and run SQL Server Browser for [agentless monitoring](./ssmp-monitoring-modes.md#configuring-agentless-monitoring-mode) mode.
  
- Remove the Microsoft SQL Server 2017+ Integration Services on Window management pack before importing this management pack.

  Management pack for SQL Server 2017+ Integration Services cannot be upgraded and has to be removed before importing this management pack.

- Grant an author set of privileges on SCOM SDK.

  This management pack requires an author set of privileges to create a management pack for storing overrides. If the default action account does not have these privileges, create a new account and map this account to the Microsoft SQL Server Run As Profile.

## Importing Management Pack

If you already have any of the version-specific management packs, discovery and monitoring provided by this management pack will be disabled and will be performed solely by the existing version-specific management packs.

To disable monitoring of SQL Server 2012/2014/2016 instances that might already be monitored by any of the version-specific management packs, the **MSSQL on Windows: Automatic setup of DB Engine discovery filter** rule is used.

This rule looks for existing instances and adds the corresponding versions to the **SQL Server versions to be excluded** parameter, which is then saved as an override to the **Microsoft SQLServer overrides** management pack. The rule then disables itself and saves its state to the **Microsoft SQLServer overrides** management pack.

If you remove the **Microsoft SQLServer overrides** management pack while still having version-specific management packs, the rule will re-create this management pack anew.

To make the version-agnostic management pack the primary source of monitoring, remove version-specific management packs and then remove (or modify) the **Microsoft SQLServer overrides** management pack.

When you import version-specific management packs after importing the version-agnostic management pack, monitoring provided by the version-agnostic management pack will not be disabled.

For more information on how to import management packs, see [How to Import a Management Pack](https://go.microsoft.com/fwlink/?LinkId=142351).

## See also

- [Management Pack Templates](management-pack-templates.md)
- [Monitors and Rules](https://docs.microsoft.com/previous-versions/system-center/system-center-2012-R2/hh457603%28v%3dsc.12%29)
