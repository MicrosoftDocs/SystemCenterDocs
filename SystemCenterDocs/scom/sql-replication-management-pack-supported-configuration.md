---
ms.assetid: b849557b-8ed6-4bed-a374-a072a724dba6
title: Scope and Supported Configuration in Management Pack for SQL Server Replication
description: This article explains the scope and supported configuration for Management Pack for SQL Server Replication
author: TDzakhov
ms.author: v-tdzakhov
manager: vvithal
ms.date: 3/17/2021
ms.topic: article
ms.prod: system-center
ms.technology: operations-manager
---

# Scope and Supported Configuration in Management Pack for SQL Server Replication

Management Pack for SQL Server Replication is version-agnostic and supports discovery and monitoring of SQL Server 2012 through 2019 and higher.

## Operating Systems and Platforms

Management Pack for SQL Server Replication supports the following 64-bit operating systems and platforms:

- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016
- Windows Server 2019

## System Center Operations Manager

Management Pack for SQL Server Replication supports the following operating systems and platforms:

- System Center Operations Manager 2012 R2
- System Center Operations Manager 2016
- System Center Operations Manager 1801
- System Center Operations Manager 1807
- System Center Operations Manager 2019

A dedicated management group is not required.

## Agentless Monitoring

Management Pack for SQL Server Replication supports [agentless mode](sql-server-management-pack-monitoring-modes.md) for monitoring of SQL on Windows.

## SQL Server Features

Management Pack for SQL Server Replication works with any Express or Enterprise edition of SQL Server 2012 up to SQL Server 2019 and higher.

All SQL Server Express editions support Replication as Subscriber with Push subscriptions only. For more informarion, see [Editions and supported features of SQL Server](https://docs.microsoft.com/sql/sql-server/editions-and-components-of-sql-server-version-15).

The following features and configurations of 64-bit SQL Server Database Engine are supported:

- Distributor
  - Log Reader Agent metrics
  - Snapshot Agent metrics
  - Queue Reader Agent metrics
  - Merge Agent metrics
  - Job metrics
  - Delivery metrics
  - Space metrics
- Publisher
- Publication
  - Database Availability metrics
  - Database Configuration metrics
  - Database Performance metrics
- Subscriber
  - Job metrics
  - Performance metrics
- Subscription (Push/Pull)
  - Database Availability metrics
  - Database Configuration metrics
  - Database Performance metrics