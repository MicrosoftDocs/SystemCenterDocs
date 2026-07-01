---
title: Troubleshoot failures when adding the Orchestrator database to a SQL Always On availability group
description: This article describes how to resolve failures when you add the Orchestrator database to a SQL Server Always On availability group.
ms.service: system-center
ms.subservice: orchestrator
ms.topic: troubleshooting-known-issue
author: Jeronika-MS
ms.author: v-gajeronika
ms.date: 06/30/2026
ms.update-cycle: 1095-days
moniker range: 'sc-orch-2022', 'sc-orch-2025'
---

# Troubleshoot failures when adding the Orchestrator database to a SQL Always On availability group

This article describes how to resolve failures when you add the Orchestrator database to a SQL Server Always On availability group.

## Issue

Operation fails when you try to add the Orchestrator database to an *Always On availability* group.

## Cause

The SQL Server Service Master Key (SMK) differs between the SQL Server instances involved in the availability group operation.

Orchestrator uses encrypted data in SQL Server. If the SMK that protects the encryption chain is inconsistent across participating SQL Server instances, operations that depend on that encryption can fail.

## Workaround

Use the following steps to align the Service Master Key across the SQL Server instances.

>[!NOTE]
> These steps affect SQL Server cryptography settings. Review your change process, involve your database administrator (DBA), and test in a non-production environment first.

### Step 1: Check the Service Master Key on each SQL Server instance

Run the following query on each SQL Server instance and compare the results:

```
USE master

SELECT \* FROM sys.symmetric_keys
```

If *key_guid* values don't match between instances, continue with the next steps.

### Step 2: Back up the Service Master Key on the source SQL Server

On the SQL Server instance that currently has the expected key, back up the Service Master Key.

```
BACKUP SERVICE MASTER KEY

TO FILE = ‘C: backup\service master key’

ENCRYPTION BY PASSWORD = ‘3dH85Hhk004GHk2597ghefj5’;
```

### Step 3: Restore the Service Master Key on the target SQL Server

Copy the backup file to the target SQL Server instance and run:

```
RESTORE SERVICE MASTER KEY

FROM FILE = ‘C: backup\service master key’ DECRYPTION BY PASSWORD = ‘3dH85Hhk004GHk2597ghefj5’ FORCE

GO
```

>[!Warning]
>FORCE can affect other databases that use SQL Server encryption on the same instance. Review potential impact before you run this command.

### Step 4: Verify key alignment

Run the query from Step 1 again on each SQL Server instance and confirm that *key_guid* values match.

### Step 5: Restart required services

Restart the SQL Server service on affected SQL Server instances, Orchestrator Management service on the management server and Orchestrator Runbook service on each runbook server.
