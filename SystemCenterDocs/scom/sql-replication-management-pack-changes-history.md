---
ms.assetid: 9f175a54-0700-4bf3-8288-d30f0f3538f0
title: Features and enhancements in Management Pack for SQL Server Replication
description: This article explains the new functionality and bug fixes implemented in Management Pack for SQL Server Replication
author: Anastas1ya
ms.author: jsuri
ms.date: 11/01/2024
ms.topic: concept-article
ms.service: system-center
ms.subservice: operations-manager
---

# Features and Enhancements in Management Pack for SQL Server Replication

This article covers new functionality and improvements in Management Pack for SQL Server Replication.

## December 2020 - 7.0.28.0 RTM

### What's New

- Updated management pack to support SQL Server 2012 through 2022
- Updated "Replication Agents failed on the Distributor" unit monitor to extend it for Log Reader and Queue Reader agents detection
- Added new property 'DiskFreeSpace' for "Publication Snapshot Available Space" unit monitor
- Removed "One or more of the Replication Agents are retrying on the Distributor" monitor as non-useful
- Removed “Availability of the Distribution database from a Subscriber” monitor as deprecated
- Updated display strings

### Bug Fixes

- Fixed discovery issue on SQL Server 2019
- Fixed issue with the incorrect definition of 'MachineName' property of DB Engine in some discoveries and replication agent-state unit monitors
- Fixed issue with wrong property-bag key initialization on case-sensitive DB Engine in some unit monitors and performance rules
- Fixed issue with the critical state of "Replication Log Reader Agent State for the Distributor" and "Replication Queue Reader Agent State for Distributor" unit monitors
- Fixed wrong space calculation in "Publication Snapshot Available Space"
- Fixed duplication of securable detection for monitor "Subscriber Securables Configuration Status"
- Fixed issue with the incorrect definition of 'InstanceName' property in "Replication Database Health" discovery
- Fixed issue with an incorrect alert message for monitor "Pending Commands on Distributor"
- Fixed issue with incorrect condition detection for monitor "Total daily execution time of the Replication Agent"

## April 2019 - 7.0.15.0 RTM

- Supported last changes in version-agnostic management pack for SQL Server

## November 2017 - 7.0.0.0 RTM

- Introduced many improvements and bug fixes

## October 2017 - 6.7.65.0 RC1

- The management pack was reimplemented in order to enable monitoring of SQL Server 2017 and all upcoming SQL Server versions
- Reduced the number of files in the management pack
- Introduced many fixes and improvements to functionality, performance, and display strings

## June 2017 - 6.7.60.0 RC0

- Added many monitors and performance rules to create the same Health model as presented in SQL Server 2008-2016 Replication management packs
- Improved and refactored the management pack modules
- Fixed many issues
