---
ms.assetid: 2973edd7-293f-496e-b4db-405d6438bb04
title: Features and enhancements in Management Pack for SQL Server
description: This article explains the new functionality and bug fixes implemented in Management Pack for SQL Server
author: vchvlad
ms.author: v-vchernov
manager: evansma
ms.date: 12/7/2022
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Features and Enhancements in Management Pack for SQL Server

This section covers new functionality and improvements in Management Pack for SQL Server.

## December 2022 - 7.0.40.0 CTP

### What's New

- Added support for the SQL Server 2022 RTM
- Added [custom monitoring](sql-server-management-pack-custom-monitor.md) which allows the creation of monitors and performance rules
- Added a new "Availability Database Log Backup Status" monitor which allows to track the alert backups in databases participated in Availability Groups
- Added new tasks which allow running the Discovery process on demand: "Run On-Demand Agent Job Discovery" and "Run On-Demand Database Discovery"
- Updated the Agent Job "Last Run Status" monitor by adding new overrides: 'Number of fails threshold' which determines the number of the job fails to change the monitor's status, and the 'Define the Canceled status as Failed' which could track the Cancelled job's last run status as a Failed
- Added new Agent "Job Duration" performance collection rule which collects the duration of the SQL Server Agent job in minutes, for Windows and Linux platforms
- Added new Agent "Job Duration" alerting rule which throws an alert if the execution time of any of SQL Agent jobs has exceeded the specified threshold in minutes, for Windows and Linux platforms
- Updated the "Securables Configuration Status" monitor by removing the unnecessary 'msdb.dbo.sp_help_jobactivity' securable and by adding new 'msdb.dbo.sysjobactivity', 'msdb.dbo.sysjobhistory', 'msdb.dbo.syssessions', and 'msdb.dbo.agent_datetime' securables
- Updated the "Low Privilege Monitoring" and the "Service SID" operations guide sections with updated T-SQL scripts for least-privileged configurations
- Added new "DB Log Bytes Flushed per Second", "DB Log Flushes per Second", and "DB Log Flush Wait Time" performance collection rules to measure the latency or investigate the I/O performance of a log device, for Windows and Linux platforms
- Added new "Long Running Queries" alerting rule which throws an alert if the execution time of any of the running SQL queries has exceeded the specified threshold in seconds, for Windows and Linux platforms
- Added new "DB Engine Disk Write Latency" and the "DB Engine Disk Read Latency" monitors to track the read/write latency issues at the DB Engine level
- Always On discovery and monitoring workflows have been optimized for better performance
- Policy discovery workflows have been optimized for better performance
- Updated space monitoring workflows to apply 4-significant digit rounding in all the values
- Updated the "Product Version Compliance" monitor with the most recent version of public updates for the SQL Server
- Updated display strings

### Bug Fixes

- Fixed a performance issue with the “Service Principal Name Configuration Status” monitor by reducing the load on the domain controller in large environments
- Fixed an issue with the "Thread Count" monitor and the performance rule. Now these workflows count free threads more precisely including only the 'VISIBLE ONLINE' schedulers
- Fixed an issue with the "Database Status" monitor in cases when the database, hosted on the Primary Replica of an Availability Group, has an issue with its state, the monitor does not change its state for that database and becomes Healthy
- Fixed an issue with showing the full SQL query instead of the path in the System Center Operations Manager diagnostic tracing toolset

## June 2022 - 7.0.38.0 RTM

### What's New

- Added 'Timeout for query execution (seconds)' override which can now be used in all workflows
- Added 'Number of samples' override to the "Database Status" monitor to help avoid alert storming
- Added support for the SQL Server 2022 public preview
- Added support for enabling debug logging in Windows Event Log
- Added support for enabling diagnostic tracing in the System Center Operations Manager toolset
- The SQL Server Evaluation edition can now be added to the exclude list of the "Local DB Engine" discovery
- Monitoring workflows have been optimized for better performance
- Updated the "Product Version Compliance" monitor with the most recent version of public updates for SQL Server
- Updated display strings

### Bug Fixes

- Fixed an issue with the failing "ROWS Data Free Space Left" monitor and "Always On Custom User Policy" workflows in cases when a non-default RunAs account is used
- Fixed an issue with the failing dashboard view in cases when the 'OperationsManagerDW' database is used by several management groups
- Fixed an issue when the "Linux Availability Group" tiles might appear unavailable in the dashboard view
- Fixed an issue with the failing event rule "The agent is suspect. No response within last minutes" on Windows
- Fixed an issue with an invalid type of the 'Timeout' override in seconds for several workflows on Windows
- Fixed an issue with the "Local DB Engine" discovery error handling in cases when the SQL Server instance was deleted, but some namespaces remained in the registry
- Fixed an issue with the failing 'EventLogReader' module in localized OS

## February 2022 - 7.0.36.0 RTM

### What's New

- Updated the "Product Version Compliance" monitor with the most recent version of public updates for SQL Server

### Bug Fixes

- Fixed an issue with the failing 'MultiValueSpaceHealthCalculator' module on localized operating systems where SQL Server is installed
- Fixed an issue with the failing 'LocalDBEngineDiscovery' module in environments, in which both x64 and x86 versions of SQL Server are installed

## December 2021 - 7.0.34.0 RTM

### What's New

- Added a new 'Health Calculation Mode' override for space monitoring workflows targeted to databases. This override allows you to define how you want to monitor free space in your environment. You can now track the health state based on the 'Threshold' parameter expressed as a percentage term (%) or as a capacity metric (MB). The override is added to the following monitors: "LOG Free Space Left", "ROWS Data Free Space Left", "FILESTREAM Data Free Space Left", "In-Memory OLTP Data Free Space Left"
- Added a new 'Timeout for query execution' override to the following performance rules: "Memory Used By Indexes (MB)" and "Memory Used By Tables (MB)". These rules are now disabled by default to avoid the extra load in environments with a large number of memory-optimized databases
- Added 'MachineName' and 'InstanceName' alert parameters to all workflows targeted to DB Engine
- Added an alert for the "Automatic setup of DB Engine discovery filter" rule
- Added a new 'Available space in MB terms' property to the "LOG Free Space Left" monitor
- Updated the "Summary Dashboard" view. Now the "SQL Server Reporting Services" tiles are combined as Instances and Deployments
- Updated the "Product Version Compliance" monitor with the most recent version of public updates for SQL Server
- Optimized performance metric collection
- Updated display strings

### Bug Fixes

- Fixed an issue with the failing discovery modules after upgrading SQL Server
- Fixed an issue with free space calculations in cases when 'Autogrowth' is enabled for the database
- Fixed an issue with the failing discovery modules in cases when Availability Group has a replica with the 'Allow read/write connections' setting
- Fixed an issue with duplicates in the list of securables for the "Securables Configuration Status" monitor targeted to the database
- Fixed an issue with not working Operations Manager console tasks (run "SQL Management Studio", run "SQL Profiler") with the latest versions of SQL Server Management Studio
- Fixed an issue with not working Operations Manager console tasks in clustered environments. Now tasks "Start Analysis Service" and "Stop Analysis Service" work properly

## June 2021 - 7.0.32.0 RTM

### What's New

- Updated override for the "Service Principal Name Configuration Status" monitor. The ‘Interval’ value is now set to 3600 (1 hour) to avoid an alert storm in multiple domain controller environments
- Updated the "Virtual Log File Count" monitor. Now it uses the ‘sys.dm_db_log_info’ view instead of DBCC on SQL Server 2016 and higher
- Updated the "Database Status" monitor. Added a new override ‘Disable if Availability Group is offline’ to avoid false positives in high-availability environments
- Updated the "Database Backup Status" monitor. Added a new override ‘Track Availability Group Backup Preferences' to instruct the monitor to track the backup location configured in the Availability Group backup preferences
- Added a new exclude list option for the "SQL Server Agent Job" discovery
- Updated overrides for the "WMI Health State" monitor. The ‘Interval’ value is now set to 3600 (1 hour) and the ‘Samples count’ value is set to 2
- Renamed some Dashboard tiles
- Added new rules targeted to the SQL Server Agent Job: "SQL Server Agent Job Duration Alert Rule" and "SQL Server Agent Job Duration" performance rule
- Updated the following space related discoveries: "DB Filegroups", "DB Files", "Transaction Log File", "FILESTREAM Filegroups", "Memory-Optimized Data Filegroup", and "Memory-Optimized Data Filegroup Containers". Now they are disabled by default to reduce the load on the environment
- Updated the "Summary Dashboard" views. Now they also contain tiles for the SQL Server Integration Services
- Updated the "Product Version Compliance" monitor with the most recent version of the public updates for SQL Server
- Updated display strings

### Bug Fixes

- Fixed an issue with continuous login attempts from passive SQL Server cluster node after the failover
- Fixed an issue with the failing "SQL Server Agent Jobs" discovery in cases of unsupported ASCII characters in job names by adding proper error handling
- Fixed performance data collection for SQL Server DB Engines with Latin1_General_CP850_BIN collations
- Fixed an issue with the incorrect alert name for the "LOG Free Space Left" monitor
- Fixed an issue with the "Blocking Sessions" monitor that was enabled by default
- Fixed an issue with the lost 'Timeout' override for the "WMI Health State" monitor
- Fixed an issue with the wrong alert parameter reference in the "Summary Dashboard" view tiles

## August 2020 - 7.0.24.0 RTM

### What's New

- Added a new "Securables Configuration Status" monitor targeted to SQL Server databases
- Updated the "Product Version Compliance" monitor with the most recent version of public updates for SQL Server
- Updated the "Securables Configuration Status" monitor targeted to the DB Engine when a SQL Server instance participates in Availability Groups
- Removed the "Securables Configuration Status" monitor targeted to the Availability Replica as non-useful
- Updated the "SQL Server Database Engines" discovery; the "Netbios Computer Name" property is now uppercased.
- Added reports from version-specific management packs for SQL Server
- Updated monitor "Job Duration" to add current job run's duration to its alert description
- Updated Web Console version of SQL MP Dashboards to support System Center Operations Manager 2019 UR1
- Updated monitor "Product Version Compliance" with versions of most recent public updates to SQL Server
- Updated data source of alerting rules to avoid alert storm after exiting maintenance mode
- Updated alert description of monitor "Securables Configuration Status"
- Added "CheckStartupType" property to the SQL Server Integration Services Health Status monitor
- Revised columns of SQL Agent and SQL Agent Jobs state views
- Updated display strings

### Bug Fixes

- Fixed the Alerting Rules data source to avoid an alert storm after exiting maintenance mode
- Fixed the SQL Log Reader data source to support changing of the SQL Authentication method
- Fixed the Performance Reader data source to support changing of the SQL Authentication method
- Fixed issue in data source of SPN Status monitor that may lead to memory leak
- Fixed error "Unsupported path format" in workflows targeting Filegroups
- Fixed discovery error on non-readable availability replicas
- Fixed wrong Run As profile in the SQL Server Integration Services Seed Discovery
- Fixed issue that caused rule "Disable Discovery of Selected DB Engines" to fail
- Fixed discovery issue for databases in recovering state
- Fixed issue in monitor "Securables Configuration Status" when it went critical on Shared-Memory-only SQL Servers

## December 2019 - 7.0.20.0 RTM

[Including changes made in the prior preview release — v.7.0.18, November 2019]

### What's New

- Updated MP to support SQL Server 2019 RTM
- Added filter by edition to "Local DB Engine Discovery"
- Redesigned DB Space monitoring to improve performance: Enabled by default monitors and performance rules targeting Database which watch for disk space consumption by ROWS Filegroups and Log files
- Redesigned DB Space monitoring: Added two monitors and two performance rules targeting Database to watch for disk space consumption by In-Memory and FILESTREAM data
- Redesigned DB Space monitoring: Read-only Filegroups now count as well
- Redesigned DB Space monitoring: Disabled by default all workflows targeting Filegroups, Files, Log files
- Redesigned XTP performance counters to make them completely version-agnostic
- Added attribute "TCP Port" to "SQL DB Engine Class" and updated "DB Engine Discovery" to populate the new property
- Added summary dashboard for System Center Operations Manager 2019 Web Console (HTML5)
- Added support for cluster nodes with disjoined namespaces
- Added sampling to algorithm of monitor "WMI Health State" in order to eliminate false alerting on cluster SQL Server instances
- Updated alert descriptions of monitors "Availability Database," "Availability Replica," and "Availability Group" (generating alerts still disabled by default)
- Updated monitor "Product Version Compliance" with versions of most recent public updates to SQL Server
- Disabled by default monitor "Buffer Cache Hit Ratio" and changed its threshold from 0% to 90%
- Disabled by default monitor "Page Life Expectancy"
- Removed monitors "Availability Database Join State" and "Availability Replica Join State" as not useful
- Updated display strings
- Revised columns on DB Engine state views

### Bug Fixes

- Fixed: monitor "Service Principal Name Configuration Status" raises false alerts because of case-sensitive comparison
- Fixed: "Local DB Engine Discovery" crashes when Windows has Turkish locale
- Fixed issue that caused performance degradation in workflows "General Always On Discovery," "Database Replica Discovery," and "Always On System Policy Monitoring"
- Fixed: "General Always On Discovery" throws errors on environments with several Distributed Availability Groups
- Fixed monitoring issue in case of Database is replicated by Always On Availability Group
- Fixed empty property bag when Availability Group has cluster type NONE
- Fixed wrong target in alerting rule "DB Backup Failed to Complete"
- Fixed rule "MSSQL Integration Services on Windows: The package restarted from checkpoint file" and its alert
- Fixed rule "OS Error occurred while performing I/O on pages" and its alert
- Fixed: "DB Disk Write Latency" and "DB Disk Read Latency" monitors and performance rules get wrong performance metric
- Fixed alert description of monitor "WMI Health State"
