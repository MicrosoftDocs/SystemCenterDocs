---
ms.assetid: d68fe81d-e14c-494f-b118-e9a421d551c1
title: Features and enhancements in Management Pack for SQL Server Reporting Services
description: This article explains the new functionality and bug fixes implemented in Management Pack for SQL Server Reporting Services
author: epomortseva
ms.author: v-vlchernov
manager: evansma
ms.date: 06/30/2025
ms.topic: concept-article
ms.service: system-center
ms.subservice: operations-manager
---

# Features and enhancements in Management Pack for SQL Server Reporting Services

This article covers new functionality and improvements in Management Pack for SQL Server Reporting Services.

## July 2025 – 7.10.4 RTM

### What’s New

- Replaced System.Data.SqlClient with the Microsoft.Data.SqlClient data provider for SQL Server (MDS):
  - Actively maintained and enhanced by Microsoft.
  - Supports the latest protocols and features, including TDS 8.0, TLS 1.3, and Always Encrypted.

- Included minor enhancements and routine maintenance updates to improve system stability and overall reliability.

- Updated the "Product Version Compliance" monitor with the latest public updates for SQL Server

### Known Issues

- To maintain backward compatibility with prior versions, the parameter `TrustServerCertificate=true` is included in the connection string.

## January 2025 - 7.8.2 RTM

### Bug fixes and improvements

- Updated the "Product Version Compliance" monitor with the latest public updates for SQL Server

## July 2024 - 7.6.1 RTM

### What's new

- Updated the "Product Version Compliance" monitor with the most recent version of public updates for the SQL Server Reporting Services
- Updated display strings

## January 2024 - 7.4.0.0 RTM

### What's new

- Updated the "Product Version Compliance" monitor with the most recent version of public updates for the SQL Server Reporting Services and Power BI Report Server
- Added new ["Securables Configuration Status"](reporting-services-management-pack-monitoring-configuration.md#securables-configuration-status-monitor) monitors targeted to SQL Server Reporting Services instance and Deployment Watcher that check if each of the required SQL Server securables is accessible under the configured Run As Account
- Added support for enabling [diagnostic tracing](/troubleshoot/system-center/scom/use-diagnostic-tracing) in the System Center Operations Manager toolset
- Improved accessibility for the Summary Dashboard view and Monitoring Wizard template, including the following major changes:
  - improved keyboard navigation
  - improved color contrast in dashboards for better legibility
  - reworked high contrast theme for dashboards
  - added support of screen-reading software
- Updated display strings

## July 2023 - 7.2.0.0 RTM

### What's new

- Added a new "Product Version Compliance" monitor which is capable to check the product version number  of the current SQL Server Reporting Services or Power BI Report Server to determine that instance is up-to-date
- Added new [Operations Manager console task](reporting-services-management-pack-tasks-overview.md), which allows saving and transport of the Event Log file from the Agent machine to the Management Server
- Extended "Failed Subscriptions" unit monitor to a 3-level state. Now the monitor raises a critical alert if the SQL Server Reporting Services or Power BI Report Server has subscriptions or scheduled refresh plans with failed statuses, otherwise, it raises a warning alert if the statuses are unknown (other than successful and failed)
- Updated display strings

## December 2022 - 7.0.42.0 RTM

### What's new

- Added a new feature group for the automated population of Power BI Report Services
- Added a new 'SQL Server Editions' exclude list override option for the instance discovery
- Added a new 'SQL Server Versions' exclude list override option for the instance discovery
- Added support for enabling debug logging in Windows Event Log
- Updated memory and space monitoring workflows to apply four significant digit rounding in all the values
- Updated display strings

### Bug fixes

- Fixed an issue with an increasing value of more than a hundred percent in the "CPU Utilization" monitor and the performance rule

## June 2022 - 7.0.38.0 RTM

### What's new

- Extended monitoring for Power BI Report Services report rendering by adding new performance rules – "Working set memory consumed by Power BI Mashup containers (GB)", "Private memory consumed by Power BI Mashup containers (GB)", "Working set memory consumed by Power BI Analysis Services process (GB)", "Private memory consumed by Power BI Analysis Services process (GB)"
- Added a new 'URL position' override that indicates which URL to use to monitor the availability of the Web service in the "Report manager accessible" and "Web service accessible" monitors
- Improved rounding of values in alerts from memory-related workflows: "Running SSRS processes consume too much memory" and "Non SSRS-related processes consume too much memory"
- Updated display strings

### Bug fixes

- Fixed an issue with collecting the wrong performance counter for the "Memory consumed by SSRS Instance" and "Memory consumed by other processes" monitors and for the "Memory consumed by SSRS (GB)" and "Memory consumed by other processes (%)" performance rules
- Fixed an issue when the 'Install Path' property might not appear in the instance discovery details view
- Fixed an issue with the failing 'RsProcessMetrics' module in some environments

## December 2021 - 7.0.34.0 RTM

### What's new

- Added a new "Failed Subscriptions" monitor that produces alerts if there are any failed Report Subscriptions or Scheduled Refresh Plans
- Improved alert generation by adding the machine name to the 'Source' path in the alerts view
- Updated the "Summary Dashboard" view. Now the 'SQL Server Reporting Services' tiles are combined as Instances and Deployments
- Updated display strings

## June 2021 - 7.0.32.0 RTM

### What's new

- Updated the 'Deployments' state view with the 'SQL Server Reporting Services Instances' column
- Updated display strings

## December 2020 - 7.0.29.0 RTM

### What's new

- Updated and improved System Center Operations Manager 2019 HTML Dashboards to display SQL Server Reporting Services health and alerts
- Updated alert description for Report Manager Accessible & Web Service Accessible monitors

## June 2020 - 7.0.22.0 RTM

### What's new

- Added tasks Start/Stop Reporting Services Windows Service
- Updated display name of SQL Server Reporting Services Deployment object to display Availability Group name as part of it instead of GUID
- Updated logic of installation detection for local Reporting Services instance to query Windows Registry instead of WMI
- Improved error handling for cases when error **Process with an Id is not running** is returned
- Updated display strings

### Bug fixes

- Fixed false alerting with status code 400 in monitor "Report Manager Accessible" for SQL Server Reporting Services 2016 and Power BI Report Services
- Fixed alert parameter replacement failure in monitor "Report Manager Accessible"
- Fixed issue with accessing 'DBConnectionString' property of Power BI Report Services

## December 2019 - 7.0.19.0 CTP

### What's new

- Added support for monitoring SQL Server Reporting Services 2012, 2014, and 2016 in addition to 2017 and higher
- Updated Event Log Collection Target Management Server Discovery to make it use default System Center Operations Manager action profile instead of SQL MP Discovery Run As profile
- Updated display strings

### Bug fixes

- Fixed 'NullReferenceException' error when Report Server portal being configured to have several ports

## April 2019 - 7.0.15.0 RTM

### What's new

- Supported last changes in version-agnostic management pack for SQL Server

## January 2019 - 7.0.12.0 RTM

### What's new

- Added support for Power BI Report Server

## October 2018 - 7.0.10.0 RTM

### What's new

- Replaced the Core Library in the delivery with the version 7.0.7.0, that version which is delivered with the most recent RTM version of the management pack for SQL Server 2017+
- Updated the monitoring of "Memory Consumption" and "CPU Usage" in order to collect performance data for all subprocesses in addition to the main SQL Server Reporting Services process
- Updated Summary dashboards
- Updated display strings

### Bug fixes

- Fixed minor issues found in the CTP version
