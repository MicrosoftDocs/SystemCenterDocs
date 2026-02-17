---
ms.assetid: d406c771-aa85-4a70-bf35-fb27e04b8244
title: Monitor Configuration in management pack for SQL Server Replication
description: This article explains the monitoring configuration in management pack for SQL Server Replication
author: Anastas1ya
manager: evansma
ms.date: 07/24/2025
ms.author: v-gajeronika
ms.topic: concept-article
ms.service: system-center
ms.subservice: operations-manager
ms.update-cycle: 1095-days
---

# Monitor Configuration in management pack for SQL Server Replication

Management Pack for SQL Server Replication enables discovery and monitoring of all SQL Server Replication related components.

The management pack supports agent, agentless, and mixed monitoring modes. The pack automatically selects monitoring mode used by Management Pack for SQL Server.

Replication objects discovered and monitored by the management pack are as follows:

- Distributor
- Publisher
- Subscriber
- Publication
- Subscription

Each managed replication object is discovered and monitored using many rules and monitors.

## Many Publication Snapshots on the Same Drive

Space monitoring introduced in this management pack might be noisy in environments where many publication snapshots share the same media. In such cases, an alert for a publication snapshot is generated when the amount of free space on the hard drive reaches the threshold.

To reduce the noise, turn off space monitors for **Snapshot Available Space (%)**, and use Operating System Management Pack to monitor space on the hard drive.

## Maintenance Job Failure

Replication uses maintenance jobs that are monitored by **MSSQL Replication: The Maintenance Job(s) Failed on Distributor Alert Rule**:

- Reinitialization subscriptions having data validation failures
- Agent history clean up: distribution
- Replication monitoring refresher for distribution
- Replication agents checkup
- Distribution clean up: distribution
- Expired subscription clean up

For more information, see [Run Replication Maintenance Jobs (SQL Server Management Studio)](/sql/relational-databases/replication/administration/run-replication-maintenance-jobs-sql-server-management-studio?preserve-view=true&view=sql-server-ver15).

## Job Failure

Management Pack for Microsoft SQL Server Replication defines a monitor targeted at the Distributor and Subscriber. These monitors oversee the replication agent jobs and change the monitor state when the job has the following states:

- Job Exist But Never Run and Has Not Scheduled
- Job Expired
- Job Failed
- Job is Disabled
- Job is Enabled but Schedule is Disabled
- Job Execution Failed and was Not in Accordance with the Schedule
- Job is Retry
- Job Never Run
- Job Never Run But Schedule Exist
- Job Successfully Done But Not in Accordance with the Schedule
- Job Execution was Stopped and was Not in Accordance with the Schedule
- Previous Job Execution Failed
- Previous Job Execution was Stopped
- Unknown State of the Job

## Distributor Securables Configuration Status Monitor

This monitor checks if each of the required Replication Distributor securables is accessible under the configured Run As account.

The following permissions are a complete list of securables that are checked by the monitor targeted to the Replication Distributor:

- Server-Level permissions
  - VIEW SERVER STATE
  - VIEW ANY DATABASE

- SELECT permission on catalog views
  - sys.servers
  - sys.configurations
  - msdb.dbo.sysjobs
  - msdb.dbo.sysjobhistory
  - msdb.dbo.sysjobschedules
  - msdb.dbo.sysschedules
  - msdb.dbo.syscategories
  - msdb.dbo.sysjobservers

- EXECUTE permission on stored procedures
  - sp_MSget_repl_commands
  - xp_sqlagent_enum_jobs

## Publisher Securables Configuration Status Monitor

This monitor checks if each of the required Replication Publisher securables is accessible under the configured Run As account.

The following permissions are a complete list of securables that are checked by the monitor targeted to the Replication Publisher:

- Server-Level permissions
  - VIEW SERVER STATE
  - VIEW ANY DATABASE

- EXECUTE permission on stored procedures
  - sp_helppublication
  - sp_helpmergepublication
  - sp_helpdistributor

## Subscriber Securables Configuration Status Monitor

This monitor checks if each of the required Replication Subscriber securables is accessible under the configured Run As account.

The following permissions are a complete list of securables that are checked by the monitor targeted to the Replication Subscriber:

- Server-Level permissions
  - VIEW SERVER STATE
  - VIEW ANY DATABASE

- SELECT permission on catalog views
  - sys.configurations
  - msdb.dbo.sysjobs
  - msdb.dbo.sysjobhistory
  - msdb.dbo.sysjobschedules
  - msdb.dbo.sysschedules
  - msdb.dbo.sysjobservers

- EXECUTE permission on stored procedures
  - sp_MSenumsubscriptions
  - sp_helppullsubscription
  - sp_helpmergepullsubscription
  - xp_sqlagent_enum_jobs
  - sp_MSget_repl_commands
