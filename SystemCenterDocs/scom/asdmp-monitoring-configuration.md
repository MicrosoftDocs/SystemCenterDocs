---
ms.assetid: 3e21f741-fd1d-4a60-9864-209ed131df1a
title: Monitoring Configuration in Management Pack for Azure SQL Database
description: This article explains the monitoring configuration in Management Pack for Azure SQL Database
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 2/5/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Monitoring Configuration in Management Pack for Azure SQL Database

Management Pack for Azure SQL Database provides the following key monitoring scenarios:

- [Service Availability Monitoring](#service-availability-monitoring)
- [Service Performance Monitoring](#service-performance-monitoring)
- [Service Performance Collection](#service-performance-collection)
- [Database Availability Monitoring](#database-availability-monitoring)
- [Database Performance Monitoring](#database-performance-monitoring)
- [Database Performance Collection](#database-performance-collection)
- [Active Geo-Replication Monitoring](#active-geo-replication-monitoring)
- [Elastic Pools Monitoring](#elastic-pools-monitoring)
- [Custom Query-Based Monitoring](asdmp-custom-query-monitoring.md)

## Service Availability Monitoring

The **State changes of the master database** monitor tracks availability of discovered Azure SQL Database. This monitor is not considered to be noisy and does not require any special configuration.

## Service Performance Monitoring

The management pack provides a server performance monitor that tracks situations when the number of databases per server exceeds the specified threshold.

By default, this monitor goes into the **Warning** state when 120 or more databases are created per server and goes into the **Critical** state when 135 or more databases are created per server.

In some situations, these default values are not appropriate. For example, an application may be designed to use all 150 databases for Azure SQL Database. When the default values create noise, the monitor should be disabled or the thresholds should be overridden, depending on the situation.

>[!NOTE]
>Database performance monitors roll up to service performance monitoring, which can affect the service health state.

## Service Performance Collection

The management pack provides a single rule that collects the number of databases that are hosted in each discovered Azure SQL Database.

## Database Availability Monitoring

The **State changes of the database** monitor tracks availability of the discovered databases. This monitor is not considered to be noisy and does not require any special configuration.

## Database Performance Monitoring

The management pack provides several monitors that detect situations when resource consumption has exceeded a predefined limit. Almost all of these monitors are disabled by default except for the database free space monitor.

To use disabled monitors, create an override that adjusts monitor thresholds for the database applications and enable the monitor.

The database performance monitors detect:

- Excessive storage space consumed by each database
- Excessive resources consumed by database sessions
- Excessive resources consumed by database transactions

## Database Performance Collection

There are several rules that collect the following performance information about discovered databases:

- Network usage
- Amount of resources consumed by database sessions
- Amount of resources consumed by database transactions
- Disk space consumed by each database

## Active Geo-Replication Monitoring

The management pack can monitor databases that participate in failover groups.

Active geo-replication is designed as a business continuity solution that allows the application to perform quick disaster recovery of individual databases in cases of a regional disaster or large-scale outage.

If geo-replication is enabled, the application can initiate failover to a secondary database in a different Azure region. For more information, see the [Creating and using active geo-replication - Azure SQL Database](https://docs.microsoft.com/azure/azure-sql/database/active-geo-replication-overview) article.

## Elastic Pools Monitoring

The management pack can monitor databases that are part of SQL elastic pools.

Elastic pools provide a simple resource allocation mechanism for managing and scaling multiple databases that have varying and unpredictable usage demands. For more information, see the [Elastic pools help you manage and scale multiple databases in Azure SQL Database](https://docs.microsoft.com/azure/azure-sql/database/elastic-pool-overview) article.

## Disabled Monitors

Most of the database performance monitors are disabled by default because the appropriate thresholds need to be determined based on the monitored database applications. If this functionality is required for proper database applications monitoring, do the following:

1. Determine the correct threshold values based on the expected usage patterns or observed resource consumption.
2. Override one or more of these monitors to adjust the thresholds and enable them.

Disabled monitors are as follows:

- Connections
  - Count of Failed Connection
  - Count of connections blocked by the Firewall
- Sessions
  - Sessions Count
  - Sessions Average Memory
  - Sessions Rows Returned
  - Sessions Total CPU Time
  - Sessions Total I/O
  - Sessions Total Memory
- Transactions
  - Transaction Locks Count
  - Transaction Log Space Used
  - Transaction Execution Time
- Geo-Replication Link State