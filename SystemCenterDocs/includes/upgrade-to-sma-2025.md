---
description: include file to provide information about how to upgrade your existing Service Management Automation to release 2025.
ms.topic: include
author: jyothisuri
ms.author: jsuri
ms.service:  system-center
keywords:  
ms.date: 04/17/2024
title:  include file
ms.subservice:  service-management-automation
ms.assetid:
---

## Upgrade to System Center 2025 - Service Management Automation

The following sections provide information about how to upgrade your existing Service Management Automation 2022 to Service Management Automation 2025.

> [!NOTE]
> To upgrade to System Center 2025 - SMA, you must have SMA 2022 installed.

## Prerequisites to upgrade

- Review the [System Requirements for Service Management Automation](../sma/system-requirements-sma.md) to determine whether your current version of SMA supports upgrade to SMA 2025.
- Perform a full backup of the SMA database as a precaution. It's a standard SQL Server database, and you can use standard tools and processes for [backing up SQL Server](/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases).

## Upgrading to SMA 2025

There's no in place upgrade for SMA servers, so you must uninstall the existing servers before installing the new ones. You can keep the database intact, which contains the runbooks and configuration settings.  

> [!NOTE]
> When installing SMA with an existing database, you must install the worker servers before the web service.

1. If SMA servers are being monitored by Operations Manager, enable maintenance mode to prevent false alerts.
2. Uninstall the SMA web service and SMA runbook workers using the instructions at <a href="/previous-versions/system-center/system-center-2012-R2/dn469636(v=sc.12)">How to uninstall Service Management Automation</a>.
3. Install the SMA runbook workers using the instructions at [How to install the Service Management Automation runbook worker](../sma/deploy.md).
4. Install the SMA web service using the instructions at [How to install the Service Management Automation web service](../sma/deploy.md).
5. Remove SMA servers from maintenance mode.
