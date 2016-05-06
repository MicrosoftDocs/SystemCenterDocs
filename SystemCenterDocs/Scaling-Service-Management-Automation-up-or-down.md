---
title: Scaling Service Management Automation up or down
ms.custom: na
ms.prod: system-center-2012
ms.reviewer: na
ms.suite: na
ms.technology: 
  - orchestrator
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 00e55889-02fc-49a9-9a52-f8cbdaf36255
---
# Scaling Service Management Automation up or down
Use the guidance in this section to scale out a machine tier in a service that is deployed in [!INCLUDE[sma_1](../Token/sma_1_md.md)]. You can add runbook workers and web services to add additional capacity for runbook processing.

### Initial recommendations
The recommended configuration is 3 virtual machines, each with an installed a runbook worker and web service. The incoming web traffic should be load balanced. The machines should each be at least each two cores and contain a minimum of 4 GB of RAM, along with 60 GB of storage. Only one PowerShell module should be installed.

### SQL Server recommendations
For the SQL Server database, 8 GB of RAM and 8 cores are recommended.

1 month of data under heavy load \(12 jobs per minute for a month\) results in 20 GB of database space usage. By default, job purging should keep the space usage from growing much beyond this. For more on settings for database purging, see [How to purge the Service Management Automation database](../Topic/How-to-purge-the-Service-Management-Automation-database.md).

### Scale out [!INCLUDE[sma_1](../Token/sma_1_md.md)]
If runbook jobs are running slowly, you might want to increase the number of runbook workers that are sharing workloads. New runbook worker\/web service instances must be installed on their own virtual machines.

Before installing or uninstalling a [!INCLUDE[sma_1](../Token/sma_1_md.md)] runbook worker, ensure that you have stopped the Runbook Worker service \(rbsvc\) on the computer where the runbook worker is installed. For instructions on how to avoid any data loss when removing a runbook worker, including Windows PowerShell cmdlets and scripting help for this operation, see the [overview of runbook worker deployments](http://go.microsoft.com/fwlink/?LinkId=301478).

