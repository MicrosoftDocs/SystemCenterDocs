---
title: How to upgrade from a previous version of Service Management Automation
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c849610a-81ea-474d-a77f-bc15694e65f0
---
# How to upgrade from a previous version of Service Management Automation

>Applies To: 

This article describes how to upgrade your existing Service Management Automation 2016 (SMA).

## Prerequisites

- Review the [System Requirements for Service Management Automation](System-requirements-for-Service-Management-Automation.md) to determine whether it will support SMA.
- Perform a full backup of the SMA database as a precaution. This is a standard SQL Server database, and you can standard tools and processes for [backing up SQL Server](http://go.microsoft.com/fwlink/p/?LinkId=216936).

## Upgrading

There is no in place upgrade for SMA servers, so you must uninstall the existing servers before installing the new ones.  You can keep the database intact which contains the runbooks and configuration settings.  

> [!NOTE] When installing SMA with an existing database, you must install the worker servers before the web service. 

1. If SMA servers are being monitored by Operations Manager, put them in maintenance mode to prevent false alerts.
2. Uninstall the SMA web service and SM runbook workers using the instructions at [How to uninstall Service Management Automation].(How%20to%20uninstall%20Service%20Management%20Automation.md) for details.
3. Install the SMA runbook workers using the instructions at [How to install the Service Management Automation runbook worker](How-to-install-the-Service-Management-Automation-runbook-worker.md).
4. Install the SMA web service using the instructions at [How to install the Service Management Automation web service](How-to-install-the-Service-Management-Automation-web-service.md).
5. Remove SMA servers from maintenance mode.


