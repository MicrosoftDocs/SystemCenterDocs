---
description: include file to describe the process to upgrade classic deployment model Automation in System Center 2016.
ms.topic:  include
author: Jeronika-MS
ms.author: v-gajeronika
ms.service:  system-center
keywords:  
ms.date: 07/24/2025
title:  include file
ms.subservice:  service-management-automation
ms.assetid: f13edf4f-5708-4a50-94ca-9afb5c266839
---

## Upgrade to System Center 2016 - Service Management Automation


The following sections provide details about how to upgrade SMA 2012 R2 to SMA 2016.

## Prerequisites

- Review the [system requirements](../sma/system-requirements-sma.md) to determine support requirements for SMA 2016.
- Perform a full backup of the SMA database as a precaution. This is a standard SQL Server database, and you can use standard tools and processes for [backing up SQL Server](/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases).

## Upgrade

There's no in place upgrade for SMA servers, so you must uninstall the existing servers before installing the new ones. You can keep the database, which contains the runbooks and configuration settings intact.

> [!NOTE]
> When installing SMA with an existing database, you must install the worker servers before the web service.

To upgrade to SMA 2016, follow these steps:

1. If SMA servers are being monitored by Operations Manager, put them in maintenance mode to prevent false alerts.
2. Uninstall the SMA web service and SMA runbook workers.
3. Install the SMA runbook workers.
4. Install the SMA web service.
5. Remove SMA servers from maintenance mode.