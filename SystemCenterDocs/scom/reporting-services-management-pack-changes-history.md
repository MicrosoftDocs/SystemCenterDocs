---
ms.assetid: d68fe81d-e14c-494f-b118-e9a421d551c1
title: Features and enhancements in Management Pack for SQL Server Reporting Services
description: This article explains the new functionality and bug fixes implemented in Management Pack for SQL Server Reporting Services
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 5/31/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Features and Enhancements in Management Pack for SQL Server Reporting Services

This section covers new functionality and improvements in Management Pack for SQL Server Reporting Services.

## June 2021 - 7.0.32.0 RTM

### What's New

- Updated the 'Deployments' state view with the 'SSRS Instances' column
- Updated display strings

## December 2020 - 7.0.29.0 RTM

- Updated and improved System Center Operations Manager 2019 HTML Dashboards to display SSRS health and alerts
- Updated alert description for Report Manager Accessible & Web Service Accessible monitors

## June 2020 - 7.0.22.0 RTM

### What's New

- Added tasks Start/Stop Reporting Services Windows Service
- Updated display name of SSRS Deployment object to display AG name as part of it instead of GUID
- Updated logic of installation detection for local Reporting Services instance to query Windows Registry instead of WMI
- Improved error handling for cases when error "Process with an Id is not running" is returned
- Updated display strings

### Bug Fixes

- Fixed false alerting with status code 400 in monitor Report Manager Accessible for SSRS 2016 and PBIRS
- Fixed alert parameter replacement failure in monitor Report Manager Accessible
- Fixed issue with accessing DBConnectionString property of PBIRS

## December 2019 - 7.0.19.0 CTP

### What's New

- Added support for monitoring SQL Server Reporting Services 2012, 2014, and 2016 in addition to 2017 and up
- Updated Event Log Collection Target Management Server Discovery to make it use default SCOM action profile instead of SQL MP Discovery run as profile
- Updated display strings

### Bug Fixes

- Fixed NullReferenceException error when Report Server portal being configured to have several ports

## April 2019 - 7.0.15.0 RTM

- Supported last changes in version-agnostic management pack for SQL Server

## January 2019 - 7.0.12.0 RTM

- Added support for Power BI Report Server

## October 2018 - 7.0.10.0 RTM

- Replaced the Core Library in the delivery with the version 7.0.7.0, that version which is delivered with the most recent RTM version of the management pack for SQL Server 2017+
- Updated the monitoring of Memory Consumption and CPU Usage in order to collect performance data for all subprocesses in addition to the main SSRS service process
- Updated Summary dashboards
- Fixed minor issues found in the CTP version
- Updated display strings