---
description: Describes how to upgrade your existing Service Management Automation.
manager:  cfreemanwa
ms.topic:  article
author:  bwren
ms.prod:  system-center-threshold
keywords:  
ms.date: 10/12/2016
title:  How to upgrade from a previous version of Service Management Automation
ms.technology:  service-management-automation
ms.assetid:  c849610a-81ea-474d-a77f-bc15694e65f0
---

# How to upgrade from a previous version of Service Management Automation

>Applies To:

This article describes how to upgrade your existing Service Management Automation 2012 R2 Service Management Automation installation. For information about upgrading all technologies in System Center, see the article, [Upgrade to System Center 2016](/system-center/upgrade-to-system-center-2016).

## Prerequisites

- Review the [System Requirements for Service Management Automation](/system-center/orchestrator/system-requirements) to determine whether it will support SMA 2016.
- Perform a full backup of the SMA database as a precaution. This is a standard SQL Server database, and you can standard tools and processes for [backing up SQL Server](https://go.microsoft.com/fwlink/p/?LinkId=216936).

## Upgrading

There is no in place upgrade for SMA servers, so you must uninstall the existing servers before installing the new ones.  You can keep the database intact which contains the runbooks and configuration settings.  

> [!NOTE]
When installing SMA with an existing database, you must install the worker servers before the web service.

1. If SMA servers are being monitored by Operations Manager, put them in maintenance mode to prevent false alerts.
2. Uninstall the SMA web service and SMA runbook workers using the instructions at <a href="https://technet.microsoft.com/en-us/library/dn469636(v=sc.12).aspx">How to uninstall Service Management Automation</a> for details.
3. Install the SMA runbook workers using the instructions at [How to install the Service Management Automation runbook worker](deploy/how-to-install-the-service-management-automation-runbook-worker.md).
4. Install the SMA web service using the instructions at [How to install the Service Management Automation web service](deploy/how-to-install-the-service-management-automation-web-service.md).
5. Remove SMA servers from maintenance mode.
