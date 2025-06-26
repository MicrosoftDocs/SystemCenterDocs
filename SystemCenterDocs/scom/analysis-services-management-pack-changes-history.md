---
ms.assetid: 8e379e26-a604-4976-88ff-d291c48b8700
title: Features and enhancements in Management Pack for SQL Server Analysis Services
description: This article explains the new functionality and bug fixes implemented in Management Pack for SQL Server Analysis Services
author: fkornilov
ms.author: v-vlchernov
manager: evansma
ms.date: 01/23/2025
ms.topic: concept-article
ms.service: system-center
ms.subservice: operations-manager
---

# Features and enhancements in Management Pack for SQL Server Analysis Services

This article covers new functionality and improvements in Management Pack for SQL Server Analysis Services.

## January 2025 - 7.8.3 RTM

### What's new

- Added automatic connection to non-default SQL Server instances when SQL Server Browser is not running.

### Bug fixes and improvements

- Improved the timeout overridable parameter handling to fix the issue with multiple instances of the same workflow running at the same time
- Improved performance and memory footprint
- Updated the "Product Version Compliance" monitor with the latest public updates for SQL Server

## July 2024 - 7.6.2 RTM

### What's New

- Added "VertiPaq memory paging indication" monitor to observe the level of VertiPaq memory paging
- Added Vertipaq tiles to Analysis Servises dashboards:
  - Monitor tiles: VertiPaq memory consumed by SSAS Instance and VertiPaq memory paging indication
 	- Perfomance tile: VertiPaq Memory Limit, VertiPaq Memory Limit(GB), VertiPaq Memory Usage on the Server (%), VertiPaq Memory Usage on the Server (GB), VertiPq Nonpaged Memory (GB) and VertiPaq Memory Paged (GB)
- Updated the "Product Version Compliance" monitor with the most recent version of public updates for the SQL Server
- Updated display strings

### Bug fixes

- Fixed an issue with alert message and monitor description for "VertiPaq memory consumed by SSAS Instance" monitor
- Fixed an issue with monitor triggers in mixed mode health calculation for the "VertiPaq memory consumed by SSAS instance" monitor
- Fixed an issue with "Memory consumed by other processes" monitor calculation

## January 2024 - 7.4.0.0 RTM

### What's new

- Added new "MDX Number of calculation covers" performance collection rule that collects total number of evaluation nodes built by MDX execution plans, including active and cached
- Added new "MDX total cells calculated" performance collection rule that collects the total number of cell properties
- Added new "MDX Total NON EMPTY for calculated members" performance collection rule that collects total number of times a NON EMPTY algorithm looped over calculated members
- Added new "MDX Total NON EMPTY unoptimized" performance collection rule that collects total number of times an unoptimized NON EMPTY algorithm was used
- Added new "MDX Total Recomputes" performance collection rule that collects total number of cells recomputed due to error
- Added new "MDX Total Sonar subcubes" performance collection rule that collects total number of subcubes that the query optimizer generated
- Added new "Processing Aggregations Rows created/sec" performance collection rule that collects rate of aggregation rows created during processing of aggregations in MOLAP data files
- Added new "Indexes Processing Rows/sec" performance collection rule that collects the number of rows per second being read from MOLAP stores to create indexes during a processing workload
- Added new "Processing Rows written/sec" performance collection rule that collects rate of rows written during processing of data
- Improved the memory-related instance monitoring workflows by adding new properties and removing deprecated ones
- Updated the "Product Version Compliance" monitor with the most recent version of public updates for the SQL Server Analysis Services
- Added support for enabling [diagnostic tracing](/troubleshoot/system-center/scom/use-diagnostic-tracing) in the System Center Operations Manager toolset
- Improved accessibility for the Summary Dashboard view and Monitoring Wizard template, including the following major changes:
  - improved keyboard navigation
  - improved color contrast in dashboards for better legibility
  - reworked high contrast theme for dashboards
  - added support of screen-reading software
- Updated display strings

### Bug fixes

- Fixed an issue with the failing "VertiPaq memory consumed by SSAS Instance" monitor in some configuration cases

## July 2023 - 7.2.0.0 RTM

### What's new

- Added new threshold overrides in percentage terms for the "VertiPaq memory consumed by SSAS Instance" monitor, now the monitor is capable to check the VertiPaq memory allocations by Analysis Services instance in gigabytes and percentage terms with the 'Health Calculation Mode' override
- Added new "VertiPaq Memory Usage on the Server (%)" performance collection rule that collects total VertiPaq memory usage in percentage terms from either limit or available memory on the server where the Analysis Services instance is installed
- Added new "VertiPaq Memory Usage on the Server (GB)" performance collection rule that collects total VertiPaq memory usage in gigabytes on the server where the Analysis Services instance is installed
- Added a new "Product Version Compliance" monitor that is capable to check the product version number of the current SQL Server instance to determine that instance is up-to-date
- Added new [Operations Manager console task](analysis-services-management-pack-tasks-overview.md), which allows saving and transport of the Event Log file from the Agent machine to the Management Server
- Updated display strings

### Bug fixes

- Fixed an issue with the inability to launch discovery and monitoring modules without the registry keys for unsigned modules

## December 2022 - 7.0.42.0 RTM

### What's new

- Added support for the SQL Server 2022 RTM
- Added a new 'SQL Server Editions' exclude list override option for the Multidimensional, PowerPivot, and Tabular instance discoveries
- Added a new 'SQL Server Versions' exclude list override option for the Multidimensional, PowerPivot, and Tabular instance discoveries
- Added a new 'Exclude list' override option for the "Multidimensional DB" and the "Tabular DB" discoveries
- Added support for enabling debug logging in Windows Event Log
- Updated memory and space monitoring workflows to apply four significant digit roundings in all the values
- Discovery and monitoring workflows have been optimized for better performance
- Updated display strings

### Bug fixes

- Fixed an issue with failing the 'MultidimensionalPartitionPropertyCD' discovery module in case Analysis Services instance is stopped

## June 2022 - 7.0.38.0 RTM

### What's new

- Extended monitoring for VertiPaq memory by adding a new "Tabular database consumes too much VertiPaq memory" monitor and the "Database VertiPaq Memory Size (GB)" performance rule
- Extended monitoring for PBI report rendering by adding a new "Memory consumed by running reports" monitor and the "Total memory usage by running reports on Server (GB)" performance rule
- Improved rounding of values in alerts from memory-related workflows: "Memory configuration conflict with SQL Server" and "Non SSAS-related processes consume too much memory"
- Added support for the SQL Server 2022 public preview
- Updated display strings

## December 2021 - 7.0.34.0 RTM

### What's new

- Improved alert generation by adding the machine name to the 'Source' path in the alerts view
- Updated display strings

### Bug fixes

- Fixed an issue with not working System Center Operations Manager console tasks in clustered environments. Now tasks "Start Analysis Service" and "Stop Analysis Service" work properly.

## June 2021 - 7.0.32.0 RTM

### What's new

- Improved performance of Discovery and Monitoring workflows

### Bug fixes

- Fixed an issue with failing space monitoring workflows for the Analysis Services database with a custom storage location  

## December 2020 - 7.0.29.0 RTM

### What's new

- Improved performance of partition discovery for multidimensional databases
- Updated and improved System Center Operations Manager 2019 HTML Dashboards to display the SQL Server Analysis Services health and alerts

## June 2020 - 7.0.22.0 RTM

### Bug fixes

- Added tasks Start/Stop Analysis Services Windows Service
- Updated display strings

## December 2019 - 7.0.19.0 CTP

### What's new

- Added support for SQL Server Analysis Services 2012, 2014, and 2016 in addition to previously supported 2017 and higher
- Implemented Database Status monitor
- Updated display strings

## October 2018 - 7.0.10.0 RTM

### What's new

- Replaced the Core Library in the delivery with the version 7.0.7.0, that version, which is delivered with the most recent RTM version of the management pack for SQL Server 2017+
- Improved displaying of the SQL Server Analysis Services instance version (now shows Patch Level version instead of Version)
- Added missed dependency monitors required to roll up the instance health appropriately
- Updated Summary dashboards
- Updated display strings

### Bug fixes

- Fixed alert for "Partition Storage Free Space" monitor
