---
ms.assetid:
title: Recommendations for antivirus exclusions that relate to Orchestrator
description: Describes some antivirus exclusions that relate to Orchestrator. These exclusions include process-based exclusions, directory-specific exclusions, and file name extension-specific exclusions.
author: PriskeyJeronika-MS
ms.author: v-gjeronika
manager: jsuri
ms.date: 05/30/2024
ms.service: system-center
ms.subservice: orchestrator
ms.topic: article
---

# Recommendations for antivirus exclusions that relate to Orchestrator

This article outlines antivirus exclusions that relate to System Center Orchestrator.

An incorrect exclusion may prevent some potentially dangerous programs from being detected. We don't recommend that you rely on exclusions that are based on any process executables for Orchestrator servers.

## Exclusions by process executable

If you must make exclusions that are based on the process executables, use the following processes:

|Component | Process |
|--------|---------|
|**Management Service** |ManagementService.exe, PolicyModule.exe |
|**Remoting Service** |OrchestratorRemotingService.exe, PolicyModule.exe |
|**Run Program Service** |OrchestratorRunProgramService.exe, PolicyModule.exe |
|**Runbook Server Monitor Service** |RunbookServerMonitorService.exe, PolicyModule.exe |
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

**For Runbook logs (Real time log, Historic log, Runbook audit history, Activity events, Audit trail)**

*%Common Files%\Microsoft System Center 2012\Orchestrator\Management Server\Components\Logs\*.log*

**For Trace logs**

*%ProgramData%Microsoft System Center 2012\Orchestrator\**\Logs\*.log*

## Exclusion of file type by extension

The following file name extension-specific exclusions for Orchestrator include real-time scans, scheduled scans, and local scans.

### SQL database servers

These exclusions include the SQL Server database files that are used by Orchestrator components and the system database files for the master database and for the tempdb database.

For example:

- *.mdf*
- *.ldf*
- *.ndf*

For standard Microsoft SQL Server specific exclusions, see [Configure antivirus software to work with SQL Server](/troubleshoot/sql/database-engine/security/antivirus-and-sql-server).

### Orchestrator (Management Server, Runbook Server)

These exclusions include the log files that are used by Orchestrator.

For Example:

- *.log*

Page files should also be excluded from any real-time scans.
