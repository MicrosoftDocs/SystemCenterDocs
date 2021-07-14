---
ms.assetid: 9550f943-bcc2-45dc-a866-9eae7b3b8b0c
title: Monitoring configuration in Management Pack for SQL Server
description: This section explains monitoring configurations in Management Pack for SQL Server
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 7/14/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Monitoring Configuration in Management Pack for SQL Server

This section explains monitoring configurations in Management Pack for SQL Server.

## SQL Server Agent Alerting Rules: Specifics of Configuration

Management Pack for SQL Server provides the following SQL Server agent alerting rules:

- MSSQL on Windows: Alert engine stopped due to unrecoverable local eventlog errors
- MSSQL on Windows: A SQL job failed to complete successfully
- MSSQL on Windows: Job step cannot be run because the subsystem failed to load
- MSSQL on Windows: The agent is suspect. No response within last minutes
- MSSQL on Windows: SQL Server Agent could not be started
- MSSQL on Windows: SQL Server Agent initiating self-termination
- MSSQL on Windows: Step of a job caused an exception in the subsystem
- MSSQL on Windows: SQL Server Agent is unable to connect to SQL Server
- MSSQL on Windows: Unable to re-open the local eventlog

By default, these rules are enabled in [agent monitoring](sql-server-management-pack-monitoring-modes.md) mode, but disabled in [mixed monitoring](sql-server-management-pack-monitoring-modes.md#configuring-mixed-monitoring-mode) mode because Operations Manager does not allow to collect events from event logs on remote computers. To change this, you can override each of these rules by enabling the **AllowProxying** option.

>[!NOTE]
>Enabling the **AllowProxying** option may cause remote code execution. Do not enable this option unless you are sure that your computer is secured.

None of these rules work in [agentless monitoring](sql-server-management-pack-monitoring-modes.md#configuring-agentless-monitoring-mode) mode and are unavailable for SQL on Linux.

## Always On Alert Rules

Management Pack for SQL Server has two event rules for alerting in cases when the following events appear in the Windows Application log:

- Event ID 1480, Database Replica role is changed

- Event ID 19406, Availability Replica role changed

By default, SQL Server may not fire these events in the application log. To enable them, run the following T-SQL scripts:

```sql
sp_altermessage 1480, 'with_log', 'true'
```

```sql
sp_altermessage 19406, 'with_log', 'true'
```

## Always On Policies Monitoring

Management Pack for SQL Server collects health for all available Always On objects on the target SQL Server instance by reading the PBM (Policy-Based Management) policies state for each of the objects.

Besides system policies, this management pack provides the ability to monitor custom user policies defined for:

- Availability Group
- Availability Replica
- Database Replica

For each facet, the management pack introduces two monitors for the custom user policy:

- Two-state monitor with a **Warning** state. This monitor shows the state of the custom user policy that has one of the predefined warning categories as **Policy Category**.
- Two-state monitor with an **Error** state. This monitor shows the state of the custom user policy that has one of the predefined error categories as **Policy Category**.

## Space Monitoring

Management Pack for SQL Server is capable of performing space monitoring by collecting a set of metrics at the following levels:

- Database
- Filegroup
- File
- Log file 

You can use unit monitors, as well as performance metrics to view this information for multiple databases and for long time intervals.

Space monitoring supports the following types of media:

- Local storage and mount points
- Cluster Shared Volumes
- SMB Shares
- Azure BLOBs

After you import Management Pack for SQL Server, you may find that some of the space monitoring workflows are enabled by default while others are disabled. For the purposes of reducing the load on the environment, space monitoring is enabled only for the database level and disabled for the filegroup, log file, In-Memory OLTP container, and FILESTREAM filegroup levels. If your environment is sensitive to extra load, enabling rarely used workflows is not recommended.

>[!NOTE]
>When monitoring filegroups, an alert is only thrown if all files in the filegroup are unhealthy altogether. If there is at least one file in the filegroup that is healthy, then no alerts will be registered. 

The following is a list that explains the default state of each of the space monitoring workflows:

- Enabled Discoveries for Windows and Linux
	- Database Engines
	- Databases for a Database Engine
- Disabled Discoveries for Windows and Linux
  - DB Filegroups
  - DB Files
  - Transaction Log File
  - FILESTREAM Filegroups
  - Memory-Optimized Data Filegroup
  - Memory-Optimized Data Filegroup Containers
- Enabled Monitors for Windows
	- Targeted to the Database
		- ROWS Data Free Space Left
		- LOG Free Space Left
- Disabled monitors for Windows
	- Targeted to the Database
		- ROWS Data Space Percentage Change
		- In-Memory OLTP Data Free Space Left
		- FILESTREAM Data Free Space Left
  - Targeted to the Filegroup
    - DB File Free Space Left
  - Targeted to the Log file
    - DB Log File Free Space Left
  - Targeted to the In-Memory OLTP Data container
    - Memory-Optimized Data Filegroup Container 
    - Free Space
  - Targeted to the FILESTREAM filegroup
    - DB FILESTREAM Filegroup Free Space
- Enabled Monitors for Linux
	- Targeted to the Filegroup
		- DB File Free Space Left
	- Targeted to the Log file
		- DB Log File Free Space Left	
	- Targeted to the In-Memory OLTP Data container
		- Memory-Optimized Data Filegroup Container Free Space

## Many Databases on the Same Drive

Space monitoring introduced in this management pack may be noisy in environments where many databases share the same media and have the **autogrowth** setting enabled. In such cases, an alert for each database is generated when the amount of free space on the hard drive reaches the threshold.

To reduce the noise, turn off space monitoring for data and transaction log files and use the Operating System Management Pack to monitor space on the hard drive.

## DB Storage Latency Monitoring

Management Pack for SQL Server collects **DB Disk Read Latency (ms)** and **DB Disk Write Latency (ms)** performance metrics for each database. In addition, the management pack defines two associated monitors that register alerts in cases of significant performance degradation. These monitors and performance rules are disabled by default. Enable them only for specific DBs when necessary.

## Blocked Sessions

Blocking Sessions monitor is designed to query each database for a session that is blocked during a significant period of time. If blocking is detected and it exceeds the given threshold, the state is changed and an alert is raised.

You can apply an override to change the **WaitMinutes** parameter used to determine if the blocked session should be considered as long-running. The default value for this parameter is one minute.

## Securables Configuration Status Monitor

This monitor checks if each of the required SQL Server securables is accessible under the configured [Run As Account](sql-server-management-pack-run-as-profiles.md).

The following is a complete list of securables that are checked by the monitor targeted to the SQL Server DB Engine:

- Server-Level permissions
  - VIEW SERVER STATE
  - VIEW ANY DEFINITION
  - VIEW ANY DATABASE

- SELECT permission on dynamic management views
  - master.sys.dm_hadr_availability_group_states
  - master.sys.dm_hadr_availability_replica_states
  - master.sys.dm_hadr_database_replica_cluster_states
  - master.sys.dm_os_performance_counters
  - master.sys.dm_tran_active_transactions
  - master.sys.dm_tran_session_transactions
  - master.sys.dm_exec_sessions
  - master.sys.dm_exec_requests
  - master.sys.dm_exec_connections
  - master.sys.dm_os_sys_info
  - master.sys.dm_os_ring_buffers
  - master.sys.dm_os_volume_stats
  - master.sys.dm_os_threads
  - master.sys.dm_server_services
  - master.sys.dm_db_xtp_checkpoint_files
  - master.sys.dm_db_xtp_table_memory_stats
  - master.sys.dm_db_xtp_hash_index_stats
  - master.sys.dm_resource_governor_resource_pools

- SELECT permission on catalog views

  - master.sys.dm_os_host_info
  - master.sys.availability_groups
  - master.sys.databases
  - master.sys.database_files
  - master.sys.tables
  - master.sys.filegroups
  - master.sys.syscolumns
  - master.sys.sysprocesses
  - master.sys.availability_replicas
  - master.sys.database_mirroring
  - master.sys.configurations
  - msdb.dbo.syspolicy_policies
  - msdb.dbo.syspolicy_conditions
  - msdb.dbo.syspolicy_policy_execution_history
  - msdb.dbo.syspolicy_configuration
  - msdb.dbo.syspolicy_system_health_state
  - msdb.dbo.syspolicy_object_sets
  - msdb.dbo.syspolicy_policy_categories
  - msdb.dbo.syspolicy_target_sets
  - msdb.dbo.syspolicy_target_set_levels
  - msdb.dbo.syspolicy_policy_execution_history_details
  - msdb.dbo.sysjobschedules
  - msdb.dbo.syscategories
  - msdb.dbo.sysjobs_view
  - msdb.dbo.log_shipping_primary_databases
  - msdb.dbo.log_shipping_secondary_databases
  - msdb.dbo.backupset

- EXECUTE permission on stored procedures
  - master.sys.sp_enumerrorlogs
  - master.sys.xp_readerrorlog
  - master.sys.xp_instance_regread
  - msdb.dbo.sp_help_jobactivity
  - msdb.dbo.sp_help_job
  - msdb.dbo.SQLAGENT_SUSER_SNAME

The following is a complete list of securables checked by the monitor targeted to SQL Server Databases:

- SELECT permission on catalog views
  - sys.database_files
  - sys.tables
  - sys.filegroups
  - sys.syscolumns