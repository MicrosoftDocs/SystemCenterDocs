---
ms.assetid:
title: Configure Antivirus for Operations Manager Components
description: This article provides design guidance for anti-virus exclusions as they relate to Operations Manager agent and server roles.
author: JYOTHIRMAISURI
ms.author: magoedte
manager: carmonm
ms.date: 07/06/2020
ms.custom: na
ms.prod: system-center
ms.technology: operations-manager
ms.topic: article
---

# Configuring antivirus exclusions for agent and components

This article outlines antivirus exclusions as they pertain to System Center - Operations Manager.  For earlier versions of Operations Manager, see [Recommendations for antivirus exclusions](https://support.microsoft.com/en-us/help/975931/recommendations-for-antivirus-exclusions-that-relate-to-operations-man).

For specific exclusion recommendations for supported versions of SQL Server, see [KB309422](https://support.microsoft.com/help/309422/choosing-antivirus-software-for-computers-that-run-sql-server).

## Exclusions by process executable

If exclusions are configured based on process executable, exclude the following processes:

|Component | Process |
|--------|---------|
|**Management servers** |MonitoringHost.exe<br> HealthService.exe<br> Microsoft.Mom.Sdk.ServiceHost.exe<br> cshost.exe |
|**Gateway server** |HealthService.exe<br> MonitoringHost.exe |
|**Windows agent** |HealthService.ex<br> MonitoringHost.exe |
|**Web Console server** |HealthService.exe<br> MonitoringHost.exe |
|**SQL Server**<sup>1</sup> |HealthService.exe<br> MonitoringHost.exe |

<sup>1</sup> For SQL Server servers hosting the Operations Manager databases (Operational, Data Warehouse, ACS) and Reporting server role.

>[!NOTE]
>You must be careful when you add exclusions that are based on executables. Incorrectly configured exclusions may prevent some potentially dangerous programs from being detected. Therefore, we do not recommend relying on exclusions that are based on any process executables for Operations Manager servers.

## Exclusions by directories

The following directory-specific exclusions for Operations Manager include real-time scans, scheduled scans, and local scans. The directories that are listed here are default application directories so you may have to modify these paths based on your specific environment. Only the following Operations Manager related directories should be excluded.

>[!NOTE]
>When a directory that is to be excluded has a directory name greater than 8 characters long, add both the short and long directory names of the directory to the exclusion list. These names are required by some antivirus programs to traverse sub-directories.

|Component | Directory Exclusion |
|----------|----------|
|**SQL Server database server** | Exclude the directory containing the .ldf and .mdf files for all Operations Manager databases,<br>Report server databases, and the **master** and **tempdb** databases. |
|**Management server** | %ProgramFiles%\Microsoft System Center 2016\Operations Manager\Server\Health Service State for Operations Manager 2016<br> %ProgramFiles%\Microsoft System Center\Operations Manager\Server\Health Service State for Operations Manager 1801 and higher. |
|**Gateway server** | %ProgramFiles%\System Center Operations Manager\Gateway\Health Service State |
|**Agent** |%ProgramFiles%\Microsoft Monitoring Agent\Agent\Health Service State |
|**Reporting server** | %ProgramFiles%\Microsoft System Center 2016\Operations Manager\Reporting for Operations Manager 2016<br> %ProgramFiles%\Microsoft System Center\Operations Manager\Reporting for Operations Manager 1801 and higher. |
|**Web Console server** |%ProgramFiles%\Microsoft System Center 2016\Operations Manager\WebConsole for Operations Manager 2016<br> %ProgramFiles%\Microsoft System Center \Operations Manager\WebConsole for Operations Manager 1801 and higher. |

## Exclusion of file type by extension

The following file name extension-specific exclusions for Operations Manager include real-time scans, scheduled scans, and local scans.

|Component | File Type Extension Exclusion |
|----------|----------|
| **SQL Server database server** | Exclude file type extension .ldf and .mdf.<br>These exclusions include SQL Server database files for all Operations Manager databases, Report Server databases, and the system database files for **master** and **tempdb**. |
| **Management server**<br>**Gateway server**<br>**Agents** | Exclude file type extensions .edb, .chk, and .log. These exclusions includes the queue and log files used by Operations Manager. |

## Next steps

For a complete listing of ports used, the direction of the communication, and if the ports can be configured, see [Configuring a Firewall for Operations Manager](plan-security-config-firewall.md).
