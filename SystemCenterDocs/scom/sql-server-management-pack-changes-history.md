---
ms.assetid: 2973edd7-293f-496e-b4db-405d6438bb04
title: Features and enhancements in Management Pack for SQL Server
description: This article explains the new functionality and bug fixes implemented in Management Pack for SQL Server.
author: epomortseva
ms.author: v-gajeronika
ms.date: 06/30/2025
ms.topic: concept-article
ms.service: system-center
ms.subservice: operations-manager
ms.update-cycle: 1095-days
---

# Features and enhancements in Management Pack for SQL Server

This section covers new functionality and improvements in Management Pack for SQL Server.

## January 2026 - 7.12 RTM

### What's New

- Support for SQL Server 2025

  - Includes support for the following editions of SQL Server 2025 (Enterprise, Standard, Enterprise Developer, Standard Developer, Evaluation, and Express)
  
- Replaced Microsoft.Data.SqlClient with the System.Data.SqlClient 

- Reverts SQL Server Management Objects (SMO) to version 15

### Bug Fixes

- Fixed a bug where Availability Group monitors were not functioning as expected for some customers.

## July 2025 – 7.10.6 RTM

### What’s New

- Replaced System.Data.SqlClient with the Microsoft.Data.SqlClient data provider for SQL Server (MDS):
  - Actively maintained and enhanced by Microsoft.
  - Supports the latest protocols and features, including TDS 8.0, TLS 1.3, and Always Encrypted.

- Upgraded Microsoft SQL Server Management Objects (SMO) from version 15 to version 17, enabled by the migration to Microsoft.Data.SqlClient. This update brings numerous improvements and adds support for new SQL Server features.
- Added an "Only Running Jobs" override to the Job Duration monitor. This setting allows the monitor to measure either all jobs or only those currently running.
- Updated display strings.
- Updated the "Product Version Compliance" monitor with the latest public updates for SQL Server

### Bug Fixes

- Fixed an issue in the "Table Clustered Index Fragmentation" monitor caused by collation differences with the master database.

### Known Issues

- To maintain backward compatibility with prior versions, the parameter `TrustServerCertificate=true` is included in the connection string.

## January 2025 - 7.8.4 RTM

### What's new

- Added an [inclusion override](sql-server-management-pack-disabling-monitoring.md#disabling-monitoring-of-specified-sql-agent-jobs-by-name) for SQL Agent Job discovery

### Bug fixes and improvements

- Improved performance:
  - Reimplemented SyncTime handling for cookdown data sources, some monitors and discoveries
- Included database name in the "Blocking sessions" monitor alert
- Fixed an issue with the Wizard where a screen reader did not automatically announce the displayed error information after a table row failed to load
- Updated the "Product Version Compliance" monitor with the latest public updates for SQL Server
- Updated display strings

## July 2024 - 7.6.5 RTM

### What's New

- Added new "Table Clustered Index Fragmentation" monitor that targets databases and checks for high fragmentation of clustered indexes
- Added support for custom database monitoring with two options depending on the type of query: database context or cookdown
- Added new "Property Bag" step in the custom monitor setup to extend the alert context with properties from the query result
- Updated the "Product Version Compliance" monitor with the most recent version of public updates for the SQL Server
- Reworked the "Long Running Queries" alert rule to improve security
- Improved accessibility for the Summary Dashboard view and Monitoring Wizard template, including the following major changes:
  - implemented [Keyboard Navigation](sql-server-dashboards-management-pack-instance-dashboard-navigation.md) using the A and D buttons on the tiles in the dashboard
  - added the ability for the screen reader to announce buttons and errors in the SQL Server wizard
  - redesigned dashboard list controls for greater accessibility

## January 2024 - 7.4.0.0 RTM

### What's new

- Added support for [custom management server resource pools](sql-server-management-pack-sql-server-monitoring-pool.md) for agentless monitoring mode
- Added new ["SQL Connection Encryption Certificate Status"](sql-server-management-pack-monitoring-configuration.md#sql-server-connection-encryption-certificate-monitoring) monitor for SQL Server on Linux, which targets Database Engine and checks if the server's transport layer security (TLS) certificate is valid
- Updated the "Product Version Compliance" monitor with the most recent version of public updates for the SQL Server
- Improved accessibility for the Summary Dashboard view and Monitoring Wizard template, including the following major changes:
  - improved keyboard navigation
  - improved color contrast in dashboards for better legibility
  - reworked high contrast theme for dashboards
  - added support for screen-reading software
- Updated display strings

### Bug fixes

- Fixed the issue of Summary Dashboard view not working in the System Center Operations Manager Console when operational and data warehouse databases are hosted on SQL Server version 2022

## July 2023 - 7.2.0.0 RTM

### What's new

- Updated the [custom monitoring](sql-server-management-pack-custom-monitor.md), which allows the creation of monitors and performance rules, now it's on the separate package installer
- Added a query execution and time synchronization schedule filtering mode for the custom monitoring
- Added the 'Number of samples' override to the "Availability Group Automatic Failover, Availability Group Online, Availability Replicas Data Synchronization, Availability Replicas Role, Availability Replicas Connection, and Synchronous Replicas Data Synchronization" unit monitors to help avoid alert storming
- Added new ["SQL Connection Encryption Certificate Status"](sql-server-management-pack-monitoring-configuration.md#sql-server-connection-encryption-certificate-monitoring) monitor, which targets the Database Engine and is capable to check the TLS certificate validation period in days and the certificate requirements for the SQL Server on Windows
- Added new ["TDE Certificate Backup Status"](sql-server-management-pack-monitoring-configuration.md#transparent-data-encryption-tde-certificate-backup-status-monitoring) monitor, which targets the Database and is capable to check that the certificate used for encrypting the database encryption key hasn't been backed up
- Added new [Operations Manager console task](sql-server-management-pack-export-event-log-task.md), which allows saving and transport of the Event Log file from the Agent machine to the Management Server
- Extended the ["Long Running Queries"](sql-server-management-pack-monitoring-configuration.md#long-running-queries-monitoring) alerting rule by adding the Application, Database, and Query exclude list overrides, which are capable to exclude queries by the application name, database name, or the custom query text from the rule alerting
- Improved the [diagnostic tracing](/troubleshoot/system-center/scom/use-diagnostic-tracing) in the System Center Operations Manager toolset
- Improved the ["Database Files Space Usage Forecast"](sql-server-management-pack-sql-server-reporting.md) report by adding the number of days for the forecast summary
- Updated the "Product Version Compliance" monitor with the most recent version of public updates for the SQL Server
- Updated display strings

### Bug fixes

- Fixed an issue with false-negative alerts from the Availability Group rollup monitors, now the "Availability Group Automatic Failover (rollup), Availability Replica Role (rollup), Availability Replicas Connection (rollup), and Synchronous Replicas Data Synchronization (rollup)" have the best state of any member rollup algorithm
- Fixed an issue with the inability to launch the custom monitoring without the registry keys for unsigned modules
- Fixed an issue with the wrong average free space in percentage terms in the "Database Files Space Usage Forecast" report
- Fixed accessibility issues

## December 2022 - 7.0.42.0 RTM

### What's new

- Added support for the SQL Server 2022
- Added [custom monitoring](sql-server-management-pack-custom-monitor.md), which allows the creation of monitors and performance rules
- Added new "Availability Database Log Backup Status" monitor, which allows to track the alert backups in databases participated in Availability Groups
- Added new Operations Manager console tasks, which allow running the Discovery process on demand: "Run On-Demand Agent Job Discovery" and "Run On-Demand Database Discovery"
- Updated the Agent Job "Last Run Status" monitor by adding new overrides: 'Number of fails threshold', which determines the number of the job fails to change the monitor's status, and the 'Define the Canceled status as Failed', which could track the canceled job's last run status as a Failed
- Added new Agent "Job Duration" performance collection rule, which collects the duration of the SQL Server Agent job in minutes, for Windows and Linux platforms
- Added new Agent "Job Duration" alerting rule, which throws an alert if the execution time of any of SQL Agent jobs has exceeded the specified threshold in minutes, for Windows and Linux platforms
- Updated the "Securables Configuration Status" monitor by removing the unnecessary msdb.dbo.sp_help_jobactivity securable and by adding new msdb.dbo.sysjobactivity, msdb.dbo.sysjobhistory, msdb.dbo.syssessions, and msdb.dbo.agent_datetime securables
- Updated the "Low Privilege Monitoring" and the "Service SID" operations guide sections with updated T-SQL scripts for least-privileged configurations
- Added new "DB Log Bytes Flushed per Second, DB Log Flushes per Second, and DB Log Flush Wait Time" performance collection rules to measure the latency or investigate the I/O performance of a log device, for Windows and Linux platforms
- Added new "Long Running Queries" alerting rule, which throws an alert if the execution time of any of the running SQL queries has exceeded the specified threshold in seconds, for Windows and Linux platforms
- Added new "Database Engine Disk Write Latency" and the "Database Engine Disk Read Latency" monitors to track the read/write latency issues at the Database Engine level
- Always On discovery and monitoring workflows have been optimized for better performance
- Policy discovery workflows have been optimized for better performance
- Updated space monitoring workflows to apply four-significant digit rounding in all the values
- Updated the "Product Version Compliance" monitor with the most recent version of public updates for the SQL Server
- Updated display strings

### Bug fixes

- Fixed a performance issue with the "Service Principal Name Configuration Status" monitor by reducing the load on the domain controller in large environments
- Fixed an issue with the "Thread Count" monitor and the performance rule. Now these workflows count free threads more precisely including only the 'VISIBLE ONLINE' schedulers
- Fixed an issue with the "Database Status" monitor in cases when the database, hosted on the Primary Replica of an Availability Group, has an issue with its state, the monitor doesn't change its state for that database and becomes Healthy
- Fixed an issue with showing the full SQL query instead of the path in the System Center Operations Manager diagnostic tracing toolset

## June 2022 - 7.0.38.0 RTM

### What's new

- Added 'Timeout for query execution (seconds)' override, which can now be used in all workflows
- Added 'Number of samples' override to the "Database Status" monitor to help avoid alert storming
- Added support for the SQL Server 2022 public preview
- Added support for enabling debug logging in Windows Event Log
- Added support for enabling [diagnostic tracing](/troubleshoot/system-center/scom/use-diagnostic-tracing) in the System Center Operations Manager toolset
- The SQL Server Evaluation edition can now be added to the exclude list of the "Local Database Engine" discovery
- Monitoring workflows have been optimized for better performance
- Updated the "Product Version Compliance" monitor with the most recent version of public updates for SQL Server
- Updated display strings

### Bug fixes

- Fixed an issue with the failing "ROWS Data Free Space Left" monitor and "Always On Custom User Policy" workflows in cases when a nondefault RunAs account is used
- Fixed an issue with the failing dashboard view in cases when the 'OperationsManagerDW' database is used by several management groups
- Fixed an issue when the "Linux Availability Group" tiles might appear unavailable in the dashboard view
- Fixed an issue with the failing event rule "The agent is suspect. No response within last minutes" on Windows
- Fixed an issue with an invalid type of the 'Timeout' override in seconds for several workflows on Windows
- Fixed an issue with the "Local Database Engine" discovery error handling in cases when the SQL Server instance was deleted, but some namespaces remained in the registry
- Fixed an issue with the failing 'EventLogReader' module in localized operating systems

## February 2022 - 7.0.36.0 RTM

### What's new

- Updated the "Product Version Compliance" monitor with the most recent version of public updates for SQL Server

### Bug fixes

- Fixed an issue with the failing 'MultiValueSpaceHealthCalculator' module on localized operating systems where SQL Server is installed
- Fixed an issue with the failing 'LocalDBEngineDiscovery' module in environments, in which both x64 and x86 versions of SQL Server are installed

## December 2021 - 7.0.34.0 RTM

### What's new

- Added a new 'Health Calculation Mode' override for space monitoring workflows targeted to databases. This override allows you to define how you want to monitor free space in your environment. You can now track the health state based on the 'Threshold' parameter expressed as a percentage term (%) or as a capacity metric (MB). The override is added to the following monitors: "LOG Free Space Left, ROWS Data Free Space Left, FILESTREAM Data Free Space Left, In-Memory OLTP Data Free Space Left"
- Added a new 'Timeout for query execution' override to the following performance rules: "Memory Used By Indexes (MB) and Memory Used By Tables (MB)". These rules are now disabled by default to avoid the extra load in environments with a large number of memory-optimized databases
- Added 'MachineName' and 'InstanceName' alert parameters to all workflows targeted to Database Engine
- Added an alert for the "Automatic setup of Database Engine discovery filter" rule
- Added a new 'Available space in MB terms' property to the "LOG Free Space Left" monitor
- Updated the "Summary Dashboard" view. Now the "SQL Server Reporting Services" tiles are combined as Instances and Deployments
- Updated the "Product Version Compliance" monitor with the most recent version of public updates for SQL Server
- Optimized performance metric collection
- Updated display strings

### Bug fixes

- Fixed an issue with the failing discovery modules after upgrading SQL Server
- Fixed an issue with free space calculations in cases when 'Autogrowth' is enabled for the database
- Fixed an issue with the failing discovery modules in cases when Availability Group has a replica with the 'Allow read/write connections' setting
- Fixed an issue with duplicates in the list of securables for the "Securables Configuration Status" monitor targeted to the database
- Fixed an issue with not working Operations Manager console tasks (run SQL Management Studio, run SQL Profiler) with the latest versions of SQL Server Management Studio
- Fixed an issue with not working Operations Manager console tasks in clustered environments. Now tasks Start Analysis Service and Stop Analysis Service work properly

## June 2021 - 7.0.32.0 RTM

### What's new

- Updated override for the "Service Principal Name Configuration Status" monitor. The 'Interval' value is now set to 3600 (1 hour) to avoid an alert storm in multiple domain controller environments
- Updated the "Virtual Log File Count" monitor. Now it uses the 'sys.dm_db_log_info' view instead of Database Console Commands on SQL Server 2016 and higher
- Updated the "Database Status" monitor. Added a new override 'Disable if Availability Group is offline' to avoid false positives in high-availability environments
- Updated the "Database Backup Status" monitor. Added a new override ‘Track Availability Group Backup Preferences' to instruct the monitor to track the backup location configured in the Availability Group backup preferences
- Added a new exclude list option for the "SQL Server Agent Job" discovery
- Updated overrides for the "WMI Health State" monitor. The 'Interval' value is now set to 3600 (1 hour) and the 'Samples count' value is set to 2
- Renamed some Dashboard tiles
- Added new rules targeted to the SQL Server Agent Job: "SQL Server Agent Job Duration Alert Rule" and "SQL Server Agent Job Duration" performance rule
- Updated the following space related discoveries: "DB Filegroups, DB Files, Transaction Log File, FILESTREAM Filegroups, Memory-Optimized Data Filegroup, and Memory-Optimized Data Filegroup Containers". Now they're disabled by default to reduce the load on the environment
- Updated the "Summary Dashboard" views. Now they also contain tiles for the SQL Server Integration Services
- Updated the "Product Version Compliance" monitor with the most recent version of the public updates for SQL Server
- Updated display strings

### Bug fixes

- Fixed an issue with continuous login attempts from passive SQL Server cluster node after the failover
- Fixed an issue with the failing "SQL Server Agent Jobs" discovery in cases of unsupported ASCII characters in job names by adding proper error handling
- Fixed performance data collection for SQL Server Database Engines with Latin1_General_CP850_BIN collations
- Fixed an issue with the incorrect alert name for the "LOG Free Space Left" monitor
- Fixed an issue with the "Blocking Sessions" monitor that was enabled by default
- Fixed an issue with the lost 'Timeout' override for the "WMI Health State" monitor
- Fixed an issue with the wrong alert parameter reference in the "Summary Dashboard" view tiles

## August 2020 - 7.0.24.0 RTM

### What's new

- Added a new "Securables Configuration Status" monitor targeted to SQL Server databases
- Updated the "Product Version Compliance" monitor with the most recent version of public updates for SQL Server
- Updated the "Securables Configuration Status" monitor targeted to the Database Engine when a SQL Server instance participates in Availability Groups
- Removed the "Securables Configuration Status" monitor targeted to the Availability Replica as nonuseful
- Updated the "SQL Server Database Engines" discovery; the "Netbios Computer Name" property is now uppercased
- Added reports from version-specific management packs for SQL Server
- Updated monitor "Job Duration" to add current job run's duration to its alert description
- Updated Web Console version of SQL MP Dashboards to support System Center Operations Manager 2019 UR1
- Updated monitor "Product Version Compliance" with versions of most recent public updates to SQL Server
- Updated data source of alerting rules to avoid alert storm after exiting maintenance mode
- Updated alert description of monitor "Securables Configuration Status"
- Added "CheckStartupType" property to the SQL Server Integration Services Health Status monitor
- Revised columns of SQL Agent and SQL Agent Jobs state views
- Updated display strings

### Bug fixes

- Fixed the Alerting Rules data source to avoid an alert storm after exiting maintenance mode
- Fixed the SQL Log Reader data source to support changing of the SQL Authentication method
- Fixed the Performance Reader data source to support changing of the SQL Authentication method
- Fixed issue in data source of Service Principal Name Status monitor that may lead to memory leak
- Fixed error "Unsupported path format" in workflows targeting filegroups
- Fixed discovery error on nonreadable availability replicas
- Fixed wrong Run As profile in the SQL Server Integration Services Seed Discovery
- Fixed issue that caused rule "Disable Discovery of Selected Database Engines" to fail
- Fixed discovery issue for databases in recovering state
- Fixed issue in monitor "Securables Configuration Status" when it went critical on Shared-Memory-only SQL Servers

## December 2019 - 7.0.20.0 RTM

[Including changes made in the prior preview release 7.0.18, November 2019]

### What's new

- Updated MP to support SQL Server 2019
- Added filter by edition to "Local Database Engine Discovery"
- Redesigned DB Space monitoring to improve performance: Enabled by default monitors and performance rules targeting Database, which watch for disk space consumption by ROWS filegroups and log files
- Redesigned DB Space monitoring: Added two monitors and two performance rules targeting Database to watch for disk space consumption by In-Memory and FILESTREAM data
- Redesigned DB Space monitoring: Read-only filegroups now count as well
- Redesigned DB Space monitoring: Disabled by default all workflows targeting filegroups, files, Log files
- Redesigned XTP performance counters to make them completely version-agnostic
- Added attribute "TCP Port" to "SQL Database Engine Class" and updated "Database Engine Discovery" to populate the new property
- Added summary dashboard for System Center Operations Manager 2019 Web Console (HTML5)
- Added support for cluster nodes with disjoined namespaces
- Added sampling to algorithm of monitor "WMI Health State" in order to eliminate false alerting on cluster SQL Server instances
- Updated alert descriptions of monitors "Availability Database," "Availability Replica," and "Availability Group" (generating alerts still disabled by default)
- Updated monitor "Product Version Compliance" with versions of most recent public updates to SQL Server
- Disabled by default monitor "Buffer Cache Hit Ratio" and changed its threshold from 0% to 90%
- Disabled by default monitor "Page Life Expectancy"
- Removed monitors "Availability Database Join State" and "Availability Replica Join State" as not useful
- Updated display strings
- Revised columns on Database Engine state views

### Bug fixes

- Fixed: monitor "Service Principal Name Configuration Status" raises false alerts because of case-sensitive comparison
- Fixed: "Local Database Engine Discovery" crashes when Windows has Turkish locale
- Fixed issue that caused performance degradation in workflows "General Always On Discovery," "Database Replica Discovery," and "Always On System Policy Monitoring"
- Fixed: "General Always On Discovery" throws errors on environments with several Distributed Availability Groups
- Fixed monitoring issue in case of Database is replicated by Always On Availability Group
- Fixed empty property bag when Availability Group has cluster type NONE
- Fixed wrong target in alerting rule "DB Backup Failed to Complete"
- Fixed rule "MSSQL Integration Services on Windows: The package restarted from checkpoint file" and its alert
- Fixed rule "OS Error occurred while performing I/O on pages" and its alert
- Fixed: "DB Disk Write Latency" and "DB Disk Read Latency" monitors and performance rules get wrong performance metric
- Fixed alert description of monitor "WMI Health State"
