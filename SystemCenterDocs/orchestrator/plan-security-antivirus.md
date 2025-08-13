---
ms.assetid:
title: Recommendations for Antivirus Exclusions that relate to System Center Orchestrator
description: Describes some antivirus exclusions that relate to Orchestrator. These exclusions include process-based exclusions, directory-specific exclusions, and file name extension-specific exclusions.
author: jyothisuri
ms.author: jsuri
ms.date: 04/10/2025
ms.service: system-center
ms.subservice: orchestrator
ms.topic: article
---

# Recommendations for antivirus exclusions that relate to Orchestrator

This article outlines antivirus exclusions that relate to System Center Orchestrator.

>[!NOTE]
>An incorrect exclusion may prevent some potentially dangerous programs from being detected. 

We don't recommend that you rely on exclusions that are based on any process executables for Orchestrator servers.

## Exclusions by process executable

If you must make exclusions that are based on the process executables, use the following processes:

|Component | Process |
|--------|---------|
|**Management Service** |ManagementService.exe|
|**Remoting Service** |OrchestratorRemotingService.exe|
|**Run Program Service** |OrchestratorRunProgramService.exe|
|**Runbook Server Monitor Service** |RunbookServerMonitorService.exe|
|**Runbook Service** |RunbookService.exe, PolicyModule.exe |

## Exclusions by folders

### SQL Database servers

These exclusions include the SQL Server database files that are used by Orchestrator components and the system database files for the master database and for the tempdb database. To exclude these files by directory, exclude the directory for the .ldf and .mdf files.

For example:

- *%ProgramFiles%\Microsoft SQL Server\MSSQL.1\MSSQL\Data*
- *D:\MSSQL\DATA*
- *E:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\Log*

For standard Microsoft SQL Server specific exclusions, see [Configure antivirus software to work with SQL Server](/troubleshoot/sql/database-engine/security/antivirus-and-sql-server).

### Orchestrator (Management Server, Runbook Server)

These exclusions include the default installation locations for all Orchestrator server roles. Any deviation from these default locations should also be included.

**For a Management Server**

*%ProgramFiles%\Microsoft System Center\Orchestrator\Management Server*

**For a Runbook Server**

*%ProgramFiles%\Microsoft System Center\Orchestrator\Runbook Server*

## Exclusion of file type by extension

The following file name extension-specific exclusions for Orchestrator include real-time scans, scheduled scans, and local scans.

### SQL database servers

These exclusions include the SQL Server database files that are used by Orchestrator components and the system database files for the master database and for the tempdb database. [Learn more](/troubleshoot/sql/database-engine/security/antivirus-and-sql-server#directories-and-file-name-extensions-to-exclude-from-virus-scanning).

For standard Microsoft SQL Server specific exclusions, see [Configure antivirus software to work with SQL Server](/troubleshoot/sql/database-engine/security/antivirus-and-sql-server).

### Orchestrator (Management Server, Runbook Server)

These exclusions include the log files that are used by Orchestrator. For more information, see [Orchestrator Logs](/system-center/orchestrator/orchestrator-logs).

Page files should also be excluded from any real-time scans.
