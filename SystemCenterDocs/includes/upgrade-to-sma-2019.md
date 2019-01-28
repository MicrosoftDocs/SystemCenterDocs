---
description: include file to provide information about how to upgrade your existing Service Management Automation to release 2019.
manager:  vvithal
ms.topic: include
author:  JYOTHIRMAISURI
ms.author: v-jysur
ms.prod:  system center
keywords:  
ms.date: 01/28/2019
title:  include file
ms.technology:  service-management-automation
ms.assetid:  7fc426cb-aa90-4e45-b14c-95d711f6e005
---

## Upgrade to System Center 2019 - Service Management Automation


The following sections provide information about how to upgrade your existing Service Management Automation installation to 2019.

> [!NOTE]
  You can upgrade to SMA 2019 from SMA 2016, 1801 and 1807.

## Prerequisites

- Review the [System Requirements for Service Management Automation](../sma/system-requirements-1801.md) to determine whether your current version of SMA supports upgrade to SMA 2019.
- Perform a full backup of the SMA database as a precaution. This is a standard SQL Server database, and you can use standard tools and processes for [backing up SQL Server](https://go.microsoft.com/fwlink/p/?LinkId=216936).

## Upgrading

There is no in place upgrade for SMA servers, so you must uninstall the existing servers before installing the new ones.  You can keep the database intact, which contains the runbooks and configuration settings.  

> [!NOTE]
When installing SMA with an existing database, you must install the worker servers before the web service.

1. If SMA servers are being monitored by Operations Manager, put them in maintenance mode to prevent false alerts.
2. Uninstall the SMA web service and SMA runbook workers using the instructions at <a href="https://technet.microsoft.com/en-us/library/dn469636(v=sc.12).aspx">How to uninstall Service Management Automation</a> for details.
3. Install the SMA runbook workers using the instructions at [How to install the Service Management Automation runbook worker](../sma/deploy/how-to-install-the-service-management-automation-runbook-worker.md).
4. Install the SMA web service using the instructions at [How to install the Service Management Automation web service](../sma/deploy/how-to-install-the-service-management-automation-web-service.md).
5. Remove SMA servers from maintenance mode.
