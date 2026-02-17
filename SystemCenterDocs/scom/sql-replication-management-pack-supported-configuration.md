---
ms.assetid: b849557b-8ed6-4bed-a374-a072a724dba6
title: Scope and supported configuration in Management Pack for SQL Server Replication
description: This article explains the scope and supported configuration for Management Pack for SQL Server Replication
author: epomortseva
ms.author: v-gajeronika
ms.date: 11/01/2024
ms.topic: concept-article
ms.service: system-center
ms.subservice: operations-manager
ms.update-cycle: 1095-days
---

# Scope and Supported Configuration in Management Pack for SQL Server Replication

## SQL Server Versions

Management Pack for SQL Server Replication is version-agnostic. It supports the discovery and monitoring of SQL Server following versions:

- SQL Server 2012
  
  Due to the [Lifecycle Policy](/lifecycle/products/microsoft-sql-server-2012), this version is no longer being tested.

- SQL Server 2014
- SQL Server 2016
- SQL Server 2017
- SQL Server 2019
- SQL Server 2022

## SQL Server Features

Management Pack for SQL Server Replication works with any edition of SQL Server from Express to Enterprise and supports the following features and configurations:

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
- [Not supported] Localized versions of SQL Server
    Management Pack for SQL Server Replication support English-language version of SQL Server only.
- [Not supported] 32-bit versions of SQL Server

All SQL Server Express editions support Replication as Subscriber with Push subscriptions only. For more information, see [Editions and supported features of SQL Server](/sql/sql-server/editions-and-components-of-sql-server-version-15).

## System Center Operations Manager

::: moniker range="<=sc-om-2022"

Management Pack for SQL Server Replication supports the following operating systems and platforms:

- System Center Operations Manager 2012 R2
  
  Due to the [Lifecycle Policy](/lifecycle/products/microsoft-system-center-2012-r2-operations-manager), this version is no longer being tested.

- System Center Operations Manager 2016

::: moniker-end

- System Center Operations Manager 2019
- System Center Operations Manager 2022

::: moniker range="sc-om-2025"

- System Center Operations Manager 2025

::: moniker-end

A dedicated management group isn't required.

## Operating Systems and Platforms

Management Pack for SQL Server Replication supports the following 64-bit operating systems and platforms:

::: moniker range="<=sc-om-2022"

- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016
- Windows Server 2019
- Windows Server 2022
::: moniker-end

::: moniker range="sc-om-2025"
- Windows Server 2019
- Windows Server 2022
- Windows Server 2025

::: moniker-end

## Agentless Monitoring

Management Pack for SQL Server Replication supports [agentless mode](sql-server-management-pack-monitoring-modes.md) for monitoring of SQL on Windows.
