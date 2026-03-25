---
title: Upgrade Operations Manager databases to SQL Server 2025
description: This article describes how to upgrade the SQL Server supporting System Center Operations Manager databases to SQL Server 2025.
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 03/23/2026
ms.service: system-center
monikerRange: 'sc-om-2025'
ms.update-cycle: 1095-days
ms.subservice: operations-manager
ms.topic: upgrade-and-migration-article
---

# Upgrade Operations Manager databases to SQL Server 2025

Operations Manager 2025 UR1 supports SQL Server 2025.

Use the steps in this article to perform an in-place upgrade of the databases supporting Operations Manager to SQL Server 2025.  Before you proceed, back up any custom authored reports, favorites, and schedules, which are stored in the report server database.  

>[!NOTE]
>Use ODBC 18 or later, and MSOLEDBSQL 19 or later.

Before you perform these upgrade steps, review the [SQL Server 2025 upgrade information](/sql/database-engine/install-windows/upgrade-sql-server?view=sql-server-ver17).

## Prerequisites

Before you upgrade Operations Manager databases to SQL Server 2025, ensure the following prerequisites are met:

- Ensure that System Center Operations Manager 2025 UR1 is installed, and has a supported Windows Server version, ODBC 18 or later, and MSOLEDBSQL 19 or later drivers.
- Stop Operations Manager services on all management servers (System Center Data Access, Microsoft Monitoring Agent, System Center Management Configuration).
- Back up all three databases: *OperationsManager*, *OperationsManagerDW*, and *ReportServer*.

## Upgrade to SQL Server 2025

To upgrade to SQL Server 2025, follow these steps:

1. Run SQL Server 2025 setup on the instance hosting the databases.
1. Select **Upgrade from previous version**. The upgrade sequence is OperationsManager > OperationsManagerDW > ReportServer.
1. Apply the latest SQL Server 2025 cumulative update after installation.

## Post-upgrade validation

To validate the upgrade, follow these steps:

1. Restart Operations Manager services.
1. Verify connectivity by running the test queries against *OperationsManager* and *OperationsManagerDW*.
1. Confirm that the Reporting Services loads custom reports, favourites, and schedules correctly.
1. Check event logs for SQL connectivity or schema errors.

## Stop the Operations Manager services

On all the management servers in the management group, stop the Operations Manager services:

- System Center Data Access
- Microsoft Monitoring Agent
- System Center Management Configuration

## Back up the Reporting server database

1. On the SQL Server hosting the Reporting server databases, create a full backup of the **ReportServer** and **ReportServerTempDB** databases. For more information, see [Create a Full Database Backup (SQL Server)](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server).

2. On the current Operations Manager reporting server, back up the SSRS encryption key. For more information, see [SSRS Encryption Keys - Back Up and Restore Encryption Keys](/sql/reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys).

3. Back up the report server configuration files. Files to back up include:

   * Web.config
