---
ms.assetid: 500910b3-e260-4673-b219-8dc24bc4f916
title: Features and enhancements in Management Pack for Azure SQL Managed Instance
description: This article explains the new functionality and bug fixes implemented in Management Pack for Azure SQL Managed Instance
author: Anastas1ya
ms.author: v-ekaterinap
manager: vvithal
ms.date: 12/20/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Features and Enhancements in Management Pack for Azure SQL Managed Instance

This article covers new functionality and improvements in Management Pack for Azure SQL Managed Instance.

## December 2021 - 7.0.34.0 RTM

### What's New

- Improved the "CPU Utilization" monitor and the associated performance rule. Now they show the same data as on the Azure portal
- Updated the SPN creation process related to the [latest changes in Azure API](/azure/active-directory/develop/reference-breaking-changes#appid-uri-in-single-tenant-applications-will-require-use-of-default-scheme-or-verified-domains)
- Updated display strings

### Bug Fixes

- Fixed an issue with creating SPN with unnecessary API permissions for the Azure AD application

## July 2020 - 7.0.22.0 RTM

### What's New

- Updated monitor “Securables Configuration Status”
- Updated monitor “Job Duration” to add current job run's duration to its alert description
- Updated UI of wizard “Automatic Discovery”
- Updated alerting rules to avoid gathering SQL Log events that happened during the maintenance mode
- Updated dashboards
- Updated display strings

### Bug Fixes

- Fixed: Self-diagnostic alerting rules fire alerts for SQL Server MP log events

## April 2020 - 7.0.21.0 CTP

### What's New

- Management pack was completely redone being based on up-to-date SQL Server MP codebase

## September 2019 - 1.0.1.0 CTP

### What's New

- Disabled “XTP Configuration Monitor”
- Disabled “Database Backup Status Monitor”
- Rebuild management pack and verify against the current version of Azure SQL Managed Instance Provided a few minor UI improvements to the Add Monitoring Wizard