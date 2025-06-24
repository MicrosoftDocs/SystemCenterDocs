---
ms.assetid: 500910b3-e260-4673-b219-8dc24bc4f916
title: Features and enhancements in Management Pack for Azure SQL Managed Instance
description: This article explains the new functionality and bug fixes implemented in Management Pack for Azure SQL Managed Instance.
author: fkornilov
ms.author: v-fkornilov
manager: vvithal
ms.date: 11/01/2024
ms.topic: concept-article
ms.service: system-center
ms.subservice: operations-manager
---

# Features and enhancements in Management Pack for Azure SQL Managed Instance

This article covers new functionality and improvements in Management Pack for Azure SQL Managed Instance.

## July 2024 - 7.6.0 RTM

### What's new

- Reworked the creation of Run As Accounts for the Automatic template to allow multiple accounts to be created in one time period
- Enhanced the Automatic template options for monitoring SQL Managed Instances by introducing support for [Managed Identity](managed-instance-management-pack-automatic-monitoring-managed-identity.md). This includes both System-assigned and User-assigned Managed Identity options
- Updated display strings

## March 2024 - 7.4.0.0 RTM

### What's new

- Updated API with Microsoft Authentication Library (MSAL) in place of deprecated Azure Active Directory Authentication Library (ADAL)
- Improved "Database Status" monitor by adding two more [database statuses](managed-instance-management-pack-monitoring-configuration.md#database-status-monitoring) for Geo-Replication - COPYING and OFFLINE_SECONDARY
- Added support for [custom management server resource pools](managed-instance-management-pack-monitoring-pool.md)
- Added support for selecting a tenant in the 'Entra ID Tenant' monitoring wizard step
- Added support for [enabling debug logging](managed-instance-management-pack-enable-debugging.md) in Windows Event Log
- Added new [Operations Manager console task](managed-instance-management-pack-export-event-log-task.md), which allows saving and transport of the Event Log file from the Management Server
- Added new [regular expression filtering mask type](managed-instance-management-pack-automatic-monitoring-service-principal-name.md#instances-filtering) in the 'Instance Filtering' monitoring wizard step; now the instance names can be filtered using regular expression and wildcards for include and exclude from the monitoring
- Added support for manually setting the expiration date for the application client secret in the [Automatic Monitoring Template wizard step](managed-instance-management-pack-automatic-monitoring-service-principal-name.md#auto-create-spn)
- Updated memory and space monitoring workflows to apply four significant digit roundings in all the values
- Improved accessibility for the Summary Dashboard view and Monitoring Wizard template, including the following major changes:
  - improved keyboard navigation
  - improved color contrast in dashboards for better legibility
  - reworked high contrast theme for dashboards
  - added support for screen-reading software
- Updated display strings

### Bug fixes

- Fixed an issue with the "Database Status" monitor becoming healthy despite the database being in an unhealthy state in some configuration cases
- Fixed an issue with the client secret expiration date if the Auto-Create Service Principal Name option is selected
- Fixed an issue with creating multiple Run As accounts per day for different application registrations

## December 2021 - 7.0.34.0 RTM

### What's new

- Improved the "CPU Utilization" monitor and the associated performance rule. Now they show the same data as on the Azure portal
- Updated the Service Principal Name creation process related to the [latest changes in Azure API](/azure/active-directory/develop/reference-breaking-changes#appid-uri-in-single-tenant-applications-will-require-use-of-default-scheme-or-verified-domains)
- Updated display strings

### Bug fixes

- Fixed an issue with creating Service Principal Name with unnecessary API permissions for the Azure AD application

## July 2020 - 7.0.22.0 RTM

### What's new

- Updated monitor "Securables Configuration Status"
- Updated monitor "Job Duration" to add current job run's duration to its alert description
- Updated UI of wizard "Automatic Discovery"
- Updated alerting rules to avoid gathering SQL Log events that happened during the maintenance mode
- Updated dashboards
- Updated display strings

### Bug fixes

- Fixed: Self-diagnostic alerting rules fire alerts for SQL Server MP log events

## April 2020 - 7.0.21.0 CTP

### What's new

- Management pack was redone being based on up-to-date SQL Server MP codebase

## September 2019 - 1.0.1.0 CTP

### What's new

- Disabled "XTP Configuration Monitor"
- Disabled "Database Backup Status Monitor"
- Rebuild management pack and verify against the current version of Azure SQL Managed Instance Provided a few minor UI improvements to the Monitoring Wizard
