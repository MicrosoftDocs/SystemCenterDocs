---
ms.assetid: 8e379e26-a604-4976-88ff-d291c48b8700
title: Features and enhancements in Management Pack for SQL Server Analysis Services
description: This article explains the new functionality and bug fixes implemented in Management Pack for SQL Server Analysis Services
author: epomortseva
ms.author: v-ekaterinap
manager: evansma
ms.date: 7/5/2023
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Features and enhancements in Management Pack for SQL Server Analysis Services

This article covers new functionality and improvements in Management Pack for SQL Server Analysis Services.

## July 2023 - 7.2.0.0 RTM

### What's new

- Added new threshold overrides in percentage terms for the "Vertipaq memory consumed by SSAS Instance" monitor, now the monitor is capable to check the Vertipaq memory allocations by Analysis Services instance in gigabytes and percentage terms with the 'Health Calculation Mode' override
- Added new "VertiPaq Memory Usage on the Server (%)" performance collection rule which collects total VertiPaq memory usage in percentage terms from either limit or available memory on the server where the Analysis Services instance is installed
- Added new "VertiPaq Memory Usage on the Server (GB)" performance collection rule which collects total VertiPaq memory usage in gigabytes on the server where the Analysis Services instance is installed
- Added a new "Product Version Compliance" monitor which is capable to check the product version number of the current SQL Server instance to determine that instance is up-to-date
- Added new [Operations Manager console task](analysis-services-management-pack-monitoring-configuration.md#tasks-overview), which allows saving and transport of the Event Log file from the Agent machine to the Management Server
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
- Updated memory and space monitoring workflows to apply four significant digit rounding in all the values
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
