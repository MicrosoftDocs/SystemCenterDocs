---
title: Monitor Scenarios in Management Pack for Azure SQL Database
description: Learn about monitoring configurations in Management Pack for Azure SQL Database.
ms.date: 04/24/2025
author: Jeronika-MS
ms.author: v-gajeronika
ms.topic: how-to
ms.service: system-center
ms.subservice: operations-manager
---

# Monitor scenarios in Management Pack for Azure SQL Database

This article describes monitoring scenarios that Management Pack for Azure SQL Database supports.

## Service availability monitoring

The *State changes of the master database* monitor tracks the availability of Azure SQL Database instances that it discovers. This monitor isn't considered noisy, and it doesn't require special configuration.

## Service performance monitoring

The management pack provides a service performance monitor that tracks when the number of databases per server exceeds a set threshold.

By default, the service performance monitor displays a **Warning** status when 120 or more databases per server are created. It displays a **Critical** status when 135 or more databases per server are created.

In some scenarios, you might change the monitor from the default values. For example, an application might be designed to use all of its 150 databases for Azure SQL Database. When the default values create noise, you can turn off the monitor or change the threshold.

> [!NOTE]
> Database performance monitors roll up to service performance monitoring, which can affect the health of the service.

## Service performance collection

The management pack has a rule that collects the number of databases that are hosted in each discovered Azure SQL Database instance.

## Database availability monitoring

The *State changes of the database* monitor tracks the availability of discovered databases. This monitor isn't considered noisy, and it doesn't require special configuration.

## Database performance monitoring

The management pack includes several monitors that detect when resource consumption exceeds a predefined limit. Almost all the monitors are inactive by default except for the *Database free space* monitor.

Database performance monitors detect:

- Excessive storage space that each database consumes
- Excessive resources that database sessions consume
- Excessive resources that database transactions consume

To use monitors that are inactive, create an override that adjusts monitor thresholds for the database applications, and then make the monitor active.

## Database performance collection

Several rules in the management pack collect the following performance information about discovered databases:

- Network usage
- Amount of resources consumed by database sessions
- Amount of resources consumed by database transactions
- Disk space consumed by each database

## Active geo-replication monitoring

The management pack can monitor failover group databases.

Active geo-replication is a business continuity solution that helps an application quickly recover individual databases if a regional disaster or large-scale outage occurs.

If geo-replication is turned on, the application can initiate failover to a secondary database that's in a different Azure region. For more information, see [Create and use active geo-replication](/azure/azure-sql/database/active-geo-replication-overview).

## Elastic pool monitoring

The management pack can monitor Azure SQL Database elastic pool databases.

Elastic pools provide a simple resource allocation mechanism for managing and scaling multiple databases that have varying and unpredictable usage demands. For more information, see [Elastic pools help you manage and scale multiple databases in Azure SQL Database](/azure/azure-sql/database/elastic-pool-overview).

## Inactive monitors

Most database performance monitors aren't active by default because the appropriate thresholds are determined based on monitored database applications.

To turn on an inactive database application  monitor, follow these steps:

1. Determine the correct threshold values to use based on expected usage patterns or observed resource consumption.
1. Override one or more of the monitors to adjust the thresholds and to make them active.

The following monitors aren't active by default:

|Title|Description|
|-|-|
|Connections| Count of Failed Connection <br> Count of connections blocked by the Firewall|
|Sessions| Sessions Count <br> Sessions Average Memory <br> Sessions Rows Returned <br> Sessions Total CPU Time <br> Sessions Total I/O <br>  Sessions Total Memory|
|Transactions| Transaction Locks Count <br> Transaction Log Space Used <br> Transaction Execution Time|
|Geo-Replication Link State||

