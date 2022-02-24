---
ms.assetid: e683af64-a4d0-4867-8941-3ac3419be3d9
title: Features and enhancements in Management Pack for Azure SQL Database
description: This article explains the new functionality and bug fixes implemented in Management Pack for Azure SQL Database
author: jyothisuri
ms.author: jsuri
manager: evansma
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Features and Enhancements in Management Pack for Azure SQL Database

This section covers new functionality and improvements in Management Pack for Azure SQL Database.

## October 2020 - 7.0.26.0 RTM

### What's New

- Added filtering list for SQL Servers and Databases to "Add Monitoring Wizard" template
- Removed deprecated workflows

### Bug Fixes

- Fixed issue with Elastic Pool performance data on vCore-based pricing tiers

## September 2020 - 7.0.25.0 CTP

### What's New

- Added support of vCore-based pricing tier
- Updated the token renewal algorithm to get rid of 401 responses
- Updated Core Library MP and the “Summary” Dashboard
- Updated display strings

### Bug Fixes

- Fixed an issue with an unnecessary slash symbol in some requests to Azure REST API
- Fixed monitoring issues for databases that are replicated by failover groups and elastic pools

## September 2019 - 7.0.5.0 private drop

### What's New

- Fixed issue: datediff used for Long Running Transactions monitoring results in overflow in some environments

## April 2018 - 7.0.4.0 RTM

### What's New

- Provided a few minor UI improvements to the Add Monitoring Wizard

### Bug Fixes

- Fixed issue: The management pack may stop working due to a conflict of the Azure REST API libraries with the ones coming from the Microsoft Azure Management Pack

## May 2017 - 6.7.28.0 RTM

### What's New

- Due to performance problems, several monitors and performance rules were enabled for getting information via T-SQL queries only (the affected metrics are as follows: Failed Connections, Blocked Connections, Successful Connections, Deadlocks Count)

### Bug Fixes

- Fixed Azure SQL DB: DB Transactions Locks Count rule and Transaction Locks Count monitor
- Fixed Azure SQL Database Event Log Collection Target Management Service Discovery
- Fixed Server Exclude list filter: servername could not contain whitespaces
- Fixed the display strings, implemented appropriate Azure portal naming style

## March 2017 - 6.7.25.0 CTP2

### What's New

- Implemented performance improvements
- Improved error handling in Add Monitoring Wizard

### Bug Fixes

- Fixed issue: "Collect Elastic Database Pool Number of Databases" rule does not collect performance data if REST monitoring is used
- Fixed issue: "Operations Manager Expression Filter Module" error messages appear in the Operations Manager event log

## December 2016 - 6.7.11.0 CTP1

### What's New

- Azure Resource Manager is now supported: the previous versions of the Management Pack used T-SQL queries to SQL Server system views to get information on the health and performance of the databases; now, the Management Pack can also get this information from Azure REST API (this is a preferred option)
- Multiple subscriptions and multiple servers are now supported
- Added support for Azure AD authentication
- Added regular expression filtering capability for Azure SQL Database instances and Elastic Pools
- Improved monitoring efficiency: monitoring target is now defined by monitoring pool; WatcherNode class is considered to be deprecated
- Improved System Center Operations Manager Add Monitoring Wizard to reflect the new features of the Management Pack
- Added health monitoring for Database Geo-Replication
- Added health monitoring for Elastic Pools
- Added monitoring for “Average DTU utilization percentage” metric
- Introduced performance improvements to the Management Pack
- Optimized performance rules notation: all Object Names are standardized; Instance Names are not used anymore
- Updated the guide to reflect all the changes
- Updated the visualization library

### Bug Fixes

- Fixed issue: some rules work only if more than 1% of Azure SQL Database space is used  

## June 2016 - 1.6.1.0

### What's New

- Added Dashboards
- Added a number of new monitors and rules, including the following:
  - CPU Usage (%)
  - Workers Usage (%)
  - Log write (%)
  - Data I/O (%)
  - Sessions (%)
  - Count Failed Connection  
  - Count Successful Connection
  - Count Connection Blocked by Firewall
  - Count of Deadlock
  - Count Throttling long transaction
  - Count Connection Failed
  - XTP Storage (In-memory OLTP Storage, %) 
- Deprecated Collect Azure SQL Database Internal/External Network Egress/Ingress performance rules
- Deprecated SQL Azure Federation and Federation member workflows
- Implemented rebranding: the management pack and some workflow names have been changed
