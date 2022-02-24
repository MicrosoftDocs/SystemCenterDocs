---
ms.assetid: 2973edd7-293f-496e-b4db-405d6438bb04
title: Features and enhancements in Management Pack for SQL Server
description: This article explains the new functionality and bug fixes implemented in Management Pack for SQL Server
author: TDzakhov
ms.author: v-tdzakhov
manager: evansma
ms.date: 2/4/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Features and Enhancements in Management Pack for SQL Server

This section covers new functionality and improvements in Management Pack for SQL Server.

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
- Fixed an issue with the failing "SQL Server Agent Jobs" discovery in cases of unsupported ASCII characters in job names&mdash;added proper error handling
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
- Added "CheckStartupType" property to SSIS Health Status monitor
- Revised columns of SQL Agent and SQL Agent Jobs state views
- Updated display strings

### Bug Fixes

- Fixed the Alerting Rules data source to avoid an alert storm after exiting maintenance mode
- Fixed the SQL Log Reader data source to support changing of the SQL Authentication method
- Fixed the Performance Reader data source to support changing of the SQL Authentication method
- Fixed issue in data source of SPN Status monitor that may lead to memory leak
- Fixed error "Unsupported path format" in workflows targeting Filegroups
- Fixed discovery error on non-readable availability replicas
- Fixed wrong Run As profile in SSIS Seed Discovery
- Fixed issue that caused rule "Disable Discovery of Selected DB Engines" to fail
- Fixed discovery issue for databases in recovering state
- Fixed issue in monitor "Securables Configuration Status" when it went critical on Shared-Memory-only SQL Servers

## December 2019 - 7.0.20.0 RTM

[Including changes made in the prior preview release — v.7.0.18, November 2019.]

### What's New

- Updated MP to support SQL Server 2019 RTM
- Added filter by edition to "Local DB Engine Discovery"
- Redesigned DB Space monitoring to improve performance: Enabled by default monitors and performance rules targeting Database which watch for disk space consumption by ROWS Filegroups and Logfiles
- Redesigned DB Space monitoring: Added two monitors and two performance rules targeting Database to watch for disk space consumption by In-Memory and FILESTREAM data
- Redesigned DB Space monitoring: Read-only filegroups now count as well
- Redesigned DB Space monitoring: Disabled by default all workflows targeting Filegroups, Files, Logfiles
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
