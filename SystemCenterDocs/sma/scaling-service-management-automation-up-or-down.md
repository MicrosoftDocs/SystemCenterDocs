---
description: Provides an overview of how you can scale out a machine tier.
ms.topic: concept-article
ms.service: system-center
author: Jeronika-MS
ms.author: v-gajeronika
keywords:
ms.date: 11/01/2024
title: Scale Service Management Automation
ms.subservice: service-management-automation
ms.assetid: 00e55889-02fc-49a9-9a52-f8cbdaf36255
ms.custom: engagement-fy24
ms.update-cycle: 1095-days
---

# Scale Service Management Automation

Use the guidance in this section to scale out a machine tier in a service that's deployed in Service Management Automation (SMA). You can add runbook workers and web services to add additional capacity for runbook processing.

## Initial recommendations

The recommended configuration is as follows:

- Three VMs, each with an installed runbook worker and web service.
- The incoming web traffic should be load balanced.
- The machines should have at least two cores and contain a minimum of 4 GB of RAM, along with 60 GB of storage.
- Only one PowerShell module should be installed.

## SQL Server recommendations

SQL Server recommendations include:

- For the SQL Server database, 8 GB of RAM and 8 cores are recommended.
- One month of data under heavy load (12 jobs per minute for a month) results in 20 GB of database space usage. By default, job purging should keep the space usage from growing much beyond this. [Learn more](how-to-purge-the-service-management-automation-database.md).

## Scale out

Scale out recommendations:

- If runbook jobs are running slowly, you can increase the number of runbook workers that are sharing workloads. New runbook worker/web service instances must be installed on their own VMs.
Before installing or uninstalling a runbook worker, stop the Runbook Worker service (rbsvc) on the computer on which the runbook worker is installed. [Learn about](/previous-versions/system-center/dn530618(v=sc.20)) runbook worker deployments.
