---
ms.assetid: 7e0ce57d-1b20-4412-a14e-941b4264f849
title: Monitoring configuration in Management Pack for Azure SQL Managed Instance
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

## Database Status Monitoring

Database status monitoring is intended to check the database status as reported by the SQL managed instance. Status check is done by running a query against the master database of the managed instance that returns the database state. If you receive an alert from this monitor, an action is required in order to bring the database back to an operational state.

All database states except the ONLINE one will result in an unhealthy monitor state. The following table defines the database states. 
  
|State|Definition|  
|-----------|----------------|  
|ONLINE|Database is available for access. The primary filegroup is online, although the undo phase of recovery may not have been completed.|  
|OFFLINE|Database is unavailable. A database becomes offline by explicit user action and remains offline until additional user action is taken. For example, the database may be taken offline in order to move a file to a new disk. The database is then brought back online after the move has been completed.|  
|RESTORING|One or more files of the primary filegroup are being restored, or one or more secondary files are being restored offline. The database is unavailable.|  
|RECOVERING|Database is being recovered. The recovering process is a transient state; the database will automatically become online if the recovery succeeds. If the recovery fails, the database will become suspect. The database is unavailable.|  
|RECOVERY PENDING|SQL Server has encountered a resource-related error during recovery. The database is not damaged, but files may be missing or system resource limitations may be preventing it from starting. The database is unavailable. Additional action by the user is required to resolve the error and let the recovery process be completed.|  
|SUSPECT|At least the primary filegroup is suspect and may be damaged. The database cannot be recovered during startup of SQL Server. The database is unavailable. Additional action by the user is required to resolve the problem.|  
|EMERGENCY|User has changed the database and set the status to EMERGENCY. The database is in single-user mode and may be repaired or restored. The database is marked READ_ONLY, logging is disabled, and access is limited to members of the **sysadmin** fixed server role. EMERGENCY is primarily used for troubleshooting purposes. For example, a database marked as suspect can be set to the EMERGENCY state. This could permit the system administrator read-only access to the database. Only members of the **sysadmin** fixed server role can set a database to the EMERGENCY state.|  

## Geo-Replication Database Monitoring

Management Pack for Azure SQL Managed Instance utilizes a monitor that checks the replication status of the primary and secondary databases located in an auto-failover group.

The monitor produces an unhealthy state which indicates that the secondary database is not transactionally consistent and is not being constantly synchronized with the primary database. 

There are three geo-replication states described in the following table.

|Replication State|Description|Health State|
|-|-|-|
|CATCH_UP|The secondary database is in a transactionally consistent state and is being constantly synchronized with the primary database.|Healthy|
|SEEDING|The geo-replication target is being seeded but the two databases are not yet synchronized. Until seeding completes, you cannot connect to the secondary database. Removing secondary database from the primary will cancel the seeding operation.|Critical|
|PENDING|This is not an active continuous-copy relationship. This state usually indicates that the bandwidth available for the interlink is insufficient for the level of transaction activity on the primary database. However, the continuous-copy relationship is still intact.|Critical|

Each of these states is produced by the 'sys.dm_hadr_fabric_continuous_copy_status' DVM, which is executed on the master database located on the managed instance.

For more information on geo-failover of multiple databases, see [Use auto-failover groups to enable transparent and coordinated geo-failover of multiple databases](/azure/sql-database/sql-database-auto-failover-group#best-practices-of-using-failover-groups-with-managed-instances).
