---
ms.assetid:
title: Antivirus exclusions (Operations Manager 2019 and later)
description: Describes some antivirus exclusions that relate to Operations Manager. These exclusions include process-based exclusions, directory-specific exclusions, and file name extension-specific exclusions.
author: jyothisuri
ms.author: jsuri

ms.date: 11/01/2024
ms.custom: UpdateFrequency2
ms.service: system-center
ms.subservice: operations-manager
ms.topic: article
---

# Recommendations for antivirus exclusions that relate to Operations Manager 2019 and later

This article outlines antivirus exclusions that relate to System Center 2019 Operations Manager and later.  For earlier versions of Operations Manager, see [antivirus exclusions (Operations Manager 2012, 2012 R2, and 2016)](/troubleshoot/system-center/scom/antivirus-exclusions-recommendations).

For specific exclusion recommendations for supported versions of SQL Server, see: [Configure antivirus software to work with SQL Server](/troubleshoot/sql/database-engine/security/antivirus-and-sql-server).

## Exclusions by process executable

If exclusions are configured based on process executable, exclude the following processes:

|Component | Process |
|--------|---------|
|**Management servers** |HealthService.exe<br> MonitoringHost.exe<br> MOMPerfSnapshotHelper.exe<br> Microsoft.Mom.Sdk.ServiceHost.exe<br> cshost.exe |
|**Gateway server** |HealthService.exe<br> MonitoringHost.exe |
|**Windows agent** |HealthService.exe<br> MonitoringHost.exe<br> MOMPerfSnapshotHelper.exe |
|**Web Console server** |HealthService.exe<br> MonitoringHost.exe |
|**SQL Server**<sup>1</sup> |HealthService.exe<br> MonitoringHost.exe |

<sup>1</sup> For SQL Server servers hosting the Operations Manager databases (Operational, Data Warehouse, ACS) and Reporting server role.

>[!NOTE]
>You must be careful when you add exclusions that are based on executables. Incorrectly configured exclusions may prevent some potentially dangerous programs from being detected. Therefore, we don't recommend relying on exclusions that are based on any process executables for Operations Manager servers.

## Exclusions by directories

The following directory-specific exclusions for Operations Manager include real-time scans, scheduled scans, and local scans. The directories that are listed here are default application directories, so you may have to modify these paths based on your specific environment. Only the following Operations Manager related directories should be excluded.

>[!NOTE]
>When a directory that is to be excluded has a directory name greater than 8 characters long, add both the short and long directory names of the directory to the exclusion list. These names are required by some antivirus programs to traverse sub-directories.

::: moniker range="sc-om-2016"

|Component | Directory Exclusion |
|----------|----------|
|**SQL Server database server** | Exclude the directory containing the .ldf and .mdf files for all Operations Manager databases,<br>Report server databases, and the **master** and **tempdb** databases. |
|**Management server** | %ProgramFiles%\Microsoft System Center 2016\Operations Manager\Server\Health Service State |
|**Gateway server** | %ProgramFiles%\System Center Operations Manager\Gateway\Health Service State |
|**Windows agent** |%ProgramFiles%\Microsoft Monitoring Agent\Agent\Health Service State |
|**Reporting server** | %ProgramFiles%\Microsoft System Center 2016\Operations Manager\Reporting  |
|**Web Console server** |%ProgramFiles%\Microsoft System Center 2016\Operations Manager\WebConsole |

::: moniker-end

::: moniker range=">=sc-om-2019"

|Component | Directory Exclusion |
|----------|----------|
|**SQL Server database server** | Exclude the directory containing the .ldf and .mdf files for all Operations Manager databases,<br>Report server databases, and the **master** and **tempdb** databases. |
|**Management server** | %ProgramFiles%\Microsoft System Center\Operations Manager\Server\Health Service State |
|**Gateway server** | %ProgramFiles%\System Center Operations Manager\Gateway\Health Service State |
|**Windows agent** |%ProgramFiles%\Microsoft Monitoring Agent\Agent\Health Service State |
|**Reporting server** | %ProgramFiles%\Microsoft System Center\Operations Manager\Reporting |
|**Web Console server** | %ProgramFiles%\Microsoft System Center\Operations Manager\WebConsole |

::: moniker-end

## Exclusion of file type by extension

The following file name extension-specific exclusions for Operations Manager include real-time scans, scheduled scans, and local scans.

|Component | File Type Extension Exclusion |
|----------|----------|
| **SQL Server database server** | Exclude file type extension .ldf and .mdf.<br>These exclusions include SQL Server database files for all Operations Manager databases, Report Server databases, and the system database files for **master** and **tempdb**. |
| **Management server**<br>**Gateway server**<br>**Agents** | Exclude file type extensions .edb, .chk, and .log. These exclusions include the queue and log files used by Operations Manager. |

## Next steps

For a complete listing of ports used, the direction of the communication, and if the ports can be configured, see [Configuring a Firewall for Operations Manager](plan-security-config-firewall.md).
