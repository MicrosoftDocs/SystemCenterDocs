---
ms.assetid: 8e379e26-a604-4976-88ff-d291c48b8700
title: Features and enhancements in Management Pack for SQL Server Analysis Services
description: This article explains the new functionality and bug fixes implemented in Management Pack for SQL Server Analysis Services
author: epomortseva
ms.author: v-ekaterinap
manager: evansma
ms.date: 12/27/2022
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Features and Enhancements in Management Pack for SQL Server Analysis Services

This article covers new functionality and improvements in Management Pack for SQL Server Analysis Services.

## December 2022 - 7.0.42.0 RTM

### What's New

- Added support for the SQL Server 2022 RTM
- Added a new 'SQL Server Editions' exclude list override option for the Multidimensional, PowerPivot, and Tabular instance discoveries
- Added a new 'SQL Server Versions' exclude list override option for the Multidimensional, PowerPivot, and Tabular instance discoveries
- Added a new 'Exclude list' override option for the "Multidimensional DB" and the "Tabular DB" discoveries
- Added support for enabling debug logging in Windows Event Log
- Updated memory and space monitoring workflows to apply four significant digit rounding in all the values
- Discovery and monitoring workflows have been optimized for better performance
- Updated display strings

### Bug Fixes

- Fixed an issue with failing the 'MultidimensionalPartitionPropertyCD' discovery module in case Analysis Services instance is stopped

## June 2022 - 7.0.38.0 RTM

### What's New

- Extended monitoring for VertiPaq memory by adding a new "Tabular database consumes too much VertiPaq memory" monitor and the "Database VertiPaq Memory Size (GB)" performance rule
- Extended monitoring for PBI report rendering by adding a new "Memory consumed by running reports" monitor and the "Total memory usage by running reports on Server (GB)" performance rule
- Improved rounding of values in alerts from memory-related workflows: "Memory configuration conflict with SQL Server" and "Non SSAS-related processes consume too much memory"
- Added support for the SQL Server 2022 public preview
- Updated display strings

## December 2021 - 7.0.34.0 RTM

### What's New

- Improved alert generation by adding the machine name to the 'Source' path in the alerts view
- Updated display strings

### Bug Fixes

- Fixed an issue with not working System Center Operations Manager console tasks in clustered environments. Now tasks "Start Analysis Service" and "Stop Analysis Service" work properly.

## June 2021 - 7.0.32.0 RTM

### What's New

- Improved performance of Discovery and Monitoring workflows

### Bug Fixes

- Fixed an issue with failing space monitoring workflows for the Analysis Services database with a custom storage location  

## December 2020 - 7.0.29.0 RTM

### What's New

- Improved performance of partition discovery for multidimensional databases
- Updated and improved System Center Operations Manager 2019 HTML Dashboards to display the SQL Server Analysis Services health and alerts

## June 2020 - 7.0.22.0 RTM

### Bug Fixes

- Added tasks Start/Stop Analysis Services Windows Service
- Updated display strings

## December 2019 - 7.0.19.0 CTP

### What's New

- Added support for SQL Server Analysis Services 2012, 2014, and 2016 in addition to previously supported 2017 and higher
- Implemented Database Status monitor
- Updated display strings

## October 2018 - 7.0.10.0 RTM

### What's New

- Replaced the Core Library in the delivery with the version 7.0.7.0, that version, which is delivered with the most recent RTM version of the management pack for SQL Server 2017+
- Improved displaying of the SQL Server Analysis Services instance version (now shows Patch Level version instead of Version)
- Added missed dependency monitors required to roll up the instance health appropriately
- Updated Summary dashboards
- Updated display strings

### Bug Fixes

- Fixed alert for "Partition Storage Free Space" monitor
