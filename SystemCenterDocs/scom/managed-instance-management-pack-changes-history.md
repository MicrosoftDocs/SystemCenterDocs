---
ms.assetid: 500910b3-e260-4673-b219-8dc24bc4f916
title: Features and Enhancements in Management Pack for Azure SQL Managed Instance
description: This article explains the new functionality and bug fixes implemented in Management Pack for Azure SQL Managed Instance
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Features and Enhancements in Management Pack for Azure SQL Managed Instance

This section covers new functionality and improvements in Management Pack for Azure SQL Managed Instance.

## July 2020 - version 7.0.22.0 RTM

### What's New

- Updated monitor “Securables Configuration Status”
- Updated monitor “Job Duration” to add current job run's duration to its alert description
- Updated UI of wizard “Automatic Discovery”
- Updated alerting rules to avoid gathering SQL Log events that happened during maintenance mode
- Updated dashboards
- Updated display strings

### Bug Fixes

- Fixed: Self-diagnostic alerting rules fire alerts for SQL Server MP log events

## April 2020 - version 7.0.21.0 CTP

### What's New

- Management pack was completely redone being based on up-to-date SQL Server MP codebase

## September 2019 - version 1.0.1.0 CTP

### What's New

- Disabled “XTP Configuration Monitor”
- Disabled “Database Backup Status Monitor”
- Rebuild management pack and verify against the current version of Managed Instance Provided a few minor UI improvements to the Add Monitoring Wizard