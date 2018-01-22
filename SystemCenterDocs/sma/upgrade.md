---
description: Describes how to upgrade Service Management Automation in System Center 2016.
manager:  cfreemanwa
ms.topic:  article
author:  bwren
ms.prod:  system-center-threshold
keywords:  
ms.date: 01/22/2018
title:  Upgrade to Service Management Automation in System Center 2016
ms.technology:  service-management-automation
---

# How to upgrade from a previous version of Service Management Automation


This article describes how to upgrade your existing Service Management Automation (SMA) 2012 R2 Service Management Automation installation. 

## Prerequisites

- Review the [system requirementsn](/system-center/orchestrator/system-requirements) to determine support requirements for SMA 2016.
- Perform a full backup of the SMA database as a precaution. This is a standard SQL Server database, and you can use standard tools and processes for [backing up SQL Server](https://go.microsoft.com/fwlink/p/?LinkId=216936).

## Upgrade

There is no in place upgrade for SMA servers, so you must uninstall the existing servers before installing the new ones.  You can keep the database intact which contains the runbooks and configuration settings.  

> [!NOTE]
When installing SMA with an existing database, you must install the worker servers before the web service.

1. If SMA servers are being monitored by Operations Manager, put them in maintenance mode to prevent false alerts.
2. Uninstall the SMA web service and SMA runbook workers.
3. Install the SMA runbook workers.
4. Install the SMA web service.
5. Remove SMA servers from maintenance mode.
