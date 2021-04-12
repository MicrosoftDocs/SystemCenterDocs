---
ms.assetid: 2973edd7-293f-496e-b4db-405d6438bb04
title: Features and enhancements in Management Pack for SQL Server
description: This article explains the new functionality and bug fixes implemented in Management Pack for SQL Server
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Features and Enhancements in Management Pack for SQL Server

This section covers new functionality and improvements in Management Pack for SQL Server.

## August 2020 - 7.0.24.0 RTM

### What's New

- Added a new "Securables Configuration Status" monitor targeted to SQL Server databases
- Updated the "Product Version Compliance" monitor with the most recent version of public updates for SQL Server
- Updated the "Securables Configuration Status" monitor targeted to the DB Engine when a SQL Server instance participates in Availability Groups
- Removed the "Securables Configuration Status" monitor targeted to the Availability Replica as non-useful
- Updated the "SQL Server Database Engines" discovery; the “Netbios Computer Name” property is now uppercased.
- Updated display strings

### Bug Fixes

- Fixed the Alerting Rules data source to avoid an alert storm after exiting maintenance mode
- Fixed the SQL Log Reader data source to support changing of the SQL Authentication method
- Fixed the Performance Reader data source to support changing of the SQL Authentication method

## June 2020 - 7.0.23.0 CTP

### What's New

- Added reports from version-specific management packs for SQL Server
- Updated monitor “Job Duration” to add current job run's duration to its alert description
- Updated Web Console version of SQL MP Dashboards to support SCOM 2019 UR1
- Updated monitor “Product Version Compliance” with versions of most recent public updates to SQL Server
- Updated data source of alerting rules to avoid alert storm after exiting maintenance mode
- Updated alert description of monitor “Securables Configuration Status”
- Added “CheckStartupType” property to SSIS Health Status monitor
- Revised columns of SQL Agent and SQL Agent Jobs state views
- Updated display strings

### Bug Fixes

- Fixed issue in data source of SPN Status monitor that may lead to memory leak
- Fixed error “Unsupported path format” in workflows targeting Filegroups
- Fixed discovery error on non-readable availability replicas
- Fixed wrong Run As profile in SSIS Seed Discovery
- Fixed issue that caused rule “Disable Discovery of Selected DB Engines” to fail
- Fixed discovery issue for databases in recovering state
- Fixed issue in monitor “Securables Configuration Status” when it went critical on Shared-Memory-only SQL Servers

## December 2019 - 7.0.20.0 RTM

[Including changes made in the prior preview release — v.7.0.18, November 2019.]

### What's New

- Updated MP to support SQL Server 2019 RTM
- Added filter by edition to “Local DB Engine Discovery”
- Redesigned DB Space monitoring to improve performance: Enabled by default monitors and performance rules targeting Database which watch for disk space consumption by ROWS Filegroups and Logfiles
- Redesigned DB Space monitoring: Added two monitors and two performance rules targeting Database to watch for disk space consumption by In-Memory and FILESTREAM data
- Redesigned DB Space monitoring: Read-only filegroups now count as well
- Redesigned DB Space monitoring: Disabled by default all workflows targeting Filegroups, Files, Logfiles
- Redesigned XTP performance counters to make them completely version-agnostic
- Added attribute “TCP Port” to “SQL DB Engine Class” and updated “DB Engine Discovery” to populate the new property
- Added summary dashboard for SCOM 2019 Web Console (HTML5)
- Added support for cluster nodes with disjoined namespaces
- Added sampling to algorithm of monitor “WMI Health State” in order to eliminate false alerting on cluster SQL Server instances
- Updated alert descriptions of monitors “Availability Database,” “Availability Replica,” and “Availability Group” (generating alerts still disabled by default)
- Updated monitor “Product Version Compliance” with versions of most recent public updates to SQL Server
- Disabled by default monitor “Buffer Cache Hit Ratio” and changed its threshold from 0% to 90%
- Disabled by default monitor “Page Life Expectancy”
- Removed monitors “Availability Database Join State” and “Availability Replica Join State” as not useful
- Updated display strings
- Revised columns on DB Engine state views

### Bug Fixes

- Fixed: monitor “Service Principal Name Configuration Status” raises false alerts because of case-sensitive comparison
- Fixed: “Local DB Engine Discovery” crashes when Windows has Turkish locale
- Fixed issue that caused performance degradation in workflows “General Always On Discovery,” “Database Replica Discovery,” and “Always On System Policy Monitoring”
- Fixed: “General Always On Discovery” throws errors on environments with several Distributed Availability Groups
- Fixed monitoring issue in case of Database is replicated by Always On Availability Group
- Fixed empty property bag when Availability Group has cluster type NONE
- Fixed wrong target in alerting rule “DB Backup Failed to Complete”
- Fixed rule “MSSQL Integration Services on Windows: The package restarted from checkpoint file” and its alert
- Fixed rule “OS Error occurred while performing I/O on pages“ and its alert
- Fixed: "DB Disk Write Latency" and "DB Disk Read Latency" monitors and performance rules get wrong performance metric
- Fixed alert description of monitor “WMI Health State”
