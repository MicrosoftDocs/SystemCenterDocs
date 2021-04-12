---
ms.assetid: 7e0ce57d-1b20-4412-a14e-941b4264f849
title: Monitoring Configuration in Management Pack for Azure SQL Managed Instance
description: This article explains the monitoring configuration in Management Pack for Azure SQL Managed Instance
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Monitoring Configuration in Management Pack for Azure SQL Managed Instance

Management Pack for Azure SQL Managed Instance has two monitoring templates for monitoring of Azure SQL Managed Instance:

- **Azure SQL MI – Automatic** 

    This template allows you to configure monitoring by discovering all managed instances in the specified Azure subscription automatically.

- **Azure SQL MI – Manual**

    This template allows you to add the selected instances to the monitoring list by specifying connection strings manually.

>[!NOTE]
>Using both templates at the same time may cause manually added instances to be monitored by two sets of monitoring workflows. This leads to redundant use of resources and also may cause performance issues.

## Securables Configuration Status Monitor

**Securables Configuration Status Monitor** checks if each of the required managed instance securables is accessible under the configured monitoring account.

## Securables List

The following is a complete list of securables checked by the monitor:

- Server-Level permissions
  - VIEW SERVER STATE
  - VIEW ANY DEFINITION
  - VIEW ANY DATABASE

- SELECT permission on dynamic management views
  - sys.dm_os_performance_counters
  - sys.dm_tran_active_transactions
  - sys.dm_tran_session_transactions
  - sys.dm_exec_sessions
  - sys.dm_exec_requests
  - sys.dm_exec_connections
  - sys.dm_os_sys_info
  - sys.dm_os_host_info
  - sys.dm_os_ring_buffers
  - sys.dm_os_volume_stats
  - sys.dm_os_threads
  - sys.dm_hadr_database_replica_states
  - sys.dm_hadr_fabric_partition_states
  - sys.dm_hadr_fabric_config_parameters
  - sys.dm_hadr_fabric_continuous_copy_status
  - sys.dm_db_xtp_checkpoint_files
  - sys.dm_db_xtp_table_memory_stats
  - sys.dm_db_xtp_hash_index_stats
  - sys.dm_internal_resource_governor_resource_pools

- SELECT permission on catalog views
  - sys.databases
  - sys.database_files
  - sys.tables
  - sys.filegroups
  - sys.syscolumns
  - sys.sysprocesses
  - sys.configurations
  - sys.syslanguages
  - sys.server_resource_stats
  - msdb.dbo.sysjobschedules
  - msdb.dbo.backupset

- EXECUTE permission on stored procedures
  - sys.sp_enumerrorlogs
  - sys.xp_readerrorlog
  - sys.xp_instance_regread
  - msdb.dbo.sp_help_jobactivity
  - msdb.dbo.sp_help_job