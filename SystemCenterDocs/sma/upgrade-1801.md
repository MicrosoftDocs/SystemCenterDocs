---
description: This article provides information about how to upgrade your existing Service Management Automation to release 1801.
manager:  vvithal
ms.topic:  article
author:  JYOTHIRMAISURI
ms.author: v-jysur
ms.prod:  system-center-threshold
keywords:  
ms.date: 02/05/2018
title:  How to upgrade from a previous version of Service Management Automation to 1801
ms.technology:  service-management-automation
ms.assetid:  23356ae4-74ba-46f0-8484-22f896a5e0f5
monikerRange: 'sc-sma-1801'
---

# Upgrade System Center 1801 - Service Management Automation


This article describes how to upgrade your existing Service Management Automation (SMA) 2012 R2 UR8/2016 UR1 Service Management Automation installation.

> [!NOTE]
  To upgrade to System Center 1801 - SMA, you must install UR8 on 2012 R2 /UR1 on 2016.

## Prerequisites

- Review the [System Requirements for Service Management Automation](system-requirements-1801.md) to determine whether your current version of SMA supports upgrade to SMA 1801.
- Perform a full backup of the SMA database as a precaution. This is a standard SQL Server database, and you can use standard tools and processes for [backing up SQL Server](https://go.microsoft.com/fwlink/p/?LinkId=216936).

## Upgrading

There is no in place upgrade for SMA servers, so you must uninstall the existing servers before installing the new ones.  You can keep the database intact, which contains the runbooks and configuration settings.  

> [!NOTE]
When installing SMA with an existing database, you must install the worker servers before the web service.

1. If SMA servers are being monitored by Operations Manager, put them in maintenance mode to prevent false alerts.
2. Uninstall the SMA web service and SMA runbook workers using the instructions at <a href="https://technet.microsoft.com/en-us/library/dn469636(v=sc.12).aspx">How to uninstall Service Management Automation</a> for details.
3. Install the SMA runbook workers using the instructions at [How to install the Service Management Automation runbook worker](deploy/how-to-install-the-service-management-automation-runbook-worker.md).
4. Install the SMA web service using the instructions at [How to install the Service Management Automation web service](deploy/how-to-install-the-service-management-automation-web-service.md).
5. Remove SMA servers from maintenance mode.
